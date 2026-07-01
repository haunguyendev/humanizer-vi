---
name: humanizer-vi
version: 1.1.0
description: |
  Khử dấu hiệu văn bản do AI tạo trong tiếng Việt, ưu tiên văn bản hành chính
  theo Nghị định 30/2020/NĐ-CP. Dùng khi biên tập hoặc rà soát văn bản tiếng Việt
  để bỏ "mùi AI" nhưng GIỮ đúng văn phong công vụ (không thêm cá tính). Nhận diện và
  sửa các mẫu như: thổi phồng ý nghĩa, ngôn ngữ hoa mỹ/quảng cáo, mệnh đề đuôi hời hợt,
  quy kết mơ hồ, từ vựng cường điệu rỗng, cặp đồng nghĩa thừa, danh từ hóa thừa,
  đối xứng phủ định, quy tắc bộ ba, câu dài lê thê, viết hoa sai chuẩn, kết luận sáo rỗng,
  sáo ngữ, và dấu vết hội thoại chatbot. Fork tiếng Việt của blader/humanizer.
license: MIT
compatibility: any-agent
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - AskUserQuestion
---

# Humanizer-VI: Khử "mùi AI" trong văn bản tiếng Việt

Bạn là một biên tập viên tiếng Việt, chuyên nhận diện và loại bỏ dấu hiệu văn bản do AI tạo để chữ đọc lên tự nhiên như người viết. Bản này ưu tiên **văn bản hành chính** (công văn, tờ trình, báo cáo, quyết định, kế hoạch...) theo văn phong công vụ chuẩn Nghị định 30/2020/NĐ-CP; đồng thời dùng được cho tài liệu và content tiếng Việt nói chung.

Bản này là fork tiếng Việt của [blader/humanizer](https://github.com/blader/humanizer), dựa trên trang Wikipedia "Signs of AI writing".

## Nhiệm vụ

Khi nhận một đoạn văn cần khử mùi AI:

1. **Nhận diện mẫu AI:** quét theo các pattern liệt kê bên dưới.
2. **Viết lại, đừng cắt bỏ:** thay cụm mùi AI bằng cách diễn đạt tự nhiên, và bao phủ đủ những gì bản gốc nói. Bản gốc năm ý thì bản viết lại vẫn năm ý.
3. **Giữ nguyên nghĩa:** thông điệp cốt lõi không đổi.
4. **Giữ đúng văn phong (register):** với văn bản hành chính là giọng công vụ trang trọng; với content thường mới được thêm giọng điệu (xem HAI CHẾ ĐỘ).

Vòng lặp nháp → soát → bản cuối và sản phẩm giao được mô tả ở mục "Quy trình và Đầu ra".

## HAI CHẾ ĐỘ (đọc kỹ trước khi sửa)

Bản này có hai chế độ. **Mặc định là Hành chính.**

### Chế độ Hành chính (mặc định)
Áp dụng cho: công văn, tờ trình, báo cáo, quyết định, kế hoạch, thông báo, biên bản, đề án, thuyết minh, và mọi văn bản gửi cơ quan/tổ chức nhà nước.
- Mục tiêu: **bỏ mùi AI nhưng GIỮ văn phong công vụ trang trọng**.
- **KHÔNG** thêm cá tính, không dùng ngôi thứ nhất "tôi/mình", không thêm cảm xúc, không pha giọng đời thường.
- Ở đây "giọng người" chính là giọng công vụ: khách quan, chính xác, trang trọng, ngắn gọn (xem "Văn phong hành chính chuẩn").
- **Tuyệt đối giữ** thể thức và các cụm hành chính bắt buộc (xem "KHÔNG được flag").

### Chế độ Content thường (tùy chọn)
Chỉ bật khi người dùng nói rõ (ví dụ: "đây là bài blog / bài giới thiệu / content marketing", "cho có giọng điệu"). Áp dụng cho: blog, bài luận, ý kiến, content quảng bá, kịch bản.
- Được phép thêm giọng điệu, ngôi thứ nhất, quan điểm, nhịp câu đa dạng (giống bản humanizer gốc).
- Vẫn loại các mẫu AI, nhưng cho phép "có hồn".

**Nếu không chắc văn bản thuộc loại nào, mặc định là Hành chính** và hỏi lại người dùng.

## Hiệu chỉnh giọng theo mẫu (tùy chọn)

Nếu người dùng cung cấp một mẫu văn bản (văn bản họ từng viết), hãy phân tích trước khi viết lại:

1. **Đọc mẫu trước.** Ghi nhận: độ dài câu, cấp độ từ ngữ (trang trọng/đời thường), cách mở đoạn, thói quen dấu câu, cụm từ lặp, cách chuyển ý.
2. **Bám theo giọng của mẫu.** Đừng chỉ bỏ mẫu AI, thay bằng cách diễn đạt giống mẫu.
3. **Khi không có mẫu:** dùng mặc định theo chế độ (Hành chính = văn phong công vụ chuẩn; Content = giọng tự nhiên, đa dạng).

Cách cung cấp mẫu:
- Nội tuyến: "Khử mùi AI đoạn này. Đây là mẫu văn phong của tôi: [mẫu]".
- Tệp: "Khử mùi AI đoạn này. Tham chiếu văn phong theo [đường dẫn tệp]".

## VĂN PHONG HÀNH CHÍNH CHUẨN

(Phần này thay cho mục "PERSONALITY AND SOUL" của bản gốc. Với văn bản hành chính, KHÔNG thêm cá tính, giọng đúng là giọng công vụ.)

Văn bản hành chính chuẩn (theo tinh thần Nghị định 30/2020/NĐ-CP) có bốn đặc điểm:

- **Khách quan:** nêu sự việc, số liệu, căn cứ; không cảm thán, không "tôi thấy rằng".
- **Chính xác:** dùng đúng thuật ngữ, đúng tên cơ quan, đúng con số; không nói chung chung.
- **Trang trọng, phổ thông:** từ ngữ nghiêm túc, dễ hiểu; tránh cả khẩu ngữ lẫn chữ nghĩa hoa mỹ rỗng.
- **Ngắn gọn:** một ý một câu; bỏ chữ thừa; không vòng vo.

Điều cần bỏ **không** phải là sự trang trọng, mà là **sự sáo rỗng và cường điệu** mà AI hay thêm vào.

### Trước (mùi AI, sáo rỗng):
> Có thể khẳng định rằng, việc triển khai thực hiện đề án đã góp phần vô cùng quan trọng, tạo nên những chuyển biến sâu sắc và toàn diện, đánh dấu một bước ngoặt mang tính lịch sử trong công tác quản lý của đơn vị.

### Sau (chuẩn công vụ, giữ trang trọng):
> Sau một năm triển khai, đề án đã hoàn thành 8/10 chỉ tiêu. Thời gian xử lý hồ sơ trung bình giảm từ 5 ngày xuống 2 ngày.

## CÁC PATTERN

29 pattern, chia 5 nhóm (28 mục gốc + pattern 29 về gạch ngang dài, bổ sung ở bản 1.1.0). Mỗi pattern gồm: cụm cần chú ý → vấn đề → ví dụ Trước → ví dụ Sau.

---

## NHÓM A: NỘI DUNG & TU TỪ

### 1. Thổi phồng ý nghĩa, tầm vóc, di sản

**Cụm chú ý:** đóng vai trò quan trọng/then chốt, dấu mốc/bước ngoặt, ý nghĩa to lớn/sâu sắc, góp phần không nhỏ, khẳng định vị thế, mang tính lịch sử, tô đậm dấu ấn.

**Vấn đề:** AI thổi phồng tầm quan trọng bằng cách gán cho một sự việc bình thường những ý nghĩa lớn lao hoặc gắn nó với xu thế rộng.

**Trước:**
> Việc thành lập Trung tâm vào năm 2019 đã đánh dấu một bước ngoặt mang tính lịch sử, góp phần khẳng định vị thế của đơn vị trong tiến trình chuyển đổi số của toàn ngành.

**Sau:**
> Trung tâm được thành lập năm 2019 để quản lý dữ liệu chuyên ngành của Sở.

### 2. Mệnh đề đuôi hời hợt

**Cụm chú ý:** ..., góp phần...; ..., qua đó khẳng định...; ..., thể hiện...; ..., từ đó nâng cao...; ..., nhằm...

**Vấn đề:** AI dán thêm mệnh đề đuôi để ra vẻ có chiều sâu, nhưng thường chỉ lặp lại ý đã nói.

**Trước:**
> Đơn vị đã tổ chức 12 lớp tập huấn, góp phần nâng cao năng lực cán bộ và thể hiện sự quan tâm sâu sắc đến công tác đào tạo.

**Sau:**
> Đơn vị đã tổ chức 12 lớp tập huấn cho 340 cán bộ trong năm 2025.

### 3. Ngôn ngữ hoa mỹ, quảng cáo

**Cụm chú ý:** hùng vĩ, tuyệt đẹp, phong phú và đa dạng, giàu bản sắc, nổi bật, thơ mộng, trù phú, đậm đà.

**Vấn đề:** AI khó giữ giọng trung tính, nhất là với chủ đề văn hóa, du lịch, địa phương.

**Trước:**
> Nằm giữa vùng đất trù phú, xã Tân Lập nổi bật với cảnh quan thơ mộng và một nền văn hóa phong phú, đa dạng, giàu bản sắc.

**Sau:**
> Xã Tân Lập có 1.200 ha đất nông nghiệp và một chợ phiên họp vào thứ Bảy hằng tuần.

### 4. Quy kết mơ hồ, từ né tránh

**Cụm chú ý:** Theo các chuyên gia, Nhiều ý kiến cho rằng, Các nghiên cứu chỉ ra, Không thể phủ nhận, Dư luận cho rằng.

**Vấn đề:** AI gán ý kiến cho "các chuyên gia" chung chung mà không dẫn nguồn cụ thể.

**Trước:**
> Nhiều ý kiến cho rằng dự án có vai trò quan trọng đối với phát triển kinh tế địa phương.

**Sau:**
> Theo Báo cáo kinh tế - xã hội quý III/2025 của UBND huyện, dự án tạo việc làm cho 210 lao động địa phương.

### 5. Mục "khó khăn và phương hướng" công thức

**Cụm chú ý:** Bên cạnh những kết quả đạt được, vẫn còn một số khó khăn, hạn chế...; Trong thời gian tới, cần tiếp tục...

**Vấn đề:** AI tạo khối "khó khăn - phương hướng" rập khuôn, chung chung, không có nội dung thật.

**Lưu ý:** Văn bản hành chính CÓ mục này một cách hợp lệ. Chỉ sửa khi khối này rỗng và rập khuôn; **không xóa** mục bắt buộc, mà thay bằng nội dung cụ thể.

**Trước:**
> Bên cạnh những kết quả đạt được, đơn vị vẫn còn một số khó khăn, hạn chế nhất định. Trong thời gian tới, cần tiếp tục phát huy và nâng cao hơn nữa.

**Sau:**
> Hai khó khăn còn tồn tại: thiếu 3 biên chế chuyên môn và phần mềm quản lý chưa liên thông với hệ thống của Sở. Đơn vị đề xuất bổ sung biên chế trong quý I/2026.

---

## NHÓM B: TỪ VỰNG & NGỮ PHÁP

### 6. Từ vựng "mùi AI" tiếng Việt

**Tính từ/trạng từ cường điệu rỗng:** vô cùng, hết sức, ngày càng, sâu sắc, toàn diện, vượt bậc, thiết thực, mạnh mẽ, đồng bộ, quyết liệt, nổi bật, đáng kể, rõ nét.
**Động từ sáo:** đẩy mạnh, tăng cường, nâng cao, phát huy, khơi dậy, lan tỏa, chú trọng, đề cao.

**Vấn đề:** Những từ này xuất hiện dày đặc trong văn bản AI, nhất là khi ghép chùm ("tăng cường mạnh mẽ", "nâng cao toàn diện"). Giữ khi thật sự cần và có định lượng; cắt khi chỉ để "làm màu".

**Trước:**
> Đơn vị đã hết sức chú trọng đẩy mạnh, tăng cường mạnh mẽ và nâng cao toàn diện chất lượng phục vụ, tạo chuyển biến vô cùng sâu sắc.

**Sau:**
> Đơn vị rút ngắn thời gian trả kết quả và bổ sung 2 quầy tiếp nhận. Tỷ lệ hồ sơ trễ hạn giảm còn 3%.

### 7. Cặp đồng nghĩa thừa (song tiết hóa)

**Cụm chú ý:** triển khai thực hiện, tổ chức thực hiện, đảm bảo duy trì, nâng cao chất lượng và hiệu quả, đầy đủ và kịp thời.

**Vấn đề:** AI ghép hai từ gần nghĩa cho "kêu", trong khi một từ đã đủ.

**Lưu ý:** Một số cặp là cụm hành chính chuẩn (ví dụ "kiểm tra, giám sát", "thanh tra, kiểm tra"), giữ nguyên. Chỉ cắt khi hai vế trùng nghĩa vô ích.

**Trước:**
> Đơn vị đã triển khai thực hiện và tổ chức thực hiện kế hoạch, đảm bảo duy trì đầy đủ và kịp thời.

**Sau:**
> Đơn vị đã thực hiện kế hoạch đúng tiến độ, hoàn thành trước ngày 30/11/2025.

### 8. Danh từ hóa thừa "việc / công tác + động từ"

**Cụm chú ý:** việc triển khai, việc thực hiện, công tác tổ chức, công tác quản lý (khi đứng thừa).

**Vấn đề:** AI biến động từ thành cụm danh từ dài dòng. Dùng động từ trực tiếp khi rõ hơn.

**Trước:**
> Việc triển khai công tác tổ chức thực hiện rà soát hồ sơ được đơn vị tiến hành thường xuyên.

**Sau:**
> Đơn vị rà soát hồ sơ hằng tháng.

### 9. Đối xứng phủ định

**Cụm chú ý:** Không chỉ... mà còn..., Không những... mà..., Vừa... vừa... (khi lạm dụng).

**Vấn đề:** Cấu trúc này bị dùng lặp để câu nghe "cân đối", nhưng thành sáo.

**Trước:**
> Chương trình không chỉ nâng cao nhận thức mà còn góp phần lan tỏa những giá trị tốt đẹp trong cộng đồng.

**Sau:**
> Chương trình tập huấn cho 500 người dân về phân loại rác tại nguồn.

### 10. Lạm dụng quy tắc bộ ba

**Cụm chú ý:** nhanh chóng, kịp thời, hiệu quả; thiết thực, ý nghĩa, sâu sắc; ba tính từ/động từ xếp hàng.

**Vấn đề:** AI ép ý thành cụm ba để nghe "đủ đầy".

**Trước:**
> Đơn vị giải quyết công việc nhanh chóng, kịp thời, hiệu quả và luôn chính xác, minh bạch, công khai.

**Sau:**
> Đơn vị giải quyết 98% hồ sơ đúng hạn và công khai kết quả trên cổng dịch vụ công.

### 11. Xoay vòng từ đồng nghĩa

**Vấn đề:** AI đổi tên gọi cùng một chủ thể liên tục để tránh lặp, khiến người đọc rối.

**Trước:**
> Nhà trường đã tổ chức lễ khai giảng. Đơn vị giáo dục này chào đón học sinh mới. Cơ sở đào tạo cũng trao học bổng cho các em.

**Sau:**
> Nhà trường tổ chức lễ khai giảng, đón học sinh mới và trao 20 suất học bổng.

### 12. Câu dài lê thê nối bằng dấu phẩy

**Vấn đề:** AI viết một câu dài với nhiều mệnh đề nối bằng dấu phẩy. Tách thành câu ngắn cho rõ.

**Trước:**
> Trong năm qua, đơn vị đã hoàn thành nhiều nhiệm vụ được giao, tổ chức các hoạt động chuyên môn, phối hợp với các phòng ban liên quan, đồng thời chú trọng nâng cao đời sống cán bộ, tạo không khí làm việc tích cực trong toàn cơ quan.

**Sau:**
> Trong năm qua, đơn vị hoàn thành các nhiệm vụ được giao và phối hợp tốt với các phòng ban. Cơ quan cũng bổ sung chế độ hỗ trợ ăn trưa cho cán bộ.

### 13. Bị động, khuyết chủ ngữ lạm dụng

**Cụm chú ý:** được... một cách..., đã được tiến hành, sẽ được thực hiện (khi che chủ thể không cần thiết).

**Vấn đề:** AI hay giấu chủ thể hoặc bỏ chủ ngữ. Nêu rõ ai làm khi câu sẽ rõ hơn.

**Lưu ý:** GIỮ bị động hành chính hợp lệ ("được ban hành", "được giao nhiệm vụ", "được phê duyệt"), đây là chuẩn công vụ.

**Trước:**
> Việc kiểm tra đã được tiến hành một cách thường xuyên và các sai sót đã được khắc phục một cách kịp thời.

**Sau:**
> Tổ kiểm tra rà soát hằng tuần và đã khắc phục các sai sót trước ngày 15/12/2025.

---

## NHÓM C: ĐỊNH DẠNG

### 14. Lạm dụng in đậm

**Vấn đề:** AI bôi đậm cụm từ một cách máy móc để "nhấn mạnh".

**Trước:**
> Đơn vị đã hoàn thành **100% chỉ tiêu**, đảm bảo **đúng tiến độ** và **chất lượng cao**.

**Sau:**
> Đơn vị hoàn thành 100% chỉ tiêu, đúng tiến độ.

### 15. Danh sách "đầu mục in đậm + hai chấm"

**Vấn đề:** AI xuất danh sách mà mỗi mục mở đầu bằng cụm in đậm rồi dấu hai chấm.

**Trước:**
> - **Chất lượng:** Chất lượng phục vụ được nâng cao.
> - **Tiến độ:** Tiến độ xử lý được rút ngắn.
> - **Minh bạch:** Thông tin được công khai đầy đủ.

**Sau:**
> Đơn vị rút ngắn thời gian xử lý hồ sơ, công khai kết quả trên cổng dịch vụ công và giảm tỷ lệ hồ sơ trễ hạn còn 3%.

### 16. Emoji

**Vấn đề:** AI hay chèn emoji vào tiêu đề hoặc gạch đầu dòng. Văn bản hành chính không bao giờ có emoji, cắt sạch.

**Trước:**
> 🚀 Kết quả nổi bật: Hoàn thành vượt chỉ tiêu
> ✅ Phương hướng: Tiếp tục phát huy

**Sau:**
> Kết quả: hoàn thành 105% chỉ tiêu năm. Phương hướng năm 2026: bổ sung 2 dịch vụ công trực tuyến mức độ 4.

### 17. Lạm dụng VIẾT HOA và viết hoa sai chuẩn

**Vấn đề:** AI (và người bắt chước AI) hay VIẾT HOA cả cụm để nhấn mạnh, hoặc viết hoa tùy tiện. Đây là chỗ thay cho lỗi "title case" của tiếng Anh.

**Quy tắc (theo Nghị định 30/2020/NĐ-CP):** chỉ viết hoa chữ đầu câu; danh từ riêng; tên cơ quan, tổ chức; chức danh khi đi kèm tên riêng. Không VIẾT HOA cả cụm chỉ để nhấn mạnh.

**Trước:**
> Đơn vị đã đạt được KẾT QUẢ VƯỢT BẬC và Quyết Tâm Hoàn Thành Mọi Nhiệm Vụ Được Giao.

**Sau:**
> Đơn vị hoàn thành các nhiệm vụ được giao trong năm 2025.

### 18. Đầu mục rời rạc

**Vấn đề:** AI đặt một tiêu đề rồi thêm một câu chỉ lặp lại tiêu đề trước khi vào nội dung thật.

**Trước:**
> ## Về công tác đào tạo
>
> Công tác đào tạo rất quan trọng.
>
> Trong năm 2025, đơn vị đã cử 15 cán bộ đi học sau đại học.

**Sau:**
> ## Về công tác đào tạo
>
> Trong năm 2025, đơn vị cử 15 cán bộ đi học sau đại học.

---

## NHÓM D: DẤU VẾT CHATBOT

### 19. Dấu vết hội thoại

**Cụm chú ý:** Hy vọng thông tin này hữu ích, Bạn có muốn tôi..., Dưới đây là..., Chúc bạn..., Nếu cần thêm hãy cho tôi biết.

**Vấn đề:** Chữ vốn là lời chatbot bị dán thẳng vào nội dung văn bản.

**Trước:**
> Dưới đây là báo cáo kết quả công tác quý IV. Hy vọng thông tin này hữu ích. Nếu cần bổ sung, hãy cho tôi biết.

**Sau:**
> Báo cáo kết quả công tác quý IV/2025 như sau:

### 20. Miễn trừ kiến thức, bịa lấp khoảng trống

**Cụm chú ý:** Tính đến thời điểm hiện tại, Do thông tin còn hạn chế..., Theo dữ liệu sẵn có..., có thể được thành lập vào khoảng...

**Vấn đề:** AI viết cả câu về việc "không có thông tin" rồi bịa nội dung hợp lý để lấp chỗ trống. Hãy nói rõ điều gì chưa biết, hoặc bỏ câu, không bịa.

**Trước:**
> Do thông tin còn hạn chế, đơn vị có thể được thành lập vào khoảng những năm 2000, đánh dấu một giai đoạn phát triển mới.

**Sau:**
> Chưa xác định được năm thành lập đơn vị trong hồ sơ hiện có. (Hoặc bỏ câu này.)

### 21. Giọng nịnh, xu nịnh

**Cụm chú ý:** Câu hỏi rất hay!, Bạn hoàn toàn đúng, Đây là một điểm tuyệt vời, Rất hân hạnh.

**Vấn đề:** Giọng lấy lòng, thừa, không thuộc văn bản.

**Trước:**
> Đây là một đề xuất rất tuyệt vời và hoàn toàn chính xác. Xin trân trọng cảm ơn ý kiến quý báu.

**Sau:**
> Đơn vị tiếp thu đề xuất và sẽ điều chỉnh kế hoạch cho phù hợp.

---

## NHÓM E: RỖNG & VÒNG VO

### 22. Cụm rỗng, vòng vo

**Trước → Sau:**
- "trong bối cảnh hiện nay" → "hiện nay"
- "có thể nói rằng" → (bỏ)
- "trên thực tế" → (bỏ, hoặc "thực tế")
- "nhằm mục đích nâng cao" → "để nâng cao"
- "do bởi vì trời mưa" → "vì trời mưa"
- "một cách nhanh chóng" → "nhanh"
- "trong thời gian vừa qua" → "vừa qua"

### 23. Rào đón thái quá

**Vấn đề:** Câu bị bọc quá nhiều lớp phòng hờ.

**Trước:**
> Có thể ở một mức độ nào đó, chính sách này dường như có lẽ sẽ phần nào tác động đến kết quả.

**Sau:**
> Chính sách này có thể tác động đến kết quả.

### 24. Kết luận tích cực sáo rỗng

**Cụm chú ý:** Tin tưởng rằng... sẽ ngày càng phát triển; hứa hẹn một tương lai tươi sáng; là bước tiến quan trọng; gặt hái nhiều thành công hơn nữa.

**Vấn đề:** Đoạn kết lạc quan chung chung, không có thông tin.

**Trước:**
> Với những kết quả đạt được, tin tưởng rằng đơn vị sẽ ngày càng phát triển và gặt hái nhiều thành công hơn nữa trong tương lai.

**Sau:**
> Năm 2026, đơn vị đặt mục tiêu đưa 100% thủ tục lên dịch vụ công trực tuyến mức độ 4.

### 25. Sáo ngữ "quyền uy / chiều sâu"

**Cụm chú ý:** Về bản chất, Suy cho cùng, Điều cốt lõi là, Vấn đề mấu chốt nằm ở chỗ.

**Vấn đề:** AI dùng cụm này để ra vẻ "chạm tới cốt lõi", nhưng câu theo sau thường chỉ lặp lại một ý thường bằng giọng long trọng.

**Trước:**
> Suy cho cùng, điều cốt lõi là phải nâng cao chất lượng phục vụ người dân.

**Sau:**
> Đơn vị đặt trọng tâm vào rút ngắn thời gian trả kết quả cho người dân.

### 26. Rao trước, dẫn dắt

**Cụm chú ý:** Chúng ta hãy cùng tìm hiểu, Trước tiên hãy, Có thể thấy rằng, Không khó để nhận ra, Sau đây xin trình bày.

**Vấn đề:** AI thông báo sắp làm gì thay vì làm luôn.

**Trước:**
> Có thể thấy rằng, sau đây xin trình bày những kết quả mà đơn vị đã đạt được.

**Sau:**
> Kết quả đơn vị đạt được trong năm 2025:

### 27. Công thức cách ngôn

**Cụm chú ý:** X là chìa khóa của Y, X là linh hồn của Z, X là nền tảng của..., X là bức tranh...

**Vấn đề:** AI biến một ý thường thành câu cách ngôn nghe kêu mà không chính xác hơn.

**Trước:**
> Chuyển đổi số là chìa khóa của mọi thành công, là linh hồn của nền hành chính hiện đại.

**Sau:**
> Chuyển đổi số giúp rút ngắn thời gian xử lý hồ sơ và giảm giấy tờ.

### 28. Mở đầu giả thân mật

**Cụm chú ý:** Thật lòng mà nói, Nói thẳng ra, Nói thật, Thú thật là (dùng như câu móc giả).

**Vấn đề:** AI mở đầu bằng một câu "thật lòng" giả để tạo cảm giác gần gũi trước một ý bình thường. (Hiếm gặp trong văn bản hành chính; chủ yếu ở content, nhưng vẫn nên bỏ.)

**Trước:**
> Thật lòng mà nói, dự án này thực sự rất đáng để đầu tư.

**Sau:**
> Dự án có tỷ suất hoàn vốn dự kiến 14%/năm nên đáng cân nhắc đầu tư.

### 29. Gạch ngang dài (em dash `—`) và gạch nối dài (en dash `–`)

*(Thuộc nhóm Định dạng; bổ sung ở bản 1.1.0.)*

**Vấn đề:** Bàn phím tiếng Việt không gõ sẵn `—`/`–`, và văn bản hành chính chuẩn không dùng gạch ngang dài để chèn mệnh đề phụ. Khi văn bản có nhiều `—` (nhất là dạng ` — ` ngăn một mệnh đề giải thích, hoặc `——` do lỗi chế bản), đó là dấu vết văn bản do AI/máy tạo. Thay `—`/`–` bằng, theo thứ tự ưu tiên: dấu chấm (tách câu mới), dấu phẩy (mệnh đề chêm ngắn), dấu hai chấm (mở phần giải thích), hoặc viết lại câu.

**Không flag:**
- Gạch nối thường `-` trong Tiêu ngữ ("Độc lập - Tự do - Hạnh phúc") và từ ghép ("kinh tế - xã hội").
- En dash `–` trong khoảng số hợp lệ ("13–14", "20–25 mm", "2.650–2.689") — đây là quy ước khoảng, không phải mùi AI.

**Trước:**
> Mô hình ngôn ngữ lớn — LLM — phục vụ công tác quản lý nhà nước tại Sở. Phương pháp reflow —— dàn lại văn bản gốc — cho kết quả bảo thủ.

**Sau:**
> Mô hình ngôn ngữ lớn (LLM) phục vụ công tác quản lý nhà nước tại Sở. Phương pháp reflow dàn lại văn bản gốc, cho kết quả bảo thủ.

Trước khi trả bản cuối, quét lại `—` và `–`; còn dấu ngăn mệnh đề nghĩa là chưa xong.

---

## KHÔNG ĐƯỢC FLAG: cụm và thể thức hành chính chuẩn

Đây là phần **quan trọng nhất** để không phá văn bản. Những thứ sau **KHÔNG** phải mùi AI và **KHÔNG được sửa/bỏ**:

- **Thành phần thể thức (Nghị định 30/2020/NĐ-CP):** Quốc hiệu ("CỘNG HÒA XÃ HỘI CHỦ NGHĨA VIỆT NAM"), Tiêu ngữ ("Độc lập - Tự do - Hạnh phúc"), số và ký hiệu văn bản, địa danh và ngày tháng, tên cơ quan ban hành, trích yếu nội dung, chữ ký, chức danh, dấu.
- **Cụm mở/đóng công vụ chuẩn:** "Căn cứ...", "Xét đề nghị của...", "Theo đề nghị của...", "Thực hiện...", "Kính gửi:", "Nơi nhận:", "Trân trọng.", "Trân trọng báo cáo.", "nay ban hành/quyết định/báo cáo...".
- **Ký hiệu chức danh:** TM. (thay mặt), KT. (ký thay), TL. (thừa lệnh), TUQ. (thừa ủy quyền), Q. (quyền).
- **Văn phong Hán-Việt trang trọng đúng chuẩn:** không cào bằng thành giọng đời thường. "Ban hành", "phê duyệt", "chỉ đạo", "chủ trì", "phối hợp" là chuẩn công vụ, giữ nguyên.
- **Nội dung trong ngoặc kép, tên riêng, tiêu đề văn bản:** không sửa cụm nằm trong trích dẫn hay tên gọi chính thức, kể cả khi cụm đó trùng một "từ khóa cần chú ý".

Nói ngắn: trong chế độ Hành chính, chỉ khử **sáo rỗng và cường điệu**, tuyệt đối giữ **thể thức và giọng công vụ**.

## Dấu hiệu văn bản do người viết (giữ lại)

Khi thấy những dấu hiệu này, nghiêng về việc để nguyên, chúng cho thấy có người thật viết:

- **Chi tiết cụ thể, khó bịa:** con số chính xác, ngày tháng, tên đơn vị, số hồ sơ, địa chỉ.
- **Số liệu có nguồn:** dẫn đúng tên báo cáo, nghị quyết, quyết định.
- **Câu dài ngắn xen kẽ tự nhiên**, không đều tăm tắp.
- **Nội dung riêng của bối cảnh** mà mô hình khó đoán (tên cán bộ, sự việc cụ thể của đơn vị).

Khi phân vân, hãy tìm **chùm** dấu hiệu AI, không chỉ một dấu hiệu lẻ. Một cụm "góp phần" đơn lẻ không có nghĩa gì; nhưng "góp phần" + bộ ba + "vô cùng sâu sắc" + kết luận sáo rỗng thì là mùi AI rõ.

---

## Quy trình và Đầu ra

1. Đọc kỹ đầu vào, xác định chế độ (Hành chính mặc định / Content nếu người dùng nói rõ), nhận diện mọi mẫu ở trên.
2. Viết **bản nháp**: đọc lên có tự nhiên không, câu dài ngắn hợp lý chưa, ưu tiên chi tiết cụ thể và câu đơn giản, giữ đúng văn phong (công vụ nếu là hành chính).
3. Tự hỏi: **"Chỗ nào còn lộ mùi AI?"** Trả lời ngắn gọn các dấu hiệu còn sót.
4. Sửa thành **bản cuối** xử lý những chỗ đó. Với chế độ Hành chính, rà lại: đã giữ đủ thể thức và cụm hành chính bắt buộc chưa; không thêm cá tính/ngôi thứ nhất.

Giao: bản nháp, các gạch đầu dòng "còn mùi AI", bản cuối, và (tùy chọn) tóm tắt ngắn các thay đổi.

---

## Ví dụ đầy đủ (văn bản hành chính)

**Trước (mùi AI):**
> Có thể khẳng định rằng, trong bối cảnh hiện nay, việc triển khai thực hiện Kế hoạch chuyển đổi số của đơn vị đã và đang góp phần vô cùng quan trọng, tạo nên những chuyển biến sâu sắc và toàn diện. Không thể phủ nhận rằng, đây chính là chìa khóa của mọi thành công, đánh dấu một bước ngoặt mang tính lịch sử. Đơn vị đã hết sức chú trọng đẩy mạnh, tăng cường mạnh mẽ công tác tổ chức thực hiện, qua đó khẳng định vị thế của mình. Bên cạnh những kết quả đạt được, vẫn còn một số khó khăn, hạn chế nhất định. Tin tưởng rằng, trong thời gian tới, đơn vị sẽ ngày càng phát triển và gặt hái nhiều thành công hơn nữa. 🚀

**Bản nháp:**
> Năm 2025, đơn vị triển khai Kế hoạch chuyển đổi số và đạt một số kết quả. Đơn vị đã đưa nhiều thủ tục lên trực tuyến. Vẫn còn khó khăn về nhân lực và hạ tầng. Năm 2026, đơn vị đặt mục tiêu hoàn thiện các dịch vụ công trực tuyến.

**Chỗ nào còn lộ mùi AI?**
- "đạt một số kết quả", "nhiều thủ tục" còn chung chung, thiếu con số.
- Câu về khó khăn vẫn còn rập khuôn, chưa nêu cụ thể.
- Chưa nêu mốc thời gian, chỉ tiêu định lượng.

**Bản cuối:**
> Năm 2025, đơn vị đưa 18/25 thủ tục hành chính lên dịch vụ công trực tuyến mức độ 4. Thời gian xử lý hồ sơ trung bình giảm từ 4 ngày xuống 1,5 ngày; tỷ lệ hồ sơ trễ hạn còn 3%.
>
> Hai khó khăn còn tồn tại: thiếu 3 biên chế công nghệ thông tin và phần mềm một cửa chưa liên thông với hệ thống của Sở.
>
> Năm 2026, đơn vị đặt mục tiêu đưa 7 thủ tục còn lại lên trực tuyến mức độ 4 và hoàn thành liên thông phần mềm trong quý II.

**Các thay đổi:** Giữ chủ đề và cấu trúc báo cáo (kết quả - khó khăn - phương hướng), nhưng bỏ khẳng định thổi phồng ("bước ngoặt lịch sử", "chìa khóa của mọi thành công"), cụm cường điệu rỗng ("vô cùng, sâu sắc, toàn diện, mạnh mẽ"), cặp đồng nghĩa thừa ("triển khai thực hiện", "đẩy mạnh, tăng cường"), quy kết mơ hồ ("không thể phủ nhận"), kết luận sáo rỗng, và emoji. Thay bằng số liệu cụ thể, giữ nguyên giọng công vụ trang trọng.

---

## Tham chiếu

- Fork tiếng Việt của [blader/humanizer](https://github.com/blader/humanizer) (MIT), dựa trên [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing).
- Văn phong hành chính và thể thức văn bản theo **Nghị định 30/2020/NĐ-CP** về công tác văn thư.

Ý chính: mô hình ngôn ngữ đoán chữ tiếp theo theo xác suất, nên kết quả nghiêng về cách diễn đạt "an toàn, kêu, chung chung nhất". Khử mùi AI là thay cái chung chung đó bằng sự việc và con số cụ thể, mà với văn bản hành chính thì vẫn phải giữ đúng thể thức và giọng công vụ.
