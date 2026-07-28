# H--project

QA toolkit: sinh Test Case CSV từ **SRS + UI** theo Template TC (MBFS).

## Skill

`.cursor/skills/Skill_CreateTCs/`

Invoke: `/Skill_CreateTCs` hoặc hỏi agent gen TC / viết testcase từ SRS.

## Layout

| Path | Mục đích |
|------|----------|
| `Templates/` | Template TC CSV |
| `Rules/rule.md` | Quy tắc QA ngắn |
| `docs/SRS/` | SRS theo UC |
| `docs/UI/` | Screenshot UI |
| `output/` | CSV TC đã gen |
| `output/reports/` | Review / gap reports |

## Quick start

1. Đặt template vào `Templates/MBFS_Testcase_Template.csv`
2. Thêm SRS vào `docs/SRS/`, screenshot vào `docs/UI/`
3. Trong Cursor Agent: `/Skill_CreateTCs` với `UC-ID` (vd: UC-01)
