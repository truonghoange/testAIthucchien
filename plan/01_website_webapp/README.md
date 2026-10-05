# Website, web app và công cụ AI

[Mục lục plan](../README.md) · [Điều hành chung](../_chung/README.md)

**Mục tiêu:** người dùng hoàn thành một việc cụ thể trong vài thao tác. Website du lịch cần khám phá/chọn hành trình; ứng dụng AI cần một luồng nhập → xử lý → kết quả kiểm được. Bản tối thiểu chứa đủ mục đề yêu cầu, link hoạt động và nội dung thật đã duyệt. Tính năng đặt chỗ/thanh toán chỉ làm nếu đề yêu cầu; không dựng nút trông như chạy mà không có xử lý.

## Đường đi ưu tiên

- Đầu vào: Nguồn nội dung, ảnh và yêu cầu luồng người dùng.
- Bản đủ: Link mở được và thực hiện trọn luồng chính.
- Phụ thuộc quan trọng: Chốt schema → luồng hoạt động → deploy → kiểm link.
- Điểm nổi bật nên chọn: hành trình gợi ý theo nhu cầu, bộ lọc hoặc cách giải thích kết quả có nguồn; chọn một.

## File cần đọc

| File | Công dụng |
| --- | --- |
| [kien_truc.md](kien_truc.md) | Chốt module, cấu trúc file và schema trước khi chia việc |
| [pipeline.md](pipeline.md) | Chạy các bước và bàn giao đúng thứ tự |
| [ke_hoach.md](ke_hoach.md) | Phân người, thời gian và budget |
| [prompts.md](prompts.md) | Giao nội dung, code, media và kiểm tra |
| [checklist.md](checklist.md) | Chốt bản nộp và phương án dự phòng |

Trước hết dùng [prompt P0/P1](../_chung/02_prompts_dieu_hanh.md); khi giao worker dùng P2 rồi bổ sung prompt theo dạng đề. Đây là kiến trúc và prompt đề xuất để diễn tập, cần thay trường trong ngoặc vuông bằng đề thật.
