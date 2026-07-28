# Template Validation Map

> Rút từ Template TC mẫu. **Mỗi field cùng loại phải có đủ pattern tương ứng** — không bỏ trừ khi SRS/scope loại trừ rõ.

## Section: Tìm kiếm

### A. Default loading (1 TC)

| Item | Expected style |
|------|----------------|
| Form fields blank | Mô tả từng field = Blank |
| Dropdown default | Blank hoặc theo UI |
| Data table | All / default list + SQL SELECT (nếu template dùng) |

### B. Dropdown độc lập — correctness (1 TC)

Liệt kê **đủ options** trong Expected (bullet +).

### C. Text field search — block per field (≈11 steps / TC_ID block)

| Step | Scenario | Expected |
|------|----------|----------|
| 1–2 | Navigate + exact search | SELECT ... WHERE field = 'value' |
| 3 | Like `%xx%` | SELECT ... LIKE |
| 4 | Space trước/sau | Trim + correct result |
| 5 | Nhập space only / empty | All list |
| 6 | Page 3, search page 1 data | Correct + pagination |
| 7 | Data không tồn tại | "Không có dữ liệu" |
| 8 | Realtime: nhập nhanh, xóa, nhập lại | No lag, no lost chars |
| 9 | Copy-paste | Success |
| 10 | XSS payload | Không thực thi script |
| 11 | SQL injection | Không thực thi SQL |

**Tiền điều kiện block:** field đang test + dropdown state; các field khác blank/default.

### D. Dropdown search — per dropdown field

| Case | Expected |
|------|----------|
| Chọn option 1 | Filter SQL / UI table |
| Chọn option 2 | Filter SQL / UI table |
| Clear selection | All / default list |
| Combined + text — match | Has results |
| Combined + text — mismatch | "Không có dữ liệu" |

---

## Section: Tạo mới

### E. Default form UI (1 TC)

List **đầy đủ** field từ UI:

- Label + control type + placeholder
- Buttons: Hủy, Thêm mới / Lưu
- Icon X

### F. Popup actions (3+ TC)

| Action | Expected |
|--------|----------|
| Click outside | Không đóng / đóng (theo spec) |
| Icon X | Close, no save |
| Button Hủy | Close, no save |

### G. Required text field — per field (≈5+ steps)

| Step | Scenario | Expected |
|------|----------|----------|
| 1 | Invalid format (SRS rule) | Highlight + message SRS |
| 2 | Duplicate value | Message "đã tồn tại", không clear form |
| 3 | Duplicate + trim space | Same |
| 4 | > max length | Không cho nhập / auto cut |
| 5 | Empty required | "Vui lòng nhập + tên trường", disable submit |

**Thêm nếu SRS/UI có:**

- Copy-paste > max → auto cut
- Trim space on save
- XSS / SQL on input

### H. Optional text field — per field (lighter)

- Max length
- Invalid format (nếu có rule)
- Valid input

### I. Happy path (2+ TC)

| Case | Input | Expected |
|------|-------|----------|
| Min valid | Required filled, min boundary | Success message, row in table, INSERT SQL |
| Max valid | Max length boundaries | Success + DB verify |
| Trim space | Leading/trailing spaces | Trim on save |

### J. Mô tả / Textarea (optional field)

- Max length
- > max: không nhập / cắt chuỗi

---

## Mapping rule: SRS field → Template pattern

| SRS control type | Apply patterns |
|------------------|----------------|
| Text search | C |
| Dropdown filter | D |
| Text required create | G |
| Text optional create | H |
| Textarea | J |
| Checkbox / Date / Number | Mở rộng tương tự G (empty, invalid, boundary) |

Section-level (không gắn 1 field):

| Section item | Pattern |
|--------------|---------|
| Default search load | A |
| Dropdown options correctness | B |
| Default create form UI | E |
| Popup close actions | F |
| Happy path create | I |

---

## Continuation row style (theo Template mẫu)

- TC đầu field: có **Tiêu đề**
- Steps 2–11 cùng field: **Tiêu đề để trống**, chỉ điền Các bước + Kết quả
- Section header row: cột Tiêu đề = tên section (Tìm kiếm, Thêm mới...)

---

## Review: thiếu case thường gặp

```
□ Field SRS có nhưng không có block TC
□ Dropdown thiếu default hoặc options list TC
□ Required field thiếu empty case
□ Search field thiếu XSS/SQL (template có)
□ Expected message khác SRS
□ SQL verify thiếu hoặc sai table/column
□ Gộp 2 field vào 1 TC
```
