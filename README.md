# H--project

QA toolkit: sinh Test Case CSV từ **SRS + UI** theo Template TC (MBFS).

## Skills

| Invoke | Path | Việc |
|--------|------|------|
| `/skill-createtcs` | `.cursor/skills/skill-createtcs/` | Gen TC từ SRS + UI |
| `/review-tc-from-srs` | `.cursor/skills/review-tc-from-srs/` | Review TC đối chiếu SRS (QTQ 4.1.11) |

### Local — để skill hiện

1. Mở repo **H--project** trong Cursor Desktop  
2. `git fetch && git checkout cursor/gen-tc-srs-ui-skill-d6be`  
3. Mở lại Agent → gõ `/skill-createtcs` hoặc `/review-tc-from-srs`

### Review TC (QTQ) — Local only cho ổ D:

```
/review-tc-from-srs
SRS: D:\QTQ\SRS\SRS_Quỹ_Nhóm CN khai thác thông tin hoạt động quỹ_Ver1.1_final(1) mục 4.1.11
TC:  D:\QTQ\testcases\Cổng\MBFS_UC_4.1.9-4.1.11_ThuVien_Testcase_v0.1
```

Cloud không đọc `D:\` — cần Local hoặc attach file.

## Layout (HATC paths)

| Path | Mục đích |
|------|----------|
| `C:\Users\hant2\Desktop\HATC\Template` | Template TC CSV |
| `Rules/rule.md` | Quy tắc QA ngắn |
| `C:\Users\hant2\Desktop\HATC\Input` | SRS theo UC |
| UI assets | N/A |
| `C:\Users\hant2\Desktop\HATC\Output` | CSV/XLSX TC đã gen |

## Quick start

**Gen TC (Local → HATC Output):** `/skill-createtcs`  
**Review TC (Local → QTQ D:):** `/review-tc-from-srs`
