# Project Config — Gen TC from SRS + UI

## Paths

| Key | Value |
|-----|-------|
| Template TC | `Templates/MBFS_Testcase_Template.csv` |
| Rules | `Rules/rule.md` |
| SRS folder | `docs/SRS/` |
| UI assets | `docs/UI/` |
| Output | `output/{UC}_testcase_v{version}.csv` |
| Review reports | `output/reports/{UC}_tc_review_{date}.md` |

## Environment (MBFS)

| Key | Value |
|-----|-------|
| Staging URL | `https://qldtqg-test.dieuhanhso.vn/quan-ly-danh-muc/nhom-thu-tuc-hanh-chinh` |
| Navigation | Đăng nhập → Quản trị hệ thống → Quản lý danh mục TTHC > [module] |

## SRS files

| UC | File |
|----|------|
| UC-01 | `docs/SRS/UC-01-loai-tthc.md` `[ĐIỀN khi có SRS]` |

## UI sources

| Màn | File / URL |
|-----|------------|
| Tìm kiếm | `docs/UI/UC-01_search.png` hoặc staging URL |
| Tạo mới | `docs/UI/UC-01_create.png` hoặc mở popup trên staging |

## CSV columns

```
ID_UC, ID_TC, Tiêu đề, Tiền điều kiện, Các bước thực hiện, Kết quả mong muốn
```

## Notes

- Cập nhật bảng SRS files / UI sources khi thêm UC mới.
- Version CSV: tăng `v{n}` mỗi lần gen lại cùng UC (v1, v2, …).
- Nếu user chỉ định path khác → ưu tiên path user.
