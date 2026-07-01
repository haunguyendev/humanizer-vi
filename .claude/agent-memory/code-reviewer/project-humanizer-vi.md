---
name: project-humanizer-vi
description: humanizer-vi là agent skill Markdown khử "mùi AI" văn bản tiếng Việt, ưu tiên hành chính NĐ30/2020, 29 pattern, 2 chế độ.
metadata:
  type: project
---

File chính: `/Users/kanenguyen/Data/12. ChinhsuasauhoidongNT/humanizer-vi/SKILL.md` (v1.1.0). Fork tiếng Việt của blader/humanizer.

Cấu trúc: 29 pattern chia 5 nhóm (A nội dung/tu từ, B từ vựng/ngữ pháp, C định dạng, D chatbot, E rỗng/vòng vo). Pattern 29 (gạch ngang dài em/en dash) bổ sung ở 1.1.0.

Hai chế độ: Hành chính (mặc định, giữ văn phong công vụ) và Content thường (tùy chọn, cho thêm giọng điệu).

Hai section chống phá văn bản: "KHÔNG ĐƯỢC FLAG" (thể thức NĐ30) và "Dấu hiệu văn bản do người viết (giữ lại)".

**Why:** review team 260701-1117 đánh giá skill trước khi dùng thật cho văn bản nghiệm thu (thuyết minh 10.000 trang A4).
**How to apply:** khi review skill này, luôn kiểm false positive trên văn bản khoa học/chuyên môn tốt — không chỉ văn bản AI xấu.
