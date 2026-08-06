# Project Config — Review TC from SRS (QTQ)

## Paths (user-specified)

| Key | Value |
|-----|-------|
| SRS | `D:\QTQ\SRS\SRS_Quỹ_Nhóm CN khai thác thông tin hoạt động quỹ_Ver1.1_final(1)` |
| SRS section (default) | `4.1.11` |
| TC file | `D:\QTQ\testcases\Cổng\MBFS_UC_4.1.9-4.1.11_ThuVien_Testcase_v0.1` |
| Report output | `D:\QTQ\testcases\Cổng\reports\` |

## File open hints

SRS folder/file name may thiếu extension — thử lần lượt:

- `...final(1).docx`, `.doc`, `.pdf`, hoặc file bên trong folder cùng tên

TC:

- `...ThuVien_Testcase_v0.1.xlsx`, `.xls`, `.csv`

Nếu nhiều file khớp → chọn bản version cao nhất / hỏi user.

## TC columns (typical MBFS)

```
ID_UC, ID_TC, Tiêu đề, Tiền điều kiện, Các bước thực hiện, Kết quả mong muốn
```

Có thể thêm: Kết quả test, Tester, Note — **không ghi đè** khi review/fix.

## Scope default

- Review **4.1.11** (Thư viện / mục user chỉ) trong file TC chung 4.1.9–4.1.11
- Sheet/section khác: bỏ qua trừ `--scope full` hoặc user yêu cầu

## Local vs Cloud

- **Local**: đọc/ghi `D:\QTQ\...`
- **Cloud**: path không tồn tại → yêu cầu attach SRS + TC vào chat
