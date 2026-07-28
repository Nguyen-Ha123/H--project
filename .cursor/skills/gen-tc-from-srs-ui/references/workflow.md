# Workflow — SRS + UI + Template → CSV

## Phase 0 — Nhận lệnh

User cung cấp (hoặc lấy từ config):

- `UC-ID` (vd: UC-01)
- `--srs` path (optional)
- `--ui` URL hoặc screenshot path (optional)
- `--scope` search | create | all (default: all)

## Phase 1 — Đọc Template TC (BẮT BUỘC TRƯỚC)

1. Mở file Template từ config
2. Ghi nhận:
   - Metadata rows (Tên hệ thống, UC, Tạo bởi...)
   - Section headers: **Tìm kiếm**, **Tạo mới**, ...
   - **Pattern validate mẫu** cho từng loại field (xem template-validation-map.md)
   - Style: multi-step trong 1 TC_ID, Tiêu đề trống ở row tiếp, SQL trong Expected
3. Liệt kê **Mandatory patterns** — không được bỏ khi gen UC mới

Output nội bộ: `Template Pattern Checklist`

## Phase 2 — Phân tích SRS

Đọc SRS section của UC. Trích xuất bảng:

| Field | Control | Required | Max len | Format | Unique | Error messages | Business rules |
|-------|---------|----------|---------|--------|--------|----------------|----------------|

Nguồn SRS thường có:

- Mô tả màn hình / wireframe text
- Bảng field specification
- Validation rules
- Message catalog
- Acceptance criteria

**Thiếu rule** → đánh dấu `TBD`, dùng pattern Template mặc định, ghi chú trong report.

## Phase 3 — Phân tích UI

### 3A. Screenshot / image

- Đọc ảnh: labels, placeholders, asterisk (*), dropdown labels, buttons, table columns
- So sánh với SRS → ghi **conflicts**

### 3B. Live UI (Browser MCP)

```
browser_navigate → URL
browser_snapshot → liệt kê controls
```

Mở form Tạo mới → liệt kê đủ field. Mở dropdown → liệt kê options.

### 3C. Field Inventory (bắt buộc xuất trước khi gen CSV lớn)

| # | Field (UI label) | Type | Required | Options | SRS ref | Template pattern |
|---|------------------|------|----------|---------|---------|------------------|

User duyệt inventory nếu > 15 fields hoặc user yêu cầu `analyze`.

## Phase 4 — Ghép 3 nguồn

Cho **mỗi field**:

```
SRS rule  +  UI confirm  +  Template mandatory patterns  →  danh sách TC
```

Ví dụ field text Tìm kiếm "Mã":

- Template có: exact, like, space, empty, pagination, not found, realtime, paste, XSS, SQL
- SRS thêm: format mã không dấu, max 50
- UI: placeholder "Nhập mã (vd: LV001)"

→ Sinh block TC_00x tương tự template mẫu, thay tên field và SQL table/column từ SRS.

## Phase 5 — Lập plan TC (markdown)

| Section | Fields | Est. TC | Patterns |
|---------|--------|---------|----------|

Tổng > 30 TC → **chờ user OK**.

## Phase 6 — Sinh CSV

Thứ tự sections (theo Template):

1. **Tìm kiếm**
   - TC_001 Default loading
   - TC_002 Dropdown options (nếu có)
   - Per text field: full search block
   - Per dropdown: option + clear + combined
   - Combined search success / fail

2. **Tạo mới**
   - Default form UI (list all fields from UI)
   - Popup actions: outside click, X, Hủy
   - Per required field: empty, max, invalid, duplicate, trim space
   - Per optional field: max, invalid (lighter set)
   - Happy path min + max boundary
   - Security (XSS/SQL) nếu template có

**Đánh số:** TC_001 liên tục. `ID_UC` = UC user cung cấp.

**Cột:**

- **Tiền điều kiện**: state form (field blank/default)
- **Các bước**: navigation từ config + action cụ thể
- **Kết quả mong muốn**: message từ SRS; SQL từ SRS/Template style

## Phase 7 — Review tự động

Chạy checklist SKILL.md + template-validation-map.md.

Xuất `output/reports/{UC}_tc_review_{date}.md` nếu có gap.

## Phase 8 — Giao user

- Path CSV
- Tổng TC, breakdown theo section
- Conflicts SRS vs UI (nếu có)
- Assumptions / TBD
