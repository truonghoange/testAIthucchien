# Prompt — Video: bản tin, quảng cáo và phim ngắn

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Dùng đúng thứ tự pipeline. Prompt ở đây bổ sung cho [P0–P4](../_chung/02_prompts_dieu_hanh.md); người phụ trách vẫn duyệt sự thật/nội dung. Điền trường thay thế, gắn spec, nguồn và task thật trước khi dùng. Các đường dẫn chương trình dưới `chung-khao/`, theo `kien_truc.md`.

**Prompt kịch bản và storyboard:**

```text
Viết [BẢN TIN/QUẢNG CÁO/PHIM NGẮN] cho [ĐỐI TƯỢNG], thời lượng [ĐỀ YÊU CẦU].
Chỉ dùng khẳng định trong sources.md đã duyệt. Xuất lời đọc tiếng Việt,
storyboard gồm shot_id, narration_id, thời lượng dự kiến, mô tả hình tiếng Anh,
loại media và source_id. Mỗi cảnh Veo chỉ có một hành động rõ.
Tối đa [N] cảnh Veo theo budget; các cảnh còn lại dùng đồ họa/ảnh khi đề cho phép.
Không làm MC giống người thật; đánh dấu nội dung là minh họa nếu cần.
```

**Prompt Veo — thay nội dung cảnh cụ thể:**

```text
[SHOT TYPE AND CAMERA MOVEMENT], [SUBJECT] [ONE ACTION], [SETTING].
[LIGHTING], [STYLE BLOCK], [MOOD]. Preserve the approved character appearance.
No on-screen text, no logos. Ambient sound only, no dialogue, no music.
```

**Prompt worker assembler:**

```text
Viết assembler từ storyboard.json và manifest media/audio thực tế.
Ghép theo narration_id và thời lượng audio đã đo, không cắt mất lời đọc.
Chuẩn hóa [KHUNG HÌNH/FPS]; phụ đề tiếng Việt từ lời đã duyệt và timing đã kiểm.
Nhạc nền thấp hơn giọng; thiếu clip thì chỉ dùng fallback đã được cho phép.
Xuất bản nháp và báo duration, resolution, audio track của file cuối.
Không gọi sinh media mới và không tự đổi kịch bản.
```

**Prompt QA riêng:** `Kiểm toàn video: tên/ngày/số, lời đọc trùng nội dung duyệt, timing phụ đề, đoạn đen, khung lỗi, âm lấn giọng, cuối bị cắt và thời lượng. Nếu đề quy định tỷ lệ cảnh/video AI thì tính lại từ timeline.`
