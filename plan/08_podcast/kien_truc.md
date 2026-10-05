# Kiến trúc chương trình — Podcast tư vấn, giáo dục và kể chuyện

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Các file dưới đây là cấu trúc chương trình dự kiến khi làm đề này. Folder `plan/` chỉ chứa tài liệu. Không cần tạo module tùy chọn nếu đề không dùng tới.

## Thành phần

| Thành phần | Đầu vào → đầu ra |
| --- | --- |
| `data/dialogue.json` | `segment_id, speaker, text, source_id` đã duyệt |
| `voices.json` và TTS queue | Speaker → giọng cố định → file đoạn |
| Audio manifest | File → thứ tự → thời lượng thật → trạng thái QA |
| `scripts/mix_audio.*` | Đoạn, khoảng nghỉ, nhạc được phép → MP3/WAV theo đề |

## Cấu trúc file chương trình

| Đường dẫn dưới chung-khao/ | Trách nhiệm | Đọc/phụ thuộc | Owner |
| --- | --- | --- | --- |
| `data/dialogue.json` | Đoạn thoại duyệt theo speaker/segment_id | Nguồn chuyên môn | Hoàng; Thành duyệt |
| `data/voices.json` | Mapping speaker → voice cố định | Đoạn thử giọng | Hoàng |
| `scripts/gen_tts.py` | Sinh đoạn, lưu theo ID, đo duration | Dialogue + voices | Đức/worker script |
| `assets/audio/` | File từng đoạn | Kết quả TTS thật | Script TTS |
| `assets/audio_manifest.json` | Thứ tự, file, duration và QA | Audio thật | Script TTS/Hoàng |
| `scripts/mix_audio.py` | Nối, khoảng nghỉ và nhạc được phép | Manifest + music tùy chọn | Worker audio |
| `out/podcast.*` | Audio cuối theo đề | Mixer | Đức |
| `out/transcript.md` | Lời tương ứng bản cuối | Dialogue đã nghe xác nhận | Hoàng |

## Hợp đồng dữ liệu

Ví dụ schema cho `data/dialogue.json`. Giá trị trong ngoặc vuông là trường thay thế, không phải dữ kiện thật. `null` nghĩa là chưa có thông tin; không mặc định đó là số không. Khi chốt spec, điền dữ liệu thật và ghi rõ trường bắt buộc.

```json
[
  {
    "segment_id": "SEG01",
    "speaker": "Host",
    "text": "[LỜI ĐÃ DUYỆT]",
    "source_id": null
  }
]
```

## Quy tắc giữa các module

- Một speaker dùng một giọng đã chốt; sinh lại chỉ đoạn có lỗi.
- Khoảng nghỉ và nhạc không làm lời khó nghe hoặc cắt đoạn.
- Timing theo audio thật; kịch bản phải được sửa có duyệt nếu lệch thời lượng.

## Chia task không đè file

Đức khóa schema và chia owner trước. Worker chỉ sửa file trong task; không tự thay dữ liệu đã duyệt. Nếu đổi schema, người tích hợp báo cả hai nhánh trước khi merge. Task 10–15 phút, có input/output và cách kiểm. Nội dung chờ duyệt thì worker tiếp tục dựng khung bằng dữ liệu minh họa có nhãn.

`AGENTS.md`, `requirements.json`, `sources.md`, `prompts/`, `assets/manifest.json`, `qa/` và `submission.md` dùng theo [harness chung](../_chung/01_harness.md). Hook BTC vẫn ở gốc repo; không chuyển vào thư mục plan.
