# Kiến trúc chương trình — Truyện tranh giáo dục và cảnh báo

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Các file dưới đây là cấu trúc chương trình dự kiến khi làm đề này. Folder `plan/` chỉ chứa tài liệu. Không cần tạo module tùy chọn nếu đề không dùng tới.

## Thành phần

| Thành phần | Hợp đồng | Owner |
| --- | --- | --- |
| `data/characters.json` | Tên, tuổi, ngoại hình, trang phục, màu nhận diện | Hoàng, Thành duyệt |
| `data/panels.json` | `id, characters, visual_prompt, dialogue, speaker, source_id` | Hoàng |
| `assets/characters/`, `assets/panels/` | Ảnh tham chiếu và ảnh từng khung không chữ | Hoàng |
| `src/comic.html` + exporter | Panel theo thứ tự, bóng thoại tiếng Việt → PNG/PDF | Đức/worker |

## Cấu trúc file chương trình

| Đường dẫn dưới chung-khao/ | Trách nhiệm | Đọc/phụ thuộc | Owner |
| --- | --- | --- | --- |
| `data/characters.json` | Danh tính và ngoại hình cố định | Kịch bản duyệt | Hoàng |
| `data/panels.json` | Hình, thoại, người nói và thứ tự | Kịch bản + nguồn | Hoàng; Thành duyệt |
| `assets/characters/` | Ảnh tham chiếu nhân vật | Character descriptions | Hoàng |
| `assets/panels/` | Ảnh theo panel_id, không chữ | Tham chiếu + visual_prompt | Hoàng |
| `assets/manifest.json` | Ánh xạ panel_id → file/trạng thái | Kết quả sinh thật | Script media/Hoàng |
| `src/comic.html` | Khung ảnh và bóng thoại | panels.json + manifest | Worker layout |
| `src/comic.css` | Bố cục, font, tail người nói | Khổ đề + style | Worker layout |
| `scripts/export_comic.*` | Xuất PNG/PDF theo trang | Layout và asset | Đức |

## Hợp đồng dữ liệu

Ví dụ schema cho `data/panels.json`. Giá trị trong ngoặc vuông là trường thay thế, không phải dữ kiện thật. `null` nghĩa là chưa có thông tin; không mặc định đó là số không. Khi chốt spec, điền dữ liệu thật và ghi rõ trường bắt buộc.

```json
[
  {
    "id": "P01",
    "characters": [
      "NhanVatA"
    ],
    "visual_prompt": "[MÔ TẢ HÌNH]",
    "dialogue": "[THOẠI ĐÃ DUYỆT]",
    "speaker": "NhanVatA",
    "source_id": null
  }
]
```

## Quy tắc giữa các module

- Panel tham chiếu cùng characters.json; không thay áo/tên tùy cảnh.
- Bóng thoại là lớp code riêng, không yêu cầu model ảnh vẽ chữ.
- Thay ảnh theo panel_id, không đổi thứ tự và lời đã duyệt.

## Chia task không đè file

Đức khóa schema và chia owner trước. Worker chỉ sửa file trong task; không tự thay dữ liệu đã duyệt. Nếu đổi schema, người tích hợp báo cả hai nhánh trước khi merge. Task 10–15 phút, có input/output và cách kiểm. Nội dung chờ duyệt thì worker tiếp tục dựng khung bằng dữ liệu minh họa có nhãn.

`AGENTS.md`, `requirements.json`, `sources.md`, `prompts/`, `assets/manifest.json`, `qa/` và `submission.md` dùng theo [harness chung](../_chung/01_harness.md). Hook BTC vẫn ở gốc repo; không chuyển vào thư mục plan.
