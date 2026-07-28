---
name: skill-createtcs
description: >-
  Skill_CreateTCs — Sinh Test Case CSV/XLSX từ SRS + UI theo Template TC (MBFS).
  Dùng khi user yêu cầu gen TC, viết testcase từ SRS, thêm TC sửa/xóa, process bar,
  field inventory, hoặc xuất CSV vào HATC Output.
---

# Skill_CreateTCs (`/skill-createtcs`)

Sinh file Test Case CSV từ **3 nguồn bắt buộc**: Template TC + SRS + UI.
Không bỏ pattern bắt buộc trong Template trừ khi SRS/scope loại trừ rõ.

## When to use

- User nói: gen TC, viết testcase, tạo CSV TC, analyze SRS/UI
- Có UC-ID (vd: UC-01) hoặc path SRS / screenshot / staging URL
- Cần field inventory trước khi gen CSV lớn

## References (đọc khi cần)

| File | Khi đọc |
|------|---------|
| [references/project-config.md](references/project-config.md) | Path template/SRS/UI/output, env, cột CSV |
| [references/srs-ui-extraction.md](references/srs-ui-extraction.md) | Trích field/rule từ SRS; checklist UI; conflict |
| [references/template-validation-map.md](references/template-validation-map.md) | Pattern bắt buộc theo loại field (C–J) |
| [references/workflow.md](references/workflow.md) | Chi tiết Phase 0–8 |

Đọc thêm `Rules/rule.md` nếu tồn tại trong repo.

## Inputs

User cung cấp (hoặc lấy từ config):

| Param | Mô tả | Default |
|-------|--------|---------|
| `UC-ID` | vd: UC-01 | bắt buộc |
| `--srs` | path SRS | `C:\Users\hant2\Desktop\HATC\Input` theo config |
| `--ui` | URL staging (UI assets = N/A) | staging URL theo config |
| `--scope` | `search` \| `create` \| `all` | `all` |
| `analyze` | chỉ inventory, chưa gen CSV | optional |

## Hard rules

1. **Đọc Template TRƯỚC** mọi thứ — ghi nhận section + mandatory patterns.
2. Mỗi field SRS/UI cùng loại phải có **đủ pattern** trong [template-validation-map.md](references/template-validation-map.md).
3. Message Expected: copy **nguyên văn** từ SRS; nếu SRS ≠ UI → ưu tiên **UI text** khi verify, ghi SRS trong note.
4. Giữ đúng cột CSV: `ID_UC, ID_TC, Tiêu đề, Tiền điều kiện, Các bước thực hiện, Kết quả mong muốn`.
5. Style continuation: TC đầu field có Tiêu đề; row tiếp cùng TC → Tiêu đề trống; section header row = tên section.
6. Không gộp 2 field vào 1 TC. Không đổi tên field/button khác SRS/UI.
7. SRS thiếu rule → `TBD` + pattern Template mặc định. Field SRS không thấy trên UI → `BLOCKED`, hỏi user.
8. Est. > 30 TC → **chờ user OK** trước khi gen CSV.
9. Inventory bắt buộc trước khi gen CSV lớn; user duyệt nếu > 15 fields hoặc lệnh `analyze`.

## Workflow (tóm tắt)

### Phase 0 — Nhận lệnh

Lấy UC-ID, paths, scope từ user/config. Xem [project-config.md](references/project-config.md).

### Phase 1 — Template TC (BẮT BUỘC TRƯỚC)

1. Mở Template từ config (`C:\Users\hant2\Desktop\HATC\Template`).
2. Ghi nhận metadata, section headers (**Tìm kiếm**, **Tạo mới**, …), pattern validate mẫu, style multi-step + SQL trong Expected.
3. Xuất nội bộ: **Template Pattern Checklist**.

### Phase 2 — Phân tích SRS

Trích bảng field: Control, Required, Max len, Format, Unique, Error messages, Business rules.
Chi tiết: [srs-ui-extraction.md](references/srs-ui-extraction.md).

### Phase 3 — Phân tích UI

- UI assets = **N/A** → bỏ screenshot inventory; chỉ dùng live staging nếu cần confirm.
- Live UI (Browser): navigate → snapshot → mở form Tạo mới → mở dropdown lấy options → trigger 1 validation so SRS.
- Xuất **Field Inventory** (bắt buộc trước gen CSV lớn).
- Không có UI → dựa SRS + Template; đánh assumption / TBD khi thiếu confirm.

### Phase 4 — Ghép 3 nguồn

Với mỗi field:

```
SRS rule + UI confirm + Template mandatory patterns → danh sách TC
```

Map control type → pattern A–J theo validation map.

### Phase 5 — Plan TC (markdown)

| Section | Fields | Est. TC | Patterns |
|---------|--------|---------|----------|

Tổng > 30 → chờ user OK.

### Phase 6 — Sinh CSV / XLSX

Thứ tự sections theo Template:

1. **Tìm kiếm**: Default loading → Dropdown options → per text (block C) → per dropdown (D) → combined
2. **Tạo mới**: Default form UI → Popup actions → per required (G) → per optional (H/J) → Happy path → Security nếu template có

- Đánh số `TC_001` liên tục; `ID_UC` = UC user cung cấp.
- **Output path:**
  - Local Windows: `C:\Users\hant2\Desktop\HATC\Output\...` (ghi thẳng)
  - Cloud: thử path trên; nếu không tồn tại → `output/` + `/opt/cursor/artifacts/` và **nói rõ** chưa ghi được ổ C:

### Phase 7 — Review tự động

Chạy checklist dưới đây + validation map. Nếu có gap → `C:\Users\hant2\Desktop\HATC\Output\reports\{UC}_tc_review_{date}.md`.

### Phase 8 — Giao user

- Path CSV
- Tổng TC + breakdown theo section
- Conflicts SRS vs UI
- Assumptions / TBD

## Review checklist (Phase 7)

```
□ Field SRS có nhưng không có block TC
□ Dropdown thiếu default hoặc options list TC
□ Required field thiếu empty case
□ Search field thiếu XSS/SQL (nếu template có)
□ Expected message khác SRS (không giải thích)
□ SQL verify thiếu hoặc sai table/column
□ Gộp 2 field vào 1 TC
□ Tiêu đề continuation / section header sai style Template
□ Scope search|create bị gen thừa section
```

## Conflict resolution

| Tình huống | Xử lý |
|------------|-------|
| SRS có field, UI không thấy | `BLOCKED` — hỏi user |
| UI có field, SRS không mô tả | TC UI-based + ghi assumption |
| Message SRS ≠ UI | Expected ghi cả 2; ưu tiên UI text khi verify |
| Max length SRS ≠ UI behavior | Theo UI behavior; note SRS |

## Output artifacts

| Artifact | Path |
|----------|------|
| CSV TC | `C:\Users\hant2\Desktop\HATC\Output\{UC}_testcase_v{version}.csv` |
| Field Map / Inventory | markdown trong chat hoặc `C:\Users\hant2\Desktop\HATC\Output\reports\` |
| Review gap | `C:\Users\hant2\Desktop\HATC\Output\reports\{UC}_tc_review_{date}.md` |

## Cấm

- Bỏ sót mandatory pattern Template cho bất kỳ field trong scope
- Gen CSV lớn trước khi có Field Inventory
- Đổi tên field/button/message khác SRS/UI đã confirm
- Tự bịa SQL table/column khi SRS không có — đánh `TBD`
