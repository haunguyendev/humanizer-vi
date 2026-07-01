# Humanizer-VI

Một agent skill thuần Markdown giúp khử "mùi AI" trong văn bản tiếng Việt, ưu tiên **văn bản hành chính** theo Nghị định 30/2020/NĐ-CP. Vì là Markdown thuần, skill chạy được trong mọi harness hỗ trợ dạng skill (Claude Code, Codex, OpenCode...).

Mục tiêu: bỏ dấu hiệu văn bản do AI tạo (thổi phồng, sáo rỗng, cường điệu rỗng...) nhưng **giữ đúng văn phong công vụ trang trọng** — không biến công văn/tờ trình/báo cáo thành giọng đời thường.

## Nguồn gốc

Đây là **fork tiếng Việt** của [blader/humanizer](https://github.com/blader/humanizer) (giấy phép MIT), vốn dựa trên trang [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing). Bản này viết lại toàn bộ bộ pattern cho tiếng Việt và định hướng văn bản hành chính. Xin cảm ơn tác giả gốc.

## Cài đặt

### Skills CLI

```bash
npx skills add haunguyendev/humanizer-vi
```

Cập nhật bản đã cài:

```bash
npx skills update humanizer-vi
```

Cài vào mọi harness được hỗ trợ:

```bash
npx skills add haunguyendev/humanizer-vi --agent '*'
```

### Plugin Claude Code

```
/plugin marketplace add haunguyendev/humanizer-vi
/plugin install humanizer-vi@humanizer-vi
```

Sau đó gọi skill bằng `/humanizer-vi:humanizer-vi`.

### Thủ công

Vì artifact chạy thật là `SKILL.md`, mọi harness đều dùng trực tiếp được. Sao chép vào thư mục skill của harness:

```bash
git clone https://github.com/haunguyendev/humanizer-vi.git /path/to/your/skills/humanizer-vi
```

Hoặc chỉ copy `SKILL.md`:

```bash
mkdir -p /path/to/your/skills/humanizer-vi
cp SKILL.md /path/to/your/skills/humanizer-vi/
```

## Cách dùng

Đưa văn bản cần khử mùi AI cho skill. Một số ví dụ prompt:

- "Khử mùi AI đoạn báo cáo này (văn bản hành chính)."
- "Rà lại tờ trình sau, bỏ chữ sáo nhưng giữ nguyên thể thức và giọng công vụ."
- "Đây là bài giới thiệu (content thường), cho có giọng điệu tự nhiên."
- "Khử mùi AI đoạn này. Đây là mẫu văn phong của tôi để bám theo: [mẫu]."

Skill có **hai chế độ**:

- **Hành chính (mặc định):** bỏ mùi AI, giữ văn phong công vụ trang trọng, không thêm cá tính; tuyệt đối giữ thể thức và cụm hành chính bắt buộc (Căn cứ..., Kính gửi:, Nơi nhận:, Trân trọng...).
- **Content thường (tùy chọn):** chỉ bật khi bạn nói rõ; được phép thêm giọng điệu, cá tính, ngôi thứ nhất — như bản humanizer gốc.

Nếu không chắc loại văn bản, skill mặc định chế độ Hành chính và hỏi lại.

## 32 pattern nhận diện

Chia 5 nhóm. Xem ví dụ trước/sau chi tiết trong `SKILL.md`.

### Nhóm A — Nội dung & tu từ
| STT | Pattern | Mô tả ngắn |
|-----|---------|------------|
| 1 | Thổi phồng ý nghĩa, tầm vóc, di sản | Gán ý nghĩa lớn lao cho sự việc bình thường ("bước ngoặt lịch sử") |
| 2 | Mệnh đề đuôi hời hợt | Dán "..., góp phần...", "..., qua đó khẳng định..." để ra vẻ chiều sâu |
| 3 | Ngôn ngữ hoa mỹ, quảng cáo | "trù phú, thơ mộng, phong phú đa dạng, giàu bản sắc" |
| 4 | Quy kết mơ hồ, từ né tránh | "Nhiều ý kiến cho rằng", "Không thể phủ nhận" không nguồn |
| 5 | Mục "khó khăn & phương hướng" công thức | Khối rập khuôn rỗng (giữ mục bắt buộc, thay nội dung cụ thể) |
| 31 | Mở bài định nghĩa kiểu bách khoa | "X là một... nằm ở... đóng vai trò quan trọng" (bổ sung v1.2.0) |

### Nhóm B — Từ vựng & ngữ pháp
| STT | Pattern | Mô tả ngắn |
|-----|---------|------------|
| 6 | Từ vựng "mùi AI" tiếng Việt | "vô cùng, sâu sắc, toàn diện, mạnh mẽ; đẩy mạnh, tăng cường, nâng cao" |
| 7 | Cặp đồng nghĩa thừa (song tiết hóa) | "triển khai thực hiện, tổ chức thực hiện, đảm bảo duy trì" |
| 8 | Danh từ hóa thừa "việc/công tác + động từ" | "việc triển khai công tác tổ chức" → động từ trực tiếp |
| 9 | Đối xứng phủ định | Lạm dụng "Không chỉ... mà còn..." |
| 10 | Lạm dụng quy tắc bộ ba | Ép thành cụm ba "nhanh chóng, kịp thời, hiệu quả" |
| 11 | Xoay vòng từ đồng nghĩa | Đổi tên gọi cùng chủ thể liên tục |
| 12 | Câu dài lê thê nối bằng dấu phẩy | Một câu nhiều mệnh đề → tách câu |
| 13 | Bị động, khuyết chủ ngữ lạm dụng | "được... một cách..." (giữ bị động hành chính hợp lệ) |
| 30 | Cú pháp dịch máy Anh→Việt | "và/hoặc", "đối với việc", chuỗi "của" liên hoàn (bổ sung v1.2.0) |
| 32 | Nhịp câu lặp đều, song song máy móc | ≥3 câu cùng khuôn chủ-vị liên tiếp (bổ sung v1.2.0) |

### Nhóm C — Định dạng
| STT | Pattern | Mô tả ngắn |
|-----|---------|------------|
| 14 | Lạm dụng in đậm | Bôi đậm cụm máy móc |
| 15 | Danh sách "đầu mục in đậm + hai chấm" | `- **Mục:** nội dung` hàng loạt |
| 16 | Emoji | Cắt sạch (VBHC không có emoji) |
| 17 | Lạm dụng VIẾT HOA & viết hoa sai chuẩn | Theo quy tắc viết hoa NĐ30 (thay "title case" tiếng Anh) |
| 18 | Đầu mục rời rạc | Heading rồi câu lặp lại heading |
| 29 | Gạch ngang dài (em dash `—`/`–`) | Thay `—` bằng dấu chấm/phẩy/hai chấm; giữ gạch nối `-` trong Tiêu ngữ và khoảng số (bổ sung v1.1.0) |

### Nhóm D — Dấu vết chatbot
| STT | Pattern | Mô tả ngắn |
|-----|---------|------------|
| 19 | Dấu vết hội thoại | "Hy vọng thông tin này hữu ích", "Dưới đây là..." |
| 20 | Miễn trừ kiến thức, bịa lấp khoảng trống | "Do thông tin còn hạn chế..." rồi bịa nội dung |
| 21 | Giọng nịnh, xu nịnh | "Câu hỏi rất hay!", "Bạn hoàn toàn đúng" |

### Nhóm E — Rỗng & vòng vo
| STT | Pattern | Mô tả ngắn |
|-----|---------|------------|
| 22 | Cụm rỗng, vòng vo | "trong bối cảnh hiện nay", "có thể nói rằng" |
| 23 | Rào đón thái quá | "có thể phần nào, dường như, ở một mức độ nào đó" |
| 24 | Kết luận tích cực sáo rỗng | "hứa hẹn tương lai tươi sáng", "ngày càng phát triển" |
| 25 | Sáo ngữ "quyền uy / chiều sâu" | "Về bản chất", "Suy cho cùng", "Điều cốt lõi là" |
| 26 | Rao trước, dẫn dắt | "Chúng ta hãy cùng tìm hiểu", "Có thể thấy rằng" |
| 27 | Công thức cách ngôn | "X là chìa khóa của Y", "X là linh hồn của Z" |
| 28 | Mở đầu giả thân mật | "Thật lòng mà nói", "Nói thẳng ra" |

**Đã cắt so với bản gốc (3 pattern chỉ đặc trưng tiếng Anh):** cặp từ gạch nối (`high-quality`), viết hoa kiểu "title case" (không có trong tiếng Việt → thay bằng pattern 17), dấu ngoặc kép cong (hạ thành ghi chú nhỏ). *Từ v1.1.0, em dash `—` được đưa lại thành pattern 29 vì thực tế đây cũng là dấu vết AI phổ biến trong tiếng Việt.*

## Không được flag (bảo vệ văn bản hành chính)

Trong chế độ Hành chính, skill **không** sửa các thành phần thể thức và cụm công vụ chuẩn theo NĐ30: Quốc hiệu, Tiêu ngữ, số/ký hiệu, "Căn cứ...", "Kính gửi:", "Nơi nhận:", "Trân trọng.", ký hiệu chức danh (TM., KT., TL., TUQ., Q.), và văn phong Hán-Việt trang trọng đúng chuẩn. Chỉ khử sáo rỗng và cường điệu.

## Lịch sử phiên bản

- **1.2.1** — Trau an toàn sau vòng kiểm định (cả 3 reviewer PASS): pattern 32 thêm ngoại lệ giữ khối "Căn cứ"/"Nơi nhận"; bảo vệ rõ khối chữ ký (chức vụ và họ tên người ký).
- **1.2.0** — Cập nhật lớn sau vòng review nội bộ (3 reviewer). Thêm **HAI NGUYÊN TẮC BẤT BIẾN** ở đầu: (1) KHÔNG bịa số liệu — sửa các ví dụ để bản "Sau" không chèn số/nguồn không có trong bản gốc; (2) KHÔNG sửa thể thức NĐ30 + quy tắc chống over-edit "≥2 dấu hiệu mới sửa". Thêm 3 pattern: 30 (cú pháp dịch máy Anh→Việt), 31 (mở bài kiểu bách khoa), 32 (nhịp câu lặp đều) → tổng 32. Mở rộng section "KHÔNG được flag" theo Điều 8/13 + Phụ lục I/II NĐ30 (độ mật/độ khẩn, tên loại văn bản in hoa, số/ký hiệu, địa danh-ngày tháng, khối Nơi nhận/Căn cứ, phụ lục, chữ ký số, thuật ngữ bản sao). Thêm ngoại lệ register khoa học (danh từ hóa cú pháp), checklist thể thức 11 mục, và xử lý tracked changes.
- **1.1.0** — Thêm pattern 29 (gạch ngang dài em dash `—`/`–`) vào nhóm Định dạng. Lý do: kiểm thử trên văn bản hành chính thực tế cho thấy em dash là dấu vết AI phổ biến trong tiếng Việt (bàn phím Việt không gõ sẵn, văn bản NĐ30 không dùng). Có ngoại lệ: giữ gạch nối `-` trong Tiêu ngữ và khoảng số. Tổng: 29 pattern.
- **1.0.0** — Bản Việt hóa đầu tiên, ưu tiên văn bản hành chính theo NĐ 30/2020. Viết lại 28 pattern (5 nhóm), cắt 4 pattern chỉ-tiếng-Anh, thêm các pattern đặc trưng tiếng Việt (từ vựng mùi AI VN, cặp đồng nghĩa thừa, danh từ hóa thừa, viết hoa sai chuẩn...). Thêm hai section riêng: "KHÔNG được flag — thể thức NĐ30" và "Văn phong hành chính chuẩn" (thay cho "PERSONALITY AND SOUL" của bản gốc). Hai chế độ: Hành chính (mặc định) và Content thường.

## Giấy phép

MIT. Giữ nguyên bản quyền gốc của tác giả humanizer (blader / Siqi Chen); phần Việt hóa bổ sung bản quyền của người fork. Xem `LICENSE`.
