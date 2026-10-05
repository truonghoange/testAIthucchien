# Kiến trúc chương trình — Chiến dịch đa định dạng và poster

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Các file dưới đây là cấu trúc chương trình dự kiến khi làm đề này. Folder `plan/` chỉ chứa tài liệu. Không cần tạo module tùy chọn nếu đề không dùng tới.

## Thành phần

| Thành phần | Đầu vào → đầu ra | Owner |
| --- | --- | --- |
| `data/campaign.json` | Đối tượng, nhu cầu, thông điệp, slogan, CTA, style | Hoàng, Thành duyệt |
| `data/deliverables.json` | ID yêu cầu → format/kênh/khổ/owner → file | Đức điều phối |
| Các nhánh sản xuất | Key visual/poster, video, bài đăng, landing nếu đề cần | Hoàng media/nội dung; Đức lắp ráp |
| `out/` và index | Bộ file cùng nhận diện + kế hoạch triển khai/đo lường | Đức |

## Cấu trúc file chương trình

| Đường dẫn dưới chung-khao/ | Trách nhiệm | Đọc/phụ thuộc | Owner |
| --- | --- | --- | --- |
| `data/campaign.json` | Thông điệp, slogan, CTA, style duyệt | Brief + nguồn | Hoàng; Thành duyệt |
| `data/deliverables.json` | ID, kênh, khổ, thời lượng, owner, file | Yêu cầu đề | Đức |
| `data/copy.json` | Bài đăng/nhận định theo ID sản phẩm | campaign.json + nguồn | Hoàng |
| `src/poster.html` | Key visual với chữ code | campaign.json + ảnh | Worker poster |
| `scripts/export_poster.*` | Xuất các khổ/crop cần nộp | Poster + deliverables | Đức |
| `data/storyboard.json; scripts/assemble_video.py` | Nhánh video nếu bắt buộc | Cùng message/style | Hoàng/worker video |
| `src/landing/` | Nhánh web nếu bắt buộc | Cùng message/CTA | Worker web |
| `out/` | File từng nhánh theo deliverable_id | Các exporter | Đức tích hợp |
| `submission.md` | Ma trận yêu cầu → file/link | deliverables.json + QA | Đức; Thành chốt |

## Hợp đồng dữ liệu

Ví dụ schema cho `data/deliverables.json`. Giá trị trong ngoặc vuông là trường thay thế, không phải dữ kiện thật. `null` nghĩa là chưa có thông tin; không mặc định đó là số không. Khi chốt spec, điền dữ liệu thật và ghi rõ trường bắt buộc.

```json
[
  {
    "id": "D01",
    "requirement_id": "REQ01",
    "format": "png",
    "channel": "[KÊNH]",
    "size": "[KHỔ TỪ ĐỀ]",
    "duration": null,
    "owner": "[NGƯỜI PHỤ TRÁCH]",
    "output_path": "out/D01.png"
  }
]
```

## Quy tắc giữa các module

- Một campaign.json dùng chung; mỗi nhánh không tự đổi slogan/CTA.
- Một worker sở hữu một nhóm file, Đức tích hợp vào ma trận.
- KPI mục tiêu ghi rõ là mục tiêu; không viết thành số hiệu quả thực.

## Chia task không đè file

Đức khóa schema và chia owner trước. Worker chỉ sửa file trong task; không tự thay dữ liệu đã duyệt. Nếu đổi schema, người tích hợp báo cả hai nhánh trước khi merge. Task 10–15 phút, có input/output và cách kiểm. Nội dung chờ duyệt thì worker tiếp tục dựng khung bằng dữ liệu minh họa có nhãn.

`AGENTS.md`, `requirements.json`, `sources.md`, `prompts/`, `assets/manifest.json`, `qa/` và `submission.md` dùng theo [harness chung](../_chung/01_harness.md). Hook BTC vẫn ở gốc repo; không chuyển vào thư mục plan.
