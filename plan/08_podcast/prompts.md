# Prompt — Podcast tư vấn, giáo dục và kể chuyện

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Dùng đúng thứ tự pipeline. Prompt ở đây bổ sung cho [P0–P4](../_chung/02_prompts_dieu_hanh.md); người phụ trách vẫn duyệt sự thật/nội dung. Điền trường thay thế, gắn spec, nguồn và task thật trước khi dùng. Các đường dẫn chương trình dưới `chung-khao/`, theo `kien_truc.md`.

**Prompt kịch bản:**

```text
Viết podcast [THỜI LƯỢNG] về [CHỦ ĐỀ] cho [ĐỐI TƯỢNG], từ nguồn duyệt.
[MỘT GIỌNG/HAI VAI] theo yêu cầu đề. Mở bằng một tình huống gần người nghe,
giải thích lần lượt, kết bằng 3 hành động nếu phù hợp nội dung.
Câu ngắn, văn nói tự nhiên, số viết bằng chữ và từ viết tắt viết đầy đủ.
Không đưa chẩn đoán hoặc thay đổi thuốc cá nhân khi nguồn không cho phép.
Xuất dialogue.json: segment_id, speaker, text, source_id.
```

**Prompt sản xuất TTS và mix:**

```text
Tạo TTS từ dialogue.json đã duyệt, giữ mapping speaker → voice cố định.
Thử một đoạn mỗi voice trước; key đọc từ môi trường, không in secret.
Lưu từng file theo segment_id, đo duration và tạo audio_manifest.json.
Nối đúng thứ tự, khoảng nghỉ tự nhiên; nhạc nền được phép thấp hơn giọng.
Xuất [ĐỊNH DẠNG] và transcript; không tự sửa lời khi ghép.
```

**Prompt QA riêng:** `Nghe toàn bộ ở tốc độ bình thường: tên/số/từ chuyên môn, giọng vai, ngắt câu, đoạn thiếu/lặp, âm vỡ và nhạc lấn giọng. Đối chiếu transcript và duration với đề; báo segment_id cần sửa.`
