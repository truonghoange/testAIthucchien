# Kế hoạch làm việc — Game giáo dục

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

## Từ T+0 đến T+15

Thành chốt đề, người dùng và yêu cầu bắt buộc; Hoàng kiểm đầu vào/nội dung/style; Đức kiểm repo/provider/hook và khóa task/schema. Mọi người cùng duyệt một spec. Xem [harness](../_chung/01_harness.md) và [P0/P1](../_chung/02_prompts_dieu_hanh.md).

## Phân việc theo mốc

| Thời gian | Thành | Hoàng | Đức |
| --- | --- | --- | --- |
| 15–30 | Duyệt luật và câu hỏi | Bàn giao JSON, style sprite | Khóa schema, engine và UI thô |
| 30–50 | Thử hiểu bài học | Tạo bộ asset nhỏ | Một màn chơi trọn vẹn, deploy |
| 50–60 | Đối chiếu đề | Gắn tài nguyên cuối | Bản đủ, kể cả phần giải thích |
| 60–100 | Chơi thử/kiểm kiến thức | Sửa câu hỏi và hình lỗi | Sửa điều khiển, feedback; thử mobile |

## Từ T+100 đến hết giờ làm

Chỉ sửa lỗi chặn nộp, đối chiếu checklist, xuất/deploy bản cuối, chốt README và prompt/nguồn, gửi log thật. Trong 10 phút sau hết giờ làm, chỉ thao tác nộp theo hướng dẫn đề. Lịch 120 phút là giả định từ chiến lược đã có, phải điều chỉnh nếu ca thi công bố thời lượng khác.

## Trần ngân sách đề xuất

| Hạng mục | Trần USD |
| --- | ---: |
| LLM/code | 14 |
| Ảnh | 8 |
| Video | 0 |
| TTS/tra cứu/khác | 3 |
| Dự phòng | 25 |
| **Tổng** | **50** |

Trần để điều phối, không phải số cần tiêu. Dùng ít hơn khi đã đạt. Đức kiểm chi tiêu ở T+30/60/90 và trước batch lớn; Thành quyết định dùng dự phòng cho yêu cầu bắt buộc. Suno theo quota tài khoản BTC, không mặc định trừ vào Gateway. Căn cứ và giả định xem [quy định/nguồn](../_chung/04_quy_dinh_nguon.md).

## Đánh đổi khi chậm

- T+35 chưa có khung: cắt thành phần tùy chọn.
- T+60 chưa đủ đề: dừng trang trí, dồn vào yêu cầu còn thiếu.
- T+100 khóa tính năng/nội dung; sửa có giới hạn và kiểm lại đúng chỗ đổi.
- Không cắt đầu ra bắt buộc chỉ để khớp lịch gợi ý.
