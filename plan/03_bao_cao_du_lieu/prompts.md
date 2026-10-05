# Prompt — Báo cáo dữ liệu và tài chính

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Dùng đúng thứ tự pipeline. Prompt ở đây bổ sung cho [P0–P4](../_chung/02_prompts_dieu_hanh.md); người phụ trách vẫn duyệt sự thật/nội dung. Điền trường thay thế, gắn spec, nguồn và task thật trước khi dùng. Các đường dẫn chương trình dưới `chung-khao/`, theo `kien_truc.md`.

**Prompt phân tích:**

```text
Đọc [FILE DỮ LIỆU] và brief.md. Viết analyze.py tính [CHỈ SỐ ĐỀ YÊU CẦU].
Trước khi tính: kiểm cột, thiếu dữ liệu, trùng dòng, đơn vị, kỳ và mẫu số.
Không tự nội suy nếu chưa được cho phép. Mỗi chỉ số xuất metric_id, value, unit,
period, formula, source_file và vị trí gốc. Vẽ biểu đồ phù hợp, không trang trí 3D.
Đối chiếu tổng và chạy lại cho kết quả nhất quán; lưu numbers.json.
```

**Prompt nhận định:**

```text
Chỉ dùng numbers.json và sources.md đã duyệt để viết báo cáo cho [NGƯỜI ĐỌC].
Theo bố cục đề; nếu đề không nêu, mở bằng 3 phát hiện và 3 hành động.
Mỗi nhận định dẫn metric_id; tách kết quả quan sát, giả định và đề xuất.
Không thêm số, không đổi đơn vị/kỳ, không suy quan hệ nhân quả từ tương quan.
Thiếu dữ liệu thì nêu giới hạn. Xuất report.json theo schema đã chốt.
```

**Prompt QA riêng:** `Đối chiếu từng số trong báo cáo/biểu đồ với metric_id. Kiểm phần trăm và điểm phần trăm, mẫu số tăng trưởng, kỳ so sánh, nhãn trục, làm tròn và tổng. Báo đúng vị trí sai; không tự chế số sửa.`
