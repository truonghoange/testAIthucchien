# Kế hoạch làm việc — Sáng tác bài hát

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

## Từ T+0 đến T+15

Thành chốt đề, người dùng và yêu cầu bắt buộc; Hoàng kiểm đầu vào/nội dung/style; Đức kiểm repo/provider/hook và khóa task/schema. Mọi người cùng duyệt một spec. Xem [harness](../_chung/01_harness.md) và [P0/P1](../_chung/02_prompts_dieu_hanh.md).

## Phân việc theo mốc

| Thời gian | Thành | Hoàng | Đức |
| --- | --- | --- | --- |
| 15–30 | Chốt thông điệp/từ khóa, duyệt chorus | Viết lời và style | Khung gói nộp, bìa nếu cần |
| 30–50 | Nghe bản đầu | Sinh/chọn hai bản theo quota | Kiểm audio, chuẩn bị export |
| 50–60 | Chọn bản có thể nộp | Bàn giao audio và lời khớp | Gói bài hát đủ |
| 60–100 | Nghe lại từ khóa/nội dung | Chỉ sửa lời và sinh lại nếu thật cần | Export; lyric video nếu bắt buộc |

## Từ T+100 đến hết giờ làm

Chỉ sửa lỗi chặn nộp, đối chiếu checklist, xuất/deploy bản cuối, chốt README và prompt/nguồn, gửi log thật. Trong 10 phút sau hết giờ làm, chỉ thao tác nộp theo hướng dẫn đề. Lịch 120 phút là giả định từ chiến lược đã có, phải điều chỉnh nếu ca thi công bố thời lượng khác.

## Trần ngân sách đề xuất

| Hạng mục | Trần USD |
| --- | ---: |
| LLM/code | 6 |
| Ảnh | 4 |
| Video | 0 |
| TTS/tra cứu/khác | 2 |
| Dự phòng | 38 |
| **Tổng** | **50** |

Trần để điều phối, không phải số cần tiêu. Dùng ít hơn khi đã đạt. Đức kiểm chi tiêu ở T+30/60/90 và trước batch lớn; Thành quyết định dùng dự phòng cho yêu cầu bắt buộc. Suno theo quota tài khoản BTC, không mặc định trừ vào Gateway. Căn cứ và giả định xem [quy định/nguồn](../_chung/04_quy_dinh_nguon.md).

## Đánh đổi khi chậm

- T+35 chưa có khung: cắt thành phần tùy chọn.
- T+60 chưa đủ đề: dừng trang trí, dồn vào yêu cầu còn thiếu.
- T+100 khóa tính năng/nội dung; sửa có giới hạn và kiểm lại đúng chỗ đổi.
- Không cắt đầu ra bắt buộc chỉ để khớp lịch gợi ý.
