# Review checklist

```
□ Mọi field SRS có ≥1 TC liên quan (hoặc PARTIAL có lý do)
□ Required: empty + invalid format + max length (nếu SRS có)
□ Optional: max / format nếu SRS nêu
□ Dropdown: đủ options + default
□ Search (nếu có): exact, like, empty, not found, combined
□ Messages Expected = nguyên văn SRS (hoặc ghi lệch SRS vs TC)
□ Happy path theo AC
□ Phân quyền / trạng thái nếu SRS có
□ Không gộp 2 field một TC
□ Không TC orphan (OBSOLETE) cho feature SRS đã bỏ
□ Style file TC (continuation title, section header) nhất quán
□ Kết quả test cũ không bị đụng khi chỉ review
```

## Severity khi báo cáo

| Level | Dùng khi |
|-------|----------|
| P0 | Sai expected / thiếu happy path AC bắt buộc |
| P1 | Thiếu validation quan trọng (required/unique/format) |
| P2 | Thiếu case biên / search phụ |
| P3 | Style, naming, gợi ý cải thiện |
