# Game giáo dục

[Mục lục plan](../README.md) · [Điều hành chung](../_chung/README.md)

**Mục tiêu:** chơi xong người dùng nhớ và áp dụng một kiến thức. Chọn một cơ chế chính: phân loại, kéo thả, lựa chọn tình huống hoặc nối cặp. Bản tối thiểu có bắt đầu → chơi → phản hồi giải thích → kết quả → chơi lại; ưu tiên một màn hoàn chỉnh trước T+50.

## Đường đi ưu tiên

- Đầu vào: Kiến thức đã duyệt, luật điểm và cơ chế chơi.
- Bản đủ: Một lượt chơi hoàn chỉnh có giải thích và chơi lại.
- Phụ thuộc quan trọng: Câu hỏi/luật → engine → một màn hoàn chỉnh → deploy.
- Điểm nổi bật nên chọn: giải thích sau lựa chọn và tổng kết kiến thức, thêm âm/hạt phản hồi nhẹ.

## File cần đọc

| File | Công dụng |
| --- | --- |
| [kien_truc.md](kien_truc.md) | Chốt module, cấu trúc file và schema trước khi chia việc |
| [pipeline.md](pipeline.md) | Chạy các bước và bàn giao đúng thứ tự |
| [ke_hoach.md](ke_hoach.md) | Phân người, thời gian và budget |
| [prompts.md](prompts.md) | Giao nội dung, code, media và kiểm tra |
| [checklist.md](checklist.md) | Chốt bản nộp và phương án dự phòng |

Trước hết dùng [prompt P0/P1](../_chung/02_prompts_dieu_hanh.md); khi giao worker dùng P2 rồi bổ sung prompt theo dạng đề. Đây là kiến trúc và prompt đề xuất để diễn tập, cần thay trường trong ngoặc vuông bằng đề thật.
