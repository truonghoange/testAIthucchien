# Kiến trúc chương trình — Video: bản tin, quảng cáo và phim ngắn

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Các file dưới đây là cấu trúc chương trình dự kiến khi làm đề này. Folder `plan/` chỉ chứa tài liệu. Không cần tạo module tùy chọn nếu đề không dùng tới.

## Thành phần

| Thành phần | Đầu vào → đầu ra |
| --- | --- |
| `data/script.json`, `data/storyboard.json` | Kịch bản duyệt → `shot_id, narration_id, visual, duration_target, media_type` |
| TTS + `audio_manifest.json` | Đoạn đọc → audio và thời lượng thực |
| Media queue + `video_jobs.json` | Prompt/ảnh tham chiếu → ID Veo → trạng thái → MP4 tải về |
| Timeline + assembler | Audio thực, clip/ảnh, đồ họa → video nháp, phụ đề, video cuối |

## Cấu trúc file chương trình

| Đường dẫn dưới chung-khao/ | Trách nhiệm | Đọc/phụ thuộc | Owner |
| --- | --- | --- | --- |
| `data/script.json` | Lời đọc duyệt theo narration_id | Nội dung có nguồn | Hoàng; Thành duyệt |
| `data/storyboard.json` | shot_id, media_type, hình và lời tương ứng | script.json | Hoàng |
| `prompts/video.json` | Prompt từng cảnh, model và tham số | Storyboard/style | Hoàng |
| `scripts/gen_media.py` | Tạo, poll và tải; lưu ID tác vụ thật | Prompt + biến môi trường | Đức/worker media |
| `assets/video_jobs.json` | Tác vụ Veo, trạng thái và file đã tải | Kết quả API thật | Script media |
| `assets/audio_manifest.json` | Đoạn audio và thời lượng đo được | TTS/giọng được phép | Script audio |
| `data/timeline.json` | Thứ tự cảnh, timing từ audio thực | Storyboard + manifest | Đức |
| `scripts/assemble_video.py` | Chuẩn hóa, nối, ghép âm/phụ đề | Timeline + media | Worker assembler |
| `out/subtitles.srt` | Phụ đề được kiểm nội dung/timing | Lời duyệt + thời gian thật | Hoàng/Đức |
| `out/final.mp4` | Bản cuối theo định dạng đề | Assembler | Sinh bằng code |

## Hợp đồng dữ liệu

Ví dụ schema cho `data/storyboard.json`. Giá trị trong ngoặc vuông là trường thay thế, không phải dữ kiện thật. `null` nghĩa là chưa có thông tin; không mặc định đó là số không. Khi chốt spec, điền dữ liệu thật và ghi rõ trường bắt buộc.

```json
[
  {
    "shot_id": "SH01",
    "narration_id": "N01",
    "visual": "[MÔ TẢ CẢNH]",
    "duration_target": 4,
    "media_type": "veo",
    "source_id": null
  }
]
```

## Quy tắc giữa các module

- Audio manifest dùng thời lượng đo thật; duration_target chỉ là dự kiến.
- Tạo Veo một lần, lưu ID; poll/tải lại không đồng nghĩa tạo tác vụ mới.
- Mọi fallback phải giữ yêu cầu về tỷ lệ cảnh AI/định dạng nếu đề nêu.
- Lớp chữ, tên và số bằng code; scene không tự quyết định nội dung.

## Chia task không đè file

Đức khóa schema và chia owner trước. Worker chỉ sửa file trong task; không tự thay dữ liệu đã duyệt. Nếu đổi schema, người tích hợp báo cả hai nhánh trước khi merge. Task 10–15 phút, có input/output và cách kiểm. Nội dung chờ duyệt thì worker tiếp tục dựng khung bằng dữ liệu minh họa có nhãn.

`AGENTS.md`, `requirements.json`, `sources.md`, `prompts/`, `assets/manifest.json`, `qa/` và `submission.md` dùng theo [harness chung](../_chung/01_harness.md). Hook BTC vẫn ở gốc repo; không chuyển vào thư mục plan.
