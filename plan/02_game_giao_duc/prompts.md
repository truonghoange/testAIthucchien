# Prompt — Game giáo dục

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Dùng đúng thứ tự pipeline. Prompt ở đây bổ sung cho [P0–P4](../_chung/02_prompts_dieu_hanh.md); người phụ trách vẫn duyệt sự thật/nội dung. Điền trường thay thế, gắn spec, nguồn và task thật trước khi dùng. Các đường dẫn chương trình dưới `chung-khao/`, theo `kien_truc.md`.

**Prompt nội dung:**

```text
Tạo [N] tình huống game về [CHỦ ĐỀ] cho [ĐỘ TUỔI], chỉ dùng nguồn đã duyệt.
Mỗi tình huống có đúng một đáp án đúng, lựa chọn nhiễu hợp lý,
giải thích dễ hiểu và source_id. Tránh mẹo ngôn ngữ hay kiến thức ngoài độ tuổi.
Xuất JSON theo schema questions.json; không tự xác nhận tính đúng của nguồn.
```

**Prompt triển khai:**

```text
Làm một vòng game [CƠ CHẾ], đọc questions.json đã duyệt.
Có start, playing, feedback, result và restart; khóa input sau khi chọn đáp án.
Hiển thị vì sao đúng/sai, tính điểm đúng luật trong AGENTS.md.
Hỗ trợ chuột và chạm, có nút tắt âm; asset thiếu thì dùng hình đơn giản.
Không đổi nội dung câu hỏi. Xong khi chơi hết một lượt rồi chơi lại không lỗi.
```

**Prompt QA riêng:** `Kiểm đúng/sai/nhấp đôi/hết câu/chơi lại. Xác minh mỗi câu đúng một đáp án và explanation khớp. Kiểm điểm không tăng hai lần, âm chỉ bật sau tương tác, nút đủ dễ chạm.`
