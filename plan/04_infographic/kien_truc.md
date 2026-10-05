# Kiến trúc chương trình — Infographic pháp luật và chính sách

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Các file dưới đây là cấu trúc chương trình dự kiến khi làm đề này. Folder `plan/` chỉ chứa tài liệu. Không cần tạo module tùy chọn nếu đề không dùng tới.

## Thành phần

| Thành phần | Đầu vào → đầu ra |
| --- | --- |
| `data/claims.json` | Văn bản đúng phiên bản/hiệu lực → khẳng định có `source_id, article, clause` |
| `data/infographic.json` | Khẳng định đã duyệt → tiêu đề, khối nội dung, hành động |
| `assets/` + `src/infographic.html` | Icon/ảnh không chữ + chữ tiếng Việt bằng HTML/SVG |
| Export và QA | Khổ đề → PNG/PDF; kiểm hiển thị đúng kích thước |

## Cấu trúc file chương trình

| Đường dẫn dưới chung-khao/ | Trách nhiệm | Đọc/phụ thuộc | Owner |
| --- | --- | --- | --- |
| `data/claims.json` | Khẳng định, điều/khoản/nguồn | Văn bản gốc đúng hiệu lực | Hoàng; Thành duyệt |
| `data/infographic.json` | Khối nội dung và hành động | claims.json | Hoàng; Thành duyệt |
| `src/infographic.html` | Layout và chữ tiếng Việt | JSON + assets | Worker layout |
| `src/infographic.css` | Thứ bậc chữ, khoảng cách, màu | Style và khổ đề | Worker layout |
| `assets/` | Icon/ảnh không chữ | Prompt/style duyệt | Hoàng |
| `scripts/export_infographic.*` | Xuất PNG/PDF đúng viewport/khổ | HTML + font | Đức |
| `out/` | Bản nháp, bản cuối | Exporter | Sinh bằng code |
| `qa/claims_review.md` | Đối chiếu nghĩa, điều/khoản và hiệu lực | Văn bản + bản cuối | Thành |

## Hợp đồng dữ liệu

Ví dụ schema cho `data/infographic.json`. Giá trị trong ngoặc vuông là trường thay thế, không phải dữ kiện thật. `null` nghĩa là chưa có thông tin; không mặc định đó là số không. Khi chốt spec, điền dữ liệu thật và ghi rõ trường bắt buộc.

```json
[
  {
    "id": "B01",
    "heading": "[TIÊU ĐỀ]",
    "body": "[NỘI DUNG DUYỆT]",
    "action": "[HÀNH ĐỘNG]",
    "article": "[ĐIỀU]",
    "clause": "[KHOẢN]",
    "source_id": "SRC-01"
  }
]
```

## Quy tắc giữa các module

- Khối UI không tự rút gọn câu pháp lý để vừa chỗ.
- Giữ điều kiện, chủ thể và ngoại lệ; nguồn ở vị trí đọc được.
- Ảnh không chứa chữ; toàn bộ chữ do HTML/SVG dựng.

## Chia task không đè file

Đức khóa schema và chia owner trước. Worker chỉ sửa file trong task; không tự thay dữ liệu đã duyệt. Nếu đổi schema, người tích hợp báo cả hai nhánh trước khi merge. Task 10–15 phút, có input/output và cách kiểm. Nội dung chờ duyệt thì worker tiếp tục dựng khung bằng dữ liệu minh họa có nhãn.

`AGENTS.md`, `requirements.json`, `sources.md`, `prompts/`, `assets/manifest.json`, `qa/` và `submission.md` dùng theo [harness chung](../_chung/01_harness.md). Hook BTC vẫn ở gốc repo; không chuyển vào thư mục plan.
