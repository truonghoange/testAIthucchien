# Kiến trúc chương trình — Sáng tác bài hát

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Các file dưới đây là cấu trúc chương trình dự kiến khi làm đề này. Folder `plan/` chỉ chứa tài liệu. Không cần tạo module tùy chọn nếu đề không dùng tới.

## Thành phần

| Thành phần | Đầu vào → đầu ra | Owner |
| --- | --- | --- |
| `data/lyrics.md`, `style.txt` | Thông điệp duyệt → lời, cấu trúc, thể loại | Hoàng; Thành duyệt |
| Suno BTC cấp | Lyrics/style → các bản audio theo quota | Hoàng vận hành |
| `assets/song_manifest.json` | Bản audio, prompt thật, thời lượng, lỗi nghe được | Hoàng |
| Gói xuất | Audio cuối + lời; bìa/lyric video chỉ khi đề cần | Đức |

## Cấu trúc file chương trình

| Đường dẫn dưới chung-khao/ | Trách nhiệm | Đọc/phụ thuộc | Owner |
| --- | --- | --- | --- |
| `data/lyrics.md` | Lời và cấu trúc được duyệt | Thông điệp/từ khóa | Hoàng; Thành duyệt |
| `data/style.txt` | Thể loại, phối khí, giọng theo đề | Định hướng đã chốt | Hoàng |
| `prompts/song.md` | Prompt/style thật dùng tạo bài | Lyrics/style | Hoàng |
| `assets/song/` | Các bản audio đã tải | Suno BTC cấp theo quota | Hoàng thao tác |
| `assets/song_manifest.json` | Bản, duration, lỗi nghe và lựa chọn | Audio thật | Hoàng |
| `scripts/export_song.py` | Chuẩn hóa/xuất đúng loại file | Bản audio được chọn | Đức/worker export |
| `src/lyrics.html` | Bố cục lyric/bìa nếu đề yêu cầu | Lời bản hát cuối | Worker layout; tùy chọn |
| `out/` | Audio cuối, lời và media bắt buộc | Bản chọn + exporter | Đức |

## Hợp đồng dữ liệu

Ví dụ schema cho `assets/song_manifest.json`. Giá trị trong ngoặc vuông là trường thay thế, không phải dữ kiện thật. `null` nghĩa là chưa có thông tin; không mặc định đó là số không. Khi chốt spec, điền dữ liệu thật và ghi rõ trường bắt buộc.

```json
[
  {
    "version_id": "V01",
    "audio_path": "assets/song/V01.mp3",
    "duration_seconds": null,
    "reviewed": false,
    "selected": false,
    "notes": "[LỖI HOẶC LÝ DO CHỌN]"
  }
]
```

## Quy tắc giữa các module

- Suno là thao tác tài khoản riêng; không giả định có API Gateway cho Suno.
- Trường selected chỉ đặt sau khi người nghe kiểm từ khóa và lời.
- Không tự chỉnh tốc độ/cắt bài để khớp thời lượng khi chưa duyệt.

## Chia task không đè file

Đức khóa schema và chia owner trước. Worker chỉ sửa file trong task; không tự thay dữ liệu đã duyệt. Nếu đổi schema, người tích hợp báo cả hai nhánh trước khi merge. Task 10–15 phút, có input/output và cách kiểm. Nội dung chờ duyệt thì worker tiếp tục dựng khung bằng dữ liệu minh họa có nhãn.

`AGENTS.md`, `requirements.json`, `sources.md`, `prompts/`, `assets/manifest.json`, `qa/` và `submission.md` dùng theo [harness chung](../_chung/01_harness.md). Hook BTC vẫn ở gốc repo; không chuyển vào thư mục plan.
