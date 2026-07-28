# QA Rules — Gen TC

Khi gen Test Case từ SRS + UI:

1. Tuân thủ skill `Skill_CreateTCs` (`.cursor/skills/Skill_CreateTCs/`).
2. Template TC là nguồn pattern bắt buộc — không bỏ case trừ khi scope loại trừ.
3. Message Expected copy nguyên văn SRS; conflict SRS/UI → ưu tiên UI text khi verify.
4. Field SRS không thấy trên UI → BLOCKED, hỏi user.
5. Output CSV đúng cột template; continuation row: Tiêu đề trống cho step tiếp cùng TC.
