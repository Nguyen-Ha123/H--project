# TC Review — 4.1.11 — 2026-08-06

## Sources
- SRS: `D:\QTQ\SRS\SRS_Quỹ_Nhóm CN khai thác thông tin hoạt động quỹ_Ver1.1_final(1)` § **4.1.11**
- TC: `D:\QTQ\testcases\Cổng\MBFS_UC_4.1.9-4.1.11_ThuVien_Testcase_v0.1`
- Scope sheets: *(chưa đọc được)*
- Repo fallbacks checked: `docs/SRS/` (empty), `/mnt/d`, `D:/QTQ` — **không có file**

## Status: BLOCKED — Cloud không đọc ổ D:

Agent chạy **Cursor Cloud** (Linux VM). Path `D:\QTQ\...` **không tồn tại**.

| Check | Result |
|-------|--------|
| `D:\QTQ\SRS\...` | Not found |
| `D:\QTQ\testcases\Cổng\...` | Not found |
| `docs/SRS/` trong repo | Chỉ `.gitkeep` |
| SRS file | Không mở được |
| TC file | Không mở được |

Theo skill `/review-tc-from-srs`: **Không giả vờ đã review khi chưa đọc file.**

## Summary
| Status | Count |
|--------|------:|
| COVERED | — |
| PARTIAL | — |
| MISSING | — |
| WRONG | — |
| OBSOLETE | — |
| BLOCKED | ALL (chưa review) |

## Requirement matrix
| Rx | SRS excerpt | TC IDs | Status | Note |
|----|-------------|--------|--------|------|
| — | — | — | BLOCKED | Chờ SRS + TC |

## Gaps (priority)
### P0
- Không thể đối chiếu coverage — thiếu cả SRS §4.1.11 và file TC.

## Assumptions / TBD
- Scope mặc định = **4.1.11** (Thư viện) trong file TC chung 4.1.9–4.1.11.
- Không đụng sheet 4.1.9 / 4.1.10 trừ khi user yêu cầu full.

## Next (chọn 1)

### A. Local (khuyến nghị)
1. Cursor Desktop → repo này → checkout branch hiện tại
2. Chạy: `/review-tc-from-srs`
3. Skill đọc thẳng `D:\QTQ\...` và xuất báo cáo đầy đủ

### B. Tiếp tục trên Cloud
Attach vào chat **2 file**:
1. SRS (docx/pdf) — file chứa mục **4.1.11**
2. TC: `MBFS_UC_4.1.9-4.1.11_ThuVien_Testcase_v0.1.xlsx` (hoặc đúng extension)

Sau khi có file → chạy lại review coverage ngay (COVERED / PARTIAL / MISSING / WRONG).
