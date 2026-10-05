# Plan làm bài thi — MedmeetAI

Bộ plan cho MedmeetAI, được tách từ tài liệu chiến lược đã bổ sung ngày 05/10/2026. Mỗi dạng đề có bộ file riêng; phần điều hành dùng chung đặt trong `_chung/`.

## Chọn loại đề

| Thư mục | Dạng đề | Bản đủ tối thiểu |
| --- | --- | --- |
| [01_website_webapp](01_website_webapp/README.md) | Website, web app và công cụ AI | Link mở được và thực hiện trọn luồng chính |
| [02_game_giao_duc](02_game_giao_duc/README.md) | Game giáo dục | Một lượt chơi hoàn chỉnh có giải thích và chơi lại |
| [03_bao_cao_du_lieu](03_bao_cao_du_lieu/README.md) | Báo cáo dữ liệu và tài chính | PDF/DOCX với số, biểu đồ và nhận định truy nguyên được |
| [04_infographic](04_infographic/README.md) | Infographic pháp luật và chính sách | PNG/PDF đúng khổ, nội dung và nguồn kiểm được |
| [05_truyen_tranh](05_truyen_tranh/README.md) | Truyện tranh giáo dục và cảnh báo | Truyện đủ khung/trang, thoại rõ và nhân vật nhất quán |
| [06_video](06_video/README.md) | Video: bản tin, quảng cáo và phim ngắn | Video có đủ lớp hình/giọng/phụ đề theo đề, đúng thời lượng |
| [07_to_gap](07_to_gap/README.md) | Tờ gấp truyền thông và hướng dẫn | PDF hai mặt đúng khổ và đúng thứ tự sau khi gấp |
| [08_podcast](08_podcast/README.md) | Podcast tư vấn, giáo dục và kể chuyện | MP3/WAV nghe trọn vẹn, rõ lời và đúng thời lượng |
| [09_bai_hat](09_bai_hat/README.md) | Sáng tác bài hát | Audio hát rõ, đúng chủ đề/từ khóa và lời khớp |
| [10_chien_dich_truyen_thong](10_chien_dich_truyen_thong/README.md) | Chiến dịch đa định dạng và poster | Bộ sản phẩm đủ ma trận, cùng thông điệp/nhận diện |

## Mỗi thư mục có gì?

| File | Nội dung |
| --- | --- |
| `README.md` | Mục tiêu, đầu ra, đường đi ưu tiên và cách đọc |
| `prompts.md` | Prompt nội dung, triển khai, media và QA theo dạng đề |
| `pipeline.md` | Sơ đồ, các bước, đầu vào/đầu ra và điểm bàn giao |
| `kien_truc.md` | Thành phần chương trình, cấu trúc file, schema và phụ thuộc |
| `ke_hoach.md` | Lịch làm việc, phân vai, budget và điểm dừng |
| `checklist.md` | Điều kiện xong, QA và phương án dự phòng |

## Cách dùng

1. Đọc [quy định và nguồn](_chung/04_quy_dinh_nguon.md), xác định điều kiện thực tế của ca thi.
2. Dùng [P0–P4](_chung/02_prompts_dieu_hanh.md) để phân tích đề, chốt hướng và chia task.
3. Chọn thư mục theo **đầu ra bắt buộc**, đọc `kien_truc.md` rồi `pipeline.md`.
4. Giao người theo `ke_hoach.md`, dùng các prompt trong `prompts.md` theo bước.
5. Kiểm `checklist.md` và [checklist nộp chung](_chung/05_qa_nop_bai.md) trước khi nộp.

Đề kết hợp nhiều đầu ra: đọc [cách ghép plan](_chung/06_ghep_plan.md), dùng chung spec, nguồn, schema và ngân sách.

## Cấu trúc đưa vào repo

Thư mục tài liệu này đặt ở `chung-khao/plan/` nếu thông báo BTC cho phép dùng tài liệu chuẩn bị trước. Các đường dẫn source trong `kien_truc.md` là cấu trúc **chương trình dự kiến dưới `chung-khao/`**, không phải mã chạy sẵn nằm trong thư mục plan.

Các prompt là khung diễn tập có trường thay thế. Không mặc định được sao chép vào ca thi; quyền dùng tài liệu, API và công cụ theo thông báo riêng của BTC. Mốc 120 phút lấy từ bản chiến lược đội cung cấp; chi tiết đã/chưa xác minh được ghi ở phần nguồn.

## Phần dùng chung

- [Harness và phân vai](_chung/01_harness.md)
- [Prompt điều hành](_chung/02_prompts_dieu_hanh.md)
- [Lịch và ngân sách](_chung/03_lich_ngan_sach.md)
- [Quy định và nguồn](_chung/04_quy_dinh_nguon.md)
- [QA và nộp bài](_chung/05_qa_nop_bai.md)
- [Ghép nhiều plan](_chung/06_ghep_plan.md)

Test push and pull request to see if the repo is private and if I can access it.
