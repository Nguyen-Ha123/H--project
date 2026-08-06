# SRS + UI Extraction Guide

## Từ SRS cần trích gì

### 1. UC metadata

- UC ID, tên chức năng, actor, preconditions
- Màn hình trong scope (Tìm kiếm, Thêm, Sửa, Xóa, Xem chi tiết)

### 2. Field specification table

Tìm trong SRS các cột/bullet:

| Thuộc tính | Ví dụ |
|------------|-------|
| Tên hiển thị | Mã loại TTHC |
| Tên DB / API | Ma, Ten |
| Kiểu | Text, Dropdown, Textarea, Date |
| Bắt buộc | Có / Không |
| Độ dài | Max 50 |
| Format | Không dấu, không space |
| Unique | Có — message "Mã đã tồn tại" |
| Default | Blank, Hoạt động |
| Dropdown values | Hoạt động, Không hoạt động |

### 3. Validation & messages

Copy **nguyên văn** message lỗi từ SRS vào Expected:

- `Vui lòng nhập + tên trường`
- `Mã không bao gồm tiếng Việt có dấu và khoảng cách`
- `Không có dữ liệu`
- `Thêm mới thành công`

### 4. Business rules

- Record mới default trạng thái = Hoạt động
- Trim space đầu cuối khi lưu
- Không cho submit khi validation fail
- SQL/table name cho verify DB

### 5. Search behavior

- Exact vs like vs combined filter
- Empty search → all records
- Pagination behavior khi search

## Từ UI cần xác nhận gì

### Screenshot checklist

```
□ Title màn hình / popup
□ Mọi input visible + label + (*)
□ Placeholder text
□ Dropdown — default text khi chưa chọn
□ Buttons (Tìm kiếm, Thêm mới, Hủy, Lưu...)
□ Table columns
□ Pagination controls
□ Empty state message (nếu thấy)
```

### Live UI (Browser)

1. Màn Tìm kiếm — snapshot → inventory fields
2. Click Thêm mới — snapshot popup → inventory fields
3. Mở từng dropdown — ghi options
4. Trigger 1 validation (để biết message hiển thị thực tế) — so SRS

### Conflict resolution

| Tình huống | Xử lý |
|------------|-------|
| SRS có field, UI không thấy | Ghi BLOCKED — hỏi user |
| UI có field, SRS không mô tả | Sinh TC UI-based, ghi assumption |
| Message SRS ≠ UI | Expected ghi cả 2; ưu tiên **UI text** trong step verify, SRS trong spec note |
| Max length SRS = 50, UI cho nhập 51 | TC: không cho nhập / báo lỗi — theo UI behavior |

## Output: Field Mapping Report (mẫu)

```markdown
# Field Map — UC-01

| Field | Type | Req | SRS rule | UI confirmed | TC patterns |
|-------|------|-----|----------|--------------|-------------|
| Mã loại TTHC | text | Y | max 50, no accent | placeholder OK | create×5, search×10 |
| Trạng thái | dropdown | N | Hoạt động/KHĐ | 2 options | search×6 |

## Conflicts
- (none)

## TBD
- SQL table name: lấy từ SRS section 3.2
```

## Field Inventory (Phase 3C — bắt buộc trước gen CSV lớn)

| # | Field (UI label) | Type | Required | Options | SRS ref | Template pattern |
|---|------------------|------|----------|---------|---------|------------------|
