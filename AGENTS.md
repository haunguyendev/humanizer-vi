# AGENTS.md

Hướng dẫn cho các AI coding agent (Claude Code, Codex, Warp...) khi làm việc trong repo này.

## Repo này là gì

`humanizer-vi` là một agent skill thuần Markdown, **fork tiếng Việt** của [`blader/humanizer`](https://github.com/blader/humanizer) (MIT). Bản này viết lại toàn bộ để khử "mùi AI" trong tiếng Việt, **ưu tiên văn bản hành chính** theo Nghị định 30/2020/NĐ-CP.

Artifact chạy thật là `SKILL.md`: agent đọc YAML frontmatter (metadata + allowed tools) rồi đến phần prompt biên tập. Không có bước build, không có code để chạy. Ngôn ngữ của skill (hướng dẫn + ví dụ) là tiếng Việt.

## File chính

- `SKILL.md` — bản thân skill. YAML frontmatter (`name`, `version`, `description`, `compatibility`, `allowed-tools`) rồi đến danh sách pattern đánh số, có ví dụ trước/sau bằng tiếng Việt. **Đây là nguồn chân lý (source of truth).**
- `README.md` — cho người đọc: cài đặt, cách dùng, bảng pattern, lịch sử phiên bản, ghi công repo gốc.
- `.claude-plugin/plugin.json` — manifest plugin Claude Code.
- `.claude-plugin/marketplace.json` — marketplace một-repo để `/plugin marketplace add <user>/humanizer-vi` chạy được.

## Hợp đồng bảo trì

`SKILL.md` và `README.md` phải luôn đồng bộ. Khi thay đổi hành vi hoặc nội dung:

- **Pattern:** skill hiện định nghĩa **29 pattern đánh số** (chia 5 nhóm A–E; pattern 29 về gạch ngang dài bổ sung ở bản 1.1.0). Nếu thêm/bớt/đánh số lại pattern nào, cập nhật đồng thời: bảng pattern trong README, số "N pattern" ở heading, và mọi tham chiếu chéo trong cùng một lần sửa. Giữ số ổn định trừ khi cố ý đánh số lại.
- **Section riêng của tiếng Việt:** hai section "KHÔNG được flag — cụm/thể thức hành chính chuẩn (NĐ30)" và "Văn phong hành chính chuẩn" là đặc trưng của bản này (thay cho `PERSONALITY AND SOUL` của bản gốc). Không xóa; đây là lớp bảo vệ để không phá văn bản hành chính.
- **Phiên bản:** frontmatter `SKILL.md` có `version:`, `README.md` có mục "Lịch sử phiên bản", `.claude-plugin/plugin.json` có `version`. Bump cùng lúc. (`marketplace.json` cố ý không có version để `plugin.json` là nguồn chuẩn.)
- **Ghi công & giấy phép:** GIỮ copyright gốc trong `LICENSE` (bắt buộc theo MIT) và giữ đoạn ghi công `blader/humanizer` trong README. Chỉ được thêm, không được xóa.
- **Fix không hiển nhiên:** nếu sửa prompt để xử lý một lỗi khó (một kiểu sửa sai lặp lại, lệch tông bất ngờ), thêm ghi chú ngắn vào mục lịch sử phiên bản của README giải thích đã sửa gì và vì sao.

## Sửa SKILL.md

- Giữ YAML frontmatter hợp lệ (định dạng và thụt lề).
- Phần prompt bên dưới frontmatter là sản phẩm. Sửa nó như một tài liệu hướng dẫn cẩn thận, không phải code.
- Ví dụ trước/sau phải bằng tiếng Việt, ưu tiên ngữ cảnh cơ quan nhà nước / văn bản hành chính.
