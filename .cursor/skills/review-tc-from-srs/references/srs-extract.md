# SRS extract — section review

Khi đọc mục SRS (vd 4.1.11), lập checklist:

## Metadata

- [ ] Mã UC / tên
- [ ] Actor, quyền
- [ ] Preconditions
- [ ] Postconditions / output

## UI / Flow

- [ ] Màn hình, tab, popup
- [ ] Button / action (Xem, Tải, Tìm, Thêm, Sửa, Xóa, …)
- [ ] Navigation path

## Fields

Với mỗi field:

| Field | Type | Req | Max | Format | Unique | Default | Messages |

## Rules & AC

- [ ] Business rules (trim, default status, phân trang, …)
- [ ] Validation messages nguyên văn
- [ ] Success messages nguyên văn
- [ ] Acceptance criteria → map thành Rx

## Đánh số requirement

`R1`, `R2`, … — một AC/rule/field-behavior = một Rx khi có thể verify bằng TC.
