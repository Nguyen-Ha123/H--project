# Project Config — Gen TC from SRS + UI

## Paths

| Key | Value |
|-----|-------|
| Template TC | `C:\Users\hant2\Desktop\HATC\Template` |
| Rules | `Rules/rule.md` |
| SRS folder | `C:\Users\hant2\Desktop\HATC\Input` |
| UI assets | N/A |
| Output | `C:\Users\hant2\Desktop\HATC\Output` |
| Review reports | `C:\Users\hant2\Desktop\HATC\Output\reports\{UC}_tc_review_{date}.md` |

## Environment (MBFS)

| Key | Value |
|-----|-------|
| Staging URL | `https://qldtqg-test.dieuhanhso.vn/quan-ly-danh-muc/nhom-thu-tuc-hanh-chinh` |
| Navigation | Đăng nhập → Quản trị hệ thống → Quản lý danh mục TTHC > [module] |

## SRS files

| UC | File |
|----|------|
| UC-01 | `C:\Users\hant2\Desktop\HATC\Input\` `[ĐIỀN tên file SRS khi có]` |

## UI sources

| Màn | File / URL |
|-----|------------|
| Tìm kiếm | N/A (UI assets không dùng) — dùng staging URL nếu cần |
| Tạo mới | N/A — mở popup trên staging nếu cần |

## CSV columns

```
ID_UC, ID_TC, Tiêu đề, Tiền điều kiện, Các bước thực hiện, Kết quả mong muốn
```

## Notes

- Template: đọc file CSV trong folder `C:\Users\hant2\Desktop\HATC\Template`.
- SRS: lấy file từ `C:\Users\hant2\Desktop\HATC\Input`.
- Output CSV/XLSX: ghi vào `C:\Users\hant2\Desktop\HATC\Output` (vd: `{UC}_testcase_v{version}.csv`).
- UI assets = N/A → bỏ Phase 3A screenshot; chỉ dùng live staging / SRS khi cần confirm UI.
- Cập nhật bảng SRS files khi thêm UC mới.
- Version CSV: tăng `v{n}` mỗi lần gen lại cùng UC (v1, v2, …).
- Nếu user chỉ định path khác → ưu tiên path user.

## Output path — Local vs Cloud (BẮT BUỘC)

| Môi trường | Ghi Output đi đâu |
|------------|-------------------|
| **Cursor Local** (agent trên máy Windows user) | **Bắt buộc** ghi thẳng `C:\Users\hant2\Desktop\HATC\Output` |
| **Cursor Cloud** (máy ảo Linux) | **Không có ổ C:** → ghi `output/` trong repo + `/opt/cursor/artifacts/` để user tải. Báo rõ không ghi được Desktop. |

Không giả vờ đã ghi ổ C: khi chạy Cloud. Muốn auto-add vào Desktop → user phải chạy skill bằng **Local agent**.
