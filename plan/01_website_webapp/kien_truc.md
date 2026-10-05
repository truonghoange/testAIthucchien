# Kiến trúc chương trình — Website, web app và công cụ AI

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Các file dưới đây là cấu trúc chương trình dự kiến khi làm đề này. Folder `plan/` chỉ chứa tài liệu. Không cần tạo module tùy chọn nếu đề không dùng tới.

## Thành phần

| Thành phần | Đầu vào → đầu ra | Phạm vi |
| --- | --- | --- |
| Vite + JavaScript, UI responsive | `data/content.json`, ảnh → trang và tương tác | Một ứng dụng; mỗi trang/module có owner |
| Dữ liệu nội dung | Nguồn duyệt → JSON có `source_id` | Tách nội dung khỏi layout |
| Serverless `/api/assist`, nếu cần AI | Input giới hạn → Gateway → JSON kết quả | Key server-side, timeout, hạn mức lượt, xử lý lỗi |
| Deploy + QA | Build → link → bằng chứng luồng chính | Deploy khung T+30; kiểm bản cuối bằng cửa sổ ẩn danh |

## Cấu trúc file chương trình

| Đường dẫn dưới chung-khao/ | Trách nhiệm | Đọc/phụ thuộc | Owner |
| --- | --- | --- | --- |
| `index.html` | Điểm vào ứng dụng | src/main.js | Đức |
| `src/main.js` | Khởi tạo UI, routing và trạng thái | UI + data adapter | Worker code 1 |
| `src/ui/` | Trang, form, bộ lọc, kết quả và thông báo lỗi | content.json; trạng thái ứng dụng | Worker code 2 |
| `src/data.js` | Đọc và kiểm schema nội dung | data/content.json | Worker code 1 |
| `src/api.js` | Gọi /api/assist khi đề cần AI | Serverless endpoint | Worker code 1 |
| `api/assist.*` | Input validation, timeout, quota; key ở server | Gateway; biến môi trường | Đức; chỉ khi đề cần |
| `data/content.json` | Nội dung và ánh xạ ảnh có nguồn | sources.md | Hoàng; Thành duyệt |
| `assets/` | Ảnh và manifest | Prompt/style duyệt | Hoàng |
| `src/styles.css` | Layout responsive và trạng thái focus | Style trong AGENTS.md | Worker code 2 |
| `package.json` | Lệnh dev/build và dependency đã chốt | Stack đã luyện | Đức |

## Hợp đồng dữ liệu

Ví dụ schema cho `data/content.json`. Giá trị trong ngoặc vuông là trường thay thế, không phải dữ kiện thật. `null` nghĩa là chưa có thông tin; không mặc định đó là số không. Khi chốt spec, điền dữ liệu thật và ghi rõ trường bắt buộc.

```json
[
  {
    "id": "item-01",
    "title": "[TIÊU ĐỀ]",
    "body": "[NỘI DUNG ĐÃ DUYỆT]",
    "source_id": "SRC-01",
    "asset_id": "hero-01"
  }
]
```

## Quy tắc giữa các module

- UI đọc content qua một adapter; không hardcode sự thật trong component.
- Nếu cần AI: frontend → serverless → Gateway; JSON kết quả phải được kiểm trước khi hiển thị.
- Dữ liệu mẫu ghi rõ là minh họa. Nếu cần lưu thật, kiểm được dữ liệu qua refresh.

## Chia task không đè file

Đức khóa schema và chia owner trước. Worker chỉ sửa file trong task; không tự thay dữ liệu đã duyệt. Nếu đổi schema, người tích hợp báo cả hai nhánh trước khi merge. Task 10–15 phút, có input/output và cách kiểm. Nội dung chờ duyệt thì worker tiếp tục dựng khung bằng dữ liệu minh họa có nhãn.

`AGENTS.md`, `requirements.json`, `sources.md`, `prompts/`, `assets/manifest.json`, `qa/` và `submission.md` dùng theo [harness chung](../_chung/01_harness.md). Hook BTC vẫn ở gốc repo; không chuyển vào thư mục plan.
