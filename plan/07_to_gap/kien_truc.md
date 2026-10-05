# Kiến trúc chương trình — Tờ gấp truyền thông và hướng dẫn

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Các file dưới đây là cấu trúc chương trình dự kiến khi làm đề này. Folder `plan/` chỉ chứa tài liệu. Không cần tạo module tùy chọn nếu đề không dùng tới.

## Thành phần

| Thành phần | Hợp đồng |
| --- | --- |
| `data/brochure.json` | `panel_id, role, heading, body, action, source_id` |
| `panel_map.md` | Mặt ngoài/mặt trong, chiều đọc, mặt gập, bìa và mặt sau |
| `src/brochure.html`, `assets/` | Layout in với chữ code và minh họa không chữ |
| Export | PDF hai mặt đúng khổ; bản preview từng mặt để kiểm |

## Cấu trúc file chương trình

| Đường dẫn dưới chung-khao/ | Trách nhiệm | Đọc/phụ thuộc | Owner |
| --- | --- | --- | --- |
| `panel_map.md` | Mặt ngoài/trong, chiều gấp và vị trí bìa | Kiểu gấp đề yêu cầu | Đức; Thành duyệt |
| `data/brochure.json` | Nội dung theo panel_id | Nguồn + panel map | Hoàng; Thành duyệt |
| `src/brochure.html` | Layout đúng vị trí panel | brochure.json + assets | Worker layout |
| `src/brochure.css` | Khổ in, nếp gấp, vùng chữ an toàn | Thông số đề/nhà in nếu có | Worker layout |
| `assets/` | Minh họa không chữ | Style chung | Hoàng |
| `scripts/export_brochure.*` | Xuất PDF và preview hai mặt | HTML + font | Đức |
| `out/brochure.pdf` | Tờ gấp cuối | Exporter | Sinh bằng code |
| `qa/fold_check.md` | Kiểm bìa/chiều đọc/nếp gấp | Preview ở khổ thật | Thành/Đức |

## Hợp đồng dữ liệu

Ví dụ schema cho `data/brochure.json`. Giá trị trong ngoặc vuông là trường thay thế, không phải dữ kiện thật. `null` nghĩa là chưa có thông tin; không mặc định đó là số không. Khi chốt spec, điền dữ liệu thật và ghi rõ trường bắt buộc.

```json
[
  {
    "panel_id": "P01",
    "role": "cover",
    "heading": "[TIÊU ĐỀ]",
    "body": "[NỘI DUNG DUYỆT]",
    "action": "[HÀNH ĐỘNG]",
    "source_id": "SRC-01"
  }
]
```

## Quy tắc giữa các module

- panel_map.md là nguồn quyết định thứ tự; không đảo theo suy đoán.
- Hotline/địa chỉ chỉ hiển thị khi có nguồn được duyệt.
- Không tự thu nhỏ chữ hoặc bỏ nội dung để vừa panel.

## Chia task không đè file

Đức khóa schema và chia owner trước. Worker chỉ sửa file trong task; không tự thay dữ liệu đã duyệt. Nếu đổi schema, người tích hợp báo cả hai nhánh trước khi merge. Task 10–15 phút, có input/output và cách kiểm. Nội dung chờ duyệt thì worker tiếp tục dựng khung bằng dữ liệu minh họa có nhãn.

`AGENTS.md`, `requirements.json`, `sources.md`, `prompts/`, `assets/manifest.json`, `qa/` và `submission.md` dùng theo [harness chung](../_chung/01_harness.md). Hook BTC vẫn ở gốc repo; không chuyển vào thư mục plan.
