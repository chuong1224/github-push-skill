## name: github-push
version: 1.0.0
description: Kích hoạt khi user muốn tạo repo mới trên GitHub, push file/code lên GitHub, setup README đẹp, thêm badge, làm README song ngữ Anh-Việt, thêm Version History. Trigger phrases: “push to github”, “tạo repo và push”, “github push”, “push lên github”, “create github repo”, “setup github”, “push skill to github”, “tạo repo github”.

## Mục đích

Giúp user nhanh chóng tạo repo GitHub mới + push code/files + setup README chuyên nghiệp (có badge, song ngữ Anh-Việt, Version History) chỉ bằng vài câu lệnh tự nhiên. Kết quả phải sạch sẽ, đẹp, sẵn sàng sử dụng.

## Workflow chính

### Bước 1 — Xác định yêu cầu
Hỏi hoặc phân tích từ user:
- Tên repo mong muốn (nếu chưa có)
- Mô tả ngắn gọn của project
- Loại project: Grok Skill / Web App / Library / Script / Khác
- Có muốn README song ngữ Anh-Việt không? (mặc định: có)
- Public hay Private? (mặc định: Public)
- Có cần LICENSE không? (mặc định: MIT)

### Bước 2 — Tạo repository
Sử dụng tool `github___create_repository`:
- name: tên repo đã chuẩn hóa (kebab-case)
- description: mô tả ngắn
- private: true/false
- autoInit: true

### Bước 3 — Chuẩn bị nội dung
Tạo các file cần thiết:
- `README.md` (song ngữ Anh-Việt + badge + Version History)
- `LICENSE` (MIT nếu user đồng ý)
- `.gitignore` (phù hợp với loại project)
- Các file code chính (nếu user cung cấp)

### Bước 4 — Tạo README song ngữ đẹp
README phải có cấu trúc:
1. Tiêu đề + dòng badge đẹp (Version, License, Last Commit, Stars, Grok Skill nếu là skill)
2. Mô tả ngắn bằng tiếng Anh
3. `---`
4. `## English` → đầy đủ các section
5. `---`
6. `## Tiếng Việt` → bản dịch tương ứng
7. `## Version History` (bảng)
8. Footer có link LICENSE và repo

Badge phổ biến nên có:
- Version
- License (github/license)
- Last Commit
- Stars (social)
- Grok Skill (nếu là skill)

### Bước 5 — Push files
Sử dụng `github___push_files` hoặc `github___create_or_update_file` để push tất cả file cùng lúc với commit message rõ ràng.

### Bước 6 — Hoàn tất
- Trả link repo
- Hướng dẫn user clone hoặc tiếp tục phát triển
- Hỏi có muốn thêm gì nữa không (release, topics, etc.)

## Gotchas

|#|Vấn đề hay gặp                              |Cách xử lý                                                                 |
|---|---------------------------------------------|----------------------------------------------------------------------------|
|1 |User chưa connect GitHub                    |Nhắc user connect GitHub account trước khi dùng skill                      |
|2 |Tên repo bị trùng hoặc không hợp lệ         |Đề xuất tên thay thế (kebab-case, ngắn gọn)                                |
|3 |README quá dài hoặc lộn xộn                 |Giữ cấu trúc rõ ràng, English trước, Vietnamese sau, dùng heading hợp lý   |
|4 |Quên thêm badge Last Commit / License       |Luôn thêm 4-5 badge phổ biến ở header                                      |
|5 |User muốn custom nhiều badge                |Hỏi thêm badge nào (ví dụ: Build Status, Coverage, v.v.) rồi thêm          |
|6 |Project là Grok Skill                       |Tự động thêm badge "Grok Skill" + mention SKILL.md                         |
|7 |Muốn Version History chi tiết               |Tạo bảng với cột: Version | Date | Changes                                   |

## Ví dụ thực tế

**User:** "Tạo repo github cho skill mới tên là x-post-reply và push lên"

**Kết quả skill:**
1. Tạo repo `x-post-reply`
2. Push `SKILL.md` + `README.md` song ngữ + `LICENSE`
3. Thêm đầy đủ badge + Version History
4. Trả link: https://github.com/chuong1224/x-post-reply

**User:** "push cái này lên github với readme song ngữ"

**Kết quả:** Tạo repo mới hoặc push vào repo hiện có (nếu user chỉ định), setup README bilingual đẹp.

---

*Skill version: 1.0.0* | Tạo bởi N0v4Ph4n | Dành cho Grok SuperGrok users