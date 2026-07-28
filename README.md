# H--project

QA toolkit: sinh Test Case CSV từ **SRS + UI** theo Template TC (MBFS).

## Skill

Path: `.cursor/skills/skill-createtcs/`  
Invoke trong Agent: **`/skill-createtcs`**

> Cursor chỉ nhận skill tên **chữ thường + gạch ngang**. Tên hiển thị vẫn là Skill_CreateTCs.

### Để skill hiện trên Cursor Local

1. Mở đúng repo **`H--project`** trong Cursor Desktop (không chỉ mở folder HATC).
2. Checkout branch có skill:
   ```bash
   git fetch origin
   git checkout cursor/gen-tc-srs-ui-skill-d6be
   ```
   (Hoặc merge PR #2 vào `main` rồi `git pull`.)
3. Restart Cursor / mở lại Agent chat.
4. Gõ `/skill-createtcs` — phải thấy gợi ý skill.

Nếu làm việc trong folder `Desktop\HATC`: copy cả thư mục `.cursor/skills/skill-createtcs` vào folder đó.

## Layout (HATC paths)

| Path | Mục đích |
|------|----------|
| `C:\Users\hant2\Desktop\HATC\Template` | Template TC CSV |
| `Rules/rule.md` | Quy tắc QA ngắn |
| `C:\Users\hant2\Desktop\HATC\Input` | SRS theo UC |
| UI assets | N/A |
| `C:\Users\hant2\Desktop\HATC\Output` | CSV/XLSX TC đã gen |

## Quick start (Local → ghi ổ C:)

1. Cursor Desktop + repo `H--project` + branch có skill
2. Agent: `/skill-createtcs` gen/add TC vào `C:\Users\hant2\Desktop\HATC\Output`
