---
name: feedback-over-edit-administrative-vi
description: Pattern hành chính humanizer-vi dễ over-edit văn bản khoa học/chuyên môn tốt; test bằng văn bản người viết thật.
metadata:
  type: feedback
---

Khi review skill khử "mùi AI" tiếng Việt: đừng chỉ test trên văn bản AI xấu — test cả trên văn bản người viết tốt (khoa học, chuyên môn) để bắt false positive.

**Why:** ví dụ "Sau" của skill thường thay câu trừu tượng bằng con số bịa cụ thể (ngày tháng, %, biên chế). Nếu LLM bắt chước, nó sẽ CHÈN số liệu không có trong bản gốc → sai sự thật, nguy hiểm hơn cả mùi AI. Văn bản thuyết minh khoa học thật (thuyet-minh-10000-trang) có nhiều cụm "khách quan, có cơ sở khoa học", "nền tảng", danh từ hóa hợp lệ mà pattern có thể flag nhầm.

**How to apply:** với mỗi pattern, hỏi "câu này do người chuyên môn viết đúng thì skill có sửa nhầm không?". Ưu tiên cảnh báo: (1) ví dụ Sau thêm dữ kiện không có ở Trước, (2) pattern flag thuật ngữ khoa học/danh từ hóa hợp lệ.
