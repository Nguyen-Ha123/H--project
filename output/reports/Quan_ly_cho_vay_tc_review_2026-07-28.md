# TC bổ sung — Quan_ly_cho_vay (Sửa/Xóa + Process bar)

## File

`output/Quan_ly_cho_vay_fix_comment_TC_MOI.xlsx`  
Artifact: `/opt/cursor/artifacts/HATC_Output/Quan_ly_cho_vay_fix_comment_TC_MOI.xlsx`

## Vì sao là file TC_MOI riêng?

Path gốc `C:\Users\hant2\Desktop\HATC\Output\Quan_ly_cho_vay_ fix comment` **không đọc được từ cloud agent** → không thể sửa in-place mà giữ nguyên Kết quả test cũ. File này chỉ chứa **TC mới (bôi vàng)** để bạn paste vào file gốc.

## Field Inventory (tóm tắt)

| Khu vực | Nội dung |
|---------|----------|
| Sheet đầu (List) | Action Sửa / Xóa hồ sơ Uỷ thác cho vay |
| Form Sửa | Prefill, Hủy/X, required, Hình thức |
| Form Sửa — Tài sản (§5) | Tài sản đảm bảo, Mô tả TSĐB, Hiện trạng, Tính pháp lý |
| Chi tiết | Thanh process 5 bước highlight theo **trạng thái hồ sơ** |

## Plan / Breakdown

| Section | # TC | ID range |
|---------|------|----------|
| Sửa hồ sơ (sheet đầu) | 10 | TC_EDIT_001–010 |
| Xóa hồ sơ (sheet đầu) | 5 | TC_DEL_001–005 |
| Chi tiết — Process bar | 11 | TC_PROC_001–011 |
| **Tổng NEW** | **26** | bôi vàng |

## Process bar (UI)

`Chờ tiếp nhận → Chờ phân công → Chờ thẩm định → Chờ ký duyệt → Đã ký duyệt`

Highlight = trạng thái hiện tại của hồ sơ; sync với cột trạng thái trên list.

## Merge (giữ nguyên TC + kết quả cũ)

1. Mở file gốc Excel trên Desktop.
2. Copy dòng `Flag=NEW` từ sheet `TC_MOI`.
3. Paste thêm vào sheet tương ứng — **không ghi đè** dòng cũ / cột Kết quả test.
4. Đổi `ID_TC` cho khớp sequence nội bộ nếu team đánh số liên tục.
5. Giữ tô vàng để phân biệt TC mới.

## Assumptions / TBD

- Message success/validate nguyên văn — ưu tiên UI khi test (`[TBD]` trong Expected).
- Rule Sửa/Xóa theo trạng thái (đặc biệt Đã ký duyệt) — `TC_EDIT_010`, `TC_DEL_004` đánh TBD.
- SQL table — không có trong SRS cloud → không bịa.
