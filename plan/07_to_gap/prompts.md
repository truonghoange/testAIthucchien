# Prompt — Tờ gấp truyền thông và hướng dẫn

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Dùng đúng thứ tự pipeline. Prompt ở đây bổ sung cho [P0–P4](../_chung/02_prompts_dieu_hanh.md); người phụ trách vẫn duyệt sự thật/nội dung. Điền trường thay thế, gắn spec, nguồn và task thật trước khi dùng. Các đường dẫn chương trình dưới `chung-khao/`, theo `kien_truc.md`.

**Prompt nội dung:**

```text
Soạn tờ gấp [KIỂU GẤP] về [CHỦ ĐỀ] cho [ĐỐI TƯỢNG], dùng nguồn đã duyệt.
Mỗi panel có một nhiệm vụ: bìa, nhận biết, tác động, xử lý, hỗ trợ, nguồn.
Ưu tiên hành động cụ thể; giọng tôn trọng, tránh hù dọa hoặc đổ lỗi.
Số điện thoại/địa chỉ chỉ điền khi có nguồn; giữ đúng panel_map.md.
Xuất brochure.json với panel_id, heading, body, action và source_id.
```

**Prompt dựng:**

```text
Dựng brochure.html theo panel_map.md và brochure.json, khổ [ĐỀ YÊU CẦU].
Xuất đúng mặt ngoài/mặt trong; chừa vùng an toàn ở nếp gấp.
Chữ tiếng Việt bằng HTML/SVG, ảnh cùng style; hotline nổi bật nếu đã được duyệt.
Xuất PDF và preview hai mặt. Không thay thứ tự panel hay thu nhỏ chữ quá mức.
```

**Prompt QA riêng:** `Kiểm bìa xuất hiện đúng sau khi gấp, các panel đọc đúng thứ tự, chữ không nằm trên nếp gấp. Đối chiếu khuyến cáo/hotline/nguồn; kiểm PDF ở khổ in thật.`
