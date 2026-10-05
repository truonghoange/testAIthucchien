# Prompt — Infographic pháp luật và chính sách

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Dùng đúng thứ tự pipeline. Prompt ở đây bổ sung cho [P0–P4](../_chung/02_prompts_dieu_hanh.md); người phụ trách vẫn duyệt sự thật/nội dung. Điền trường thay thế, gắn spec, nguồn và task thật trước khi dùng. Các đường dẫn chương trình dưới `chung-khao/`, theo `kien_truc.md`.

**Prompt nội dung:**

```text
Từ [VĂN BẢN CHÍNH THỨC] tạo nội dung infographic cho [ĐỐI TƯỢNG].
Mỗi khối có heading, body, action, article, clause, source_id.
Giữ đúng chủ thể, điều kiện, ngoại lệ và hiệu lực. Tối đa 6 khối nếu đủ yêu cầu đề.
Tiêu đề ngắn, câu dễ hiểu; ghi câu nào chưa thể rút gọn mà không đổi nghĩa.
Không tự thêm mức phạt, số điều hoặc nghĩa vụ không có trong nguồn.
```

**Prompt dựng:**

```text
Dựng infographic từ data/infographic.json, khổ [RỘNG x CAO] theo đề.
Chữ tiếng Việt là HTML/SVG, ảnh AI chỉ là minh họa không chữ.
Có thứ bậc tiêu đề, khối nội dung, nguồn/hiệu lực; style theo AGENTS.md.
Xuất [PNG/PDF] vào out/. Không cắt chữ; kiểm ở kích thước nộp thật.
Không tự sửa câu đã duyệt để vừa layout; báo khối quá dài cho người phụ trách.
```

**Prompt QA riêng:** `Đối chiếu từng khối với claims.json và văn bản. Kiểm điều/khoản, ngoại lệ, hiệu lực và cách diễn đạt. Sau đó kiểm dấu tiếng Việt, chữ nhỏ, độ tương phản và kích thước file.`
