# Prompt — Sáng tác bài hát

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Dùng đúng thứ tự pipeline. Prompt ở đây bổ sung cho [P0–P4](../_chung/02_prompts_dieu_hanh.md); người phụ trách vẫn duyệt sự thật/nội dung. Điền trường thay thế, gắn spec, nguồn và task thật trước khi dùng. Các đường dẫn chương trình dưới `chung-khao/`, theo `kien_truc.md`.

**Prompt lời:**

```text
Viết lời bài hát tiếng Việt cho [ĐƠN VỊ/CHỦ ĐỀ], người nghe [ĐỐI TƯỢNG].
Giữ nguyên các từ khóa bắt buộc [DANH SÁCH]. Thể loại [THỂ LOẠI],
thời lượng mục tiêu [ĐỀ YÊU CẦU], có nhãn cấu trúc phù hợp.
Điệp khúc dễ nhớ, câu ngắn dễ hát; tránh tên/từ hiếm khó phát âm.
Không thêm số liệu hoặc tuyên bố thành tích chưa có nguồn.
Trả lời bằng lyrics và style prompt riêng; không mô phỏng giọng ca sĩ thật.
```

**Prompt style Suno — ví dụ để thay theo đề:**

```text
Vietnamese pop, uplifting, clear Vietnamese diction, warm lead vocal,
memorable chorus, acoustic guitar and piano, modern clean arrangement.
```

**Prompt hoàn thiện gói:**

```text
Từ bản audio đã chọn, xác nhận thời lượng và xuất [ĐỊNH DẠNG ĐỀ YÊU CẦU].
Đính kèm lyrics.md đúng bản hát được người phụ trách nghe xác nhận.
Chỉ làm bìa/lyric video nếu requirements.json yêu cầu; chữ do code dựng.
Không cắt/căng tốc độ bài để đạt thời lượng nếu chưa được người phụ trách duyệt.
Ghi prompt/style và bản được chọn vào manifest.
```

**Prompt QA riêng:** `Nghe từ đầu đến cuối, so từng đoạn với lời: tên đơn vị, từ khóa, từ bị hát sai, cấu trúc, thời lượng và đoạn kết. Nếu có transcript AI, chỉ dùng làm gợi ý; người nghe xác nhận cuối.`
