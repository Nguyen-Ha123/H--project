---
name: review-tc-from-srs
description: >-
  Reviews MBFS/QTQ test cases against SRS section requirements (default UC 4.1.11
  Thư viện). Finds gaps, wrong expected results, missing field cases, and outdated
  steps. Use when the user asks to review TC, đối chiếu SRS, check coverage 4.1.11,
  or audit file MBFS_UC_4.1.9-4.1.11_ThuVien_Testcase.
disable-model-invocation: true
---

# Review TC from SRS (`/review-tc-from-srs`)

Đối chiếu Test Case với SRS → báo cáo thiếu / sai / dư / lệch message.

## When to use

- Review TC, đối chiếu SRS, check coverage, audit testcase
- User chỉ SRS section (vd: **4.1.11**) + file TC
- Sau khi gen TC bằng `/skill-createtcs` và cần kiểm tra lại

## Config

Đọc [references/project-config.md](references/project-config.md) trước.

**Default (verbatim paths user):**

| Key | Path |
|-----|------|
| SRS | `D:\QTQ\SRS\SRS_Quỹ_Nhóm CN khai thác thông tin hoạt động quỹ_Ver1.1_final(1)` — mục **4.1.11** |
| TC file | `D:\QTQ\testcases\Cổng\MBFS_UC_4.1.9-4.1.11_ThuVien_Testcase_v0.1` |
| Report out | cùng folder TC, hoặc `D:\QTQ\testcases\Cổng\reports\` |

Thử mở với extension thường gặp: `.docx` / `.doc` / `.pdf` (SRS), `.xlsx` / `.xls` / `.csv` (TC).

## Local vs Cloud

| Môi trường | Hành vi |
|------------|---------|
| **Local** (Windows) | Đọc/ghi thẳng path `D:\QTQ\...` |
| **Cloud** | Không có ổ D: → báo rõ; yêu cầu user attach SRS + TC hoặc chạy Local |

Không giả vờ đã đọc file khi path không tồn tại.

## Inputs

| Param | Default |
|-------|---------|
| `--srs` | path SRS trong config |
| `--section` | `4.1.11` |
| `--tc` | path TC trong config |
| `--scope` | section trong TC tương ứng 4.1.11 (vd sheet/tab Thư viện) |
| `--fix` | nếu user OK → đề xuất / append TC thiếu (bôi vàng); **không sửa Kết quả test cũ** |

## Workflow

### 1. Mở SRS — mục section

Trích từ mục **4.1.11** (hoặc `--section`):

- UC ID / tên chức năng / actor / preconditions
- Màn hình, button, flow
- Bảng field (label, type, required, max, format, unique, default)
- Message lỗi / thành công **nguyên văn**
- Business rules, phân quyền, trạng thái
- Acceptance criteria

Output nội bộ: **SRS Requirement Checklist** (list đánh số R1, R2, …).

Chi tiết trích: [references/srs-extract.md](references/srs-extract.md).

### 2. Mở file TC

- Liệt kê sheet / section liên quan **4.1.11** (không review 4.1.9–4.1.10 trừ khi user yêu cầu full file)
- Inventory: ID_TC, tiêu đề, field/màn cover, expected
- Giữ nguyên cột Kết quả test — chỉ đọc

### 3. Mapping SRS ↔ TC

Với mỗi requirement Rx:

| Status | Nghĩa |
|--------|--------|
| COVERED | Có TC đủ, expected khớp SRS |
| PARTIAL | Có TC nhưng thiếu case / message lệch |
| MISSING | Không có TC |
| WRONG | TC trái SRS (step/expected/field sai) |
| OBSOLETE | TC cho thứ SRS đã bỏ |
| BLOCKED | SRS thiếu chi tiết — không kết luận |

### 4. Review checklist

Chạy [references/review-checklist.md](references/review-checklist.md).

Ưu tiên bắt:

- Field SRS không có block TC
- Required thiếu empty / invalid / max
- Message Expected ≠ SRS (ghi cả 2 nếu UI khác — note)
- Search thiếu exact/like/empty/not found (nếu UC có search)
- CRUD thiếu theo scope UC
- Gộp 2 field / trùng ý
- Tiêu đề continuation / section header sai style file TC

### 5. Xuất báo cáo

Ghi markdown (và optional xlsx):

`{TC_basename}_review_{section}_{date}.md`

Template báo cáo: xem [references/report-template.md](references/report-template.md).

Tóm tắt cho user:

1. Path SRS + TC đã dùng
2. Tổng R / COVERED / PARTIAL / MISSING / WRONG
3. Top gaps cần fix
4. Assumptions / TBD

### 6. Fix (chỉ khi user yêu cầu)

- Append TC thiếu vào file TC — **bôi vàng**, Flag=`NEW`
- Sửa expected WRONG chỉ khi user confirm
- **Cấm** xóa/ghi đè Kết quả test đã có

## Hard rules

1. SRS section chỉ định là nguồn truth cho coverage.
2. Message: so khớp nguyên văn SRS; lệch → đánh PARTIAL/WRONG + quote cả 2.
3. Không bịa rule/SQL khi SRS không có → TBD/BLOCKED.
4. Scope mặc định = **4.1.11**; không đụng sheet khác trừ khi user nói full.
5. Cloud không đọc được `D:\` → dừng và hướng dẫn Local / attach file.

## Related

Gen TC mới: `/skill-createtcs`
