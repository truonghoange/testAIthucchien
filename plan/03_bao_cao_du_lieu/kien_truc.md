# Kiến trúc chương trình — Báo cáo dữ liệu và tài chính

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Các file dưới đây là cấu trúc chương trình dự kiến khi làm đề này. Folder `plan/` chỉ chứa tài liệu. Không cần tạo module tùy chọn nếu đề không dùng tới.

## Thành phần

| Thành phần | Đầu vào → đầu ra | Owner |
| --- | --- | --- |
| `data/raw/`, `data_dictionary.md` | File gốc → mô tả cột, kỳ, đơn vị | Hoàng |
| `scripts/analyze.py` | Dữ liệu + công thức → `out/numbers.json`, bảng, biểu đồ | Hoàng/worker phân tích |
| `data/report.json` | Chỉ số có ID + nguồn → diễn giải có dẫn ID | Hoàng, Thành duyệt |
| `scripts/render_report.*` | Nội dung + chart → PDF/DOCX theo đề | Đức/worker xuất báo cáo |

## Cấu trúc file chương trình

| Đường dẫn dưới chung-khao/ | Trách nhiệm | Đọc/phụ thuộc | Owner |
| --- | --- | --- | --- |
| `data/raw/` | Lưu bản dữ liệu gốc để đối chiếu | File được cung cấp | Hoàng |
| `data_dictionary.md` | Cột, đơn vị, kỳ, trường thiếu và định nghĩa | Dữ liệu gốc | Hoàng |
| `scripts/analyze.py` | Kiểm dữ liệu, tính chỉ số và vẽ chart | data/raw/ | Worker phân tích/Hoàng |
| `out/numbers.json` | Chỉ số chuẩn có ID, công thức và nguồn | analyze.py | Sinh bằng code |
| `out/charts/` | Biểu đồ từ số đã tính | numbers.json hoặc bảng tính cùng nguồn | Sinh bằng code |
| `data/report.json` | Nhận định dẫn metric_id | numbers.json; sources.md | Hoàng; Thành duyệt |
| `src/report.html hoặc scripts/render_docx.py` | Một renderer phù hợp định dạng đề | report.json + charts | Worker xuất báo cáo |
| `scripts/render_report.*` | Tạo file cuối và preview để kiểm trang | Template do đội dựng trong ca | Đức |
| `qa/reconciliation.md` | Đối chiếu tổng/đơn vị/kỳ và lỗi đã sửa | Số gốc + bản cuối | Thành/Hoàng |

## Hợp đồng dữ liệu

Ví dụ schema cho `out/numbers.json`. Giá trị trong ngoặc vuông là trường thay thế, không phải dữ kiện thật. `null` nghĩa là chưa có thông tin; không mặc định đó là số không. Khi chốt spec, điền dữ liệu thật và ghi rõ trường bắt buộc.

```json
[
  {
    "metric_id": "M01",
    "value": null,
    "unit": "[ĐƠN VỊ]",
    "period": "[KỲ]",
    "formula": "[CÔNG THỨC]",
    "source_file": "[FILE GỐC]",
    "source_location": "[SHEET/CỘT/DÒNG]"
  }
]
```

## Quy tắc giữa các module

- Code là nguồn duy nhất sinh số; LLM chỉ diễn giải số được bàn giao.
- Metric không tính được mang trạng thái thiếu, không được tự thay null bằng 0.
- Renderer không tự làm phép tính mới; mọi con số trong bài phải dẫn được metric_id.

## Chia task không đè file

Đức khóa schema và chia owner trước. Worker chỉ sửa file trong task; không tự thay dữ liệu đã duyệt. Nếu đổi schema, người tích hợp báo cả hai nhánh trước khi merge. Task 10–15 phút, có input/output và cách kiểm. Nội dung chờ duyệt thì worker tiếp tục dựng khung bằng dữ liệu minh họa có nhãn.

`AGENTS.md`, `requirements.json`, `sources.md`, `prompts/`, `assets/manifest.json`, `qa/` và `submission.md` dùng theo [harness chung](../_chung/01_harness.md). Hook BTC vẫn ở gốc repo; không chuyển vào thư mục plan.
