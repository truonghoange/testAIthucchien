# Prompt — Chiến dịch đa định dạng và poster

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Dùng đúng thứ tự pipeline. Prompt ở đây bổ sung cho [P0–P4](../_chung/02_prompts_dieu_hanh.md); người phụ trách vẫn duyệt sự thật/nội dung. Điền trường thay thế, gắn spec, nguồn và task thật trước khi dùng. Các đường dẫn chương trình dưới `chung-khao/`, theo `kien_truc.md`.

**Prompt chiến lược:**

```text
Lập chiến dịch [CHỦ ĐỀ/DỊP] cho [THƯƠNG HIỆU], đối tượng [ĐỐI TƯỢNG].
Từ brief và nguồn duyệt, xuất campaign.json: insight (ghi rõ nếu là giả định),
big_idea, message, slogan, CTA, style và deliverables theo đúng đề.
Mỗi sản phẩm có kênh, mục tiêu, định dạng, khổ/thời lượng và ID yêu cầu.
Nếu đề yêu cầu lịch/KPI, tách chỉ tiêu mục tiêu khỏi số liệu thực tế;
không bịa độ phủ, doanh số hoặc ngân sách quảng cáo.
```

**Prompt key visual/poster:**

```text
Dựng poster theo campaign.json: một hình chủ đạo, thông điệp và CTA đã duyệt.
Sinh ảnh nền không chữ, cùng STYLE BLOCK; chữ tiếng Việt ghép bằng HTML/SVG.
Xuất đúng các tỷ lệ [DANH SÁCH TỪ ĐỀ], kiểm từng bản crop không mất chủ thể/chữ.
Giữ slogan và nhận diện thống nhất với video/bài đăng; không tự thêm claim.
```

**Prompt các nhánh:**

```text
Đọc campaign.json, deliverables.json và task được giao.
Sản xuất riêng [ID SẢN PHẨM] theo format/khổ/thời lượng đã chốt.
Giữ nguyên message, slogan, CTA và style. Nội dung có claim phải dẫn source_id.
Không sửa sản phẩm của nhánh khác. Nếu thiếu đầu vào, báo ID thiếu;
không tự tạo thông điệp mới. Dùng plan video/web tương ứng nếu task cần.
```

**Prompt QA riêng:** `Lập ma trận yêu cầu → file, kiểm đủ số lượng/format/khổ/thời lượng. So slogan, CTA, màu, tên thương hiệu và claim giữa mọi sản phẩm. KPI nào là mục tiêu phải ghi là mục tiêu; file nào thiếu nội dung phải báo.`
