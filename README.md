# H--project

QA toolkit: sinh Test Case CSV từ **SRS + UI** theo Template TC (MBFS).

## Skill

`.cursor/skills/Skill_CreateTCs/`

Invoke: `/Skill_CreateTCs` hoặc hỏi agent gen TC / viết testcase từ SRS.

## Layout (HATC paths)

| Path | Mục đích |
|------|----------|
| `C:\Users\hant2\Desktop\HATC\Template` | Template TC CSV |
| `Rules/rule.md` | Quy tắc QA ngắn |
| `C:\Users\hant2\Desktop\HATC\Input` | SRS theo UC |
| UI assets | N/A |
| `C:\Users\hant2\Desktop\HATC\Output` | CSV TC đã gen |

## Quick start

1. Đặt template CSV vào `C:\Users\hant2\Desktop\HATC\Template`
2. Thêm SRS vào `C:\Users\hant2\Desktop\HATC\Input`
3. Trong Cursor Agent: `/Skill_CreateTCs` với `UC-ID` (vd: UC-01)
