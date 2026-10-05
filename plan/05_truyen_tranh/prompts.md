# Prompt — Truyện tranh giáo dục và cảnh báo

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Dùng đúng thứ tự pipeline. Prompt ở đây bổ sung cho [P0–P4](../_chung/02_prompts_dieu_hanh.md); người phụ trách vẫn duyệt sự thật/nội dung. Điền trường thay thế, gắn spec, nguồn và task thật trước khi dùng. Các đường dẫn chương trình dưới `chung-khao/`, theo `kien_truc.md`.

**Prompt kịch bản:**

```text
Viết truyện tranh [SỐ KHUNG] về [CHỦ ĐỀ] cho [ĐỘ TUỔI], dựa trên nguồn duyệt.
Cấu trúc: tình huống quen thuộc → dấu hiệu vấn đề → lựa chọn sai → hậu quả
→ cách xử lý đúng → câu ghi nhớ. Không đổ lỗi hay làm nhục nạn nhân.
Mỗi khung có mô tả hình tiếng Anh, thoại tiếng Việt ngắn, speaker và source_id
nếu có hướng dẫn thực tế. Dùng tên/ngoại hình nhân vật cố định.
Xuất panels.json; tránh nhồi nhiều hành động vào một khung.
```

**Prompt ảnh từng khung — dùng cùng mô tả và tham chiếu đã thử:**

```text
Comic panel [ID]. [CHARACTER DESCRIPTION], [ONE ACTION], [SETTING].
Keep the same clothing, hair, age and colors as the approved character reference.
[STYLE BLOCK]. Clear expression and composition; reserve empty space for dialogue.
No text, no letters, no speech bubbles, no logos, no watermark. ref-[SUFFIX]
```

**Prompt lắp ráp:**

```text
Dựng comic.html theo panels.json, không đổi thứ tự hay lời thoại đã duyệt.
Ảnh nằm dưới lớp bóng thoại HTML/SVG; tail chỉ đúng người nói.
Theo số trang và khổ đề yêu cầu; thoại không che hành động quan trọng.
Xuất PNG/PDF. Thiếu một ảnh thì báo đúng panel_id, không tự bỏ panel.
```

**Prompt QA riêng:** `Đọc truyện từ đầu đến cuối. Kiểm thứ tự, tính nhất quán nhân vật/đạo cụ, ai nói, nguyên nhân–hậu quả và hướng dẫn xử lý. Đánh dấu khung có tay/mặt lỗi, chữ lạ, thoại che hình hoặc bài học chưa rõ.`
