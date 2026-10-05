# Sáng tác bài hát

[Mục lục plan](../README.md) · [Điều hành chung](../_chung/README.md)

**Mục tiêu:** lời rõ, đúng chủ đề, điệp khúc dễ nhớ và đáp ứng yêu cầu âm nhạc của đề. Suno là luồng tài khoản riêng theo hướng dẫn BTC, không tự xem nó như endpoint của Gateway.

## Đường đi ưu tiên

- Đầu vào: Chủ đề, từ khóa bắt buộc, thể loại và thời lượng.
- Bản đủ: Audio hát rõ, đúng chủ đề/từ khóa và lời khớp.
- Phụ thuộc quan trọng: Lời duyệt → tạo bản audio → nghe/chọn → export.
- Điểm nổi bật nên chọn: điệp khúc có một hình ảnh hoặc câu người nghe nhớ, thay vì dồn khẩu hiệu.

## File cần đọc

| File | Công dụng |
| --- | --- |
| [kien_truc.md](kien_truc.md) | Chốt module, cấu trúc file và schema trước khi chia việc |
| [pipeline.md](pipeline.md) | Chạy các bước và bàn giao đúng thứ tự |
| [ke_hoach.md](ke_hoach.md) | Phân người, thời gian và budget |
| [prompts.md](prompts.md) | Giao nội dung, code, media và kiểm tra |
| [checklist.md](checklist.md) | Chốt bản nộp và phương án dự phòng |

Trước hết dùng [prompt P0/P1](../_chung/02_prompts_dieu_hanh.md); khi giao worker dùng P2 rồi bổ sung prompt theo dạng đề. Đây là kiến trúc và prompt đề xuất để diễn tập, cần thay trường trong ngoặc vuông bằng đề thật.
