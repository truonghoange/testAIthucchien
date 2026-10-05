# Prompt — Website, web app và công cụ AI

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Dùng đúng thứ tự pipeline. Prompt ở đây bổ sung cho [P0–P4](../_chung/02_prompts_dieu_hanh.md); người phụ trách vẫn duyệt sự thật/nội dung. Điền trường thay thế, gắn spec, nguồn và task thật trước khi dùng. Các đường dẫn chương trình dưới `chung-khao/`, theo `kien_truc.md`.

**Prompt nội dung — Hoàng, sau khi Thành chốt nguồn:**

```text
Từ sources.md đã duyệt, tạo content.json cho [WEBSITE/APP], người dùng [ĐỐI TƯỢNG].
Mỗi mục có id, title, body, source_id và asset_id. Nêu đúng thông tin đã có nguồn.
Viết ngắn, phù hợp hành động [VIỆC NGƯỜI DÙNG CẦN LÀM].
Thiếu thông tin thì ghi unknown, không bịa địa chỉ, giá, hotline hay công dụng.
Tuân thủ schema trong AGENTS.md; chưa dựng giao diện.
```

**Prompt triển khai — worker code:**

```text
Dựng [CÁC MỤC BẮT BUỘC] bằng Vite + JavaScript, đọc data/content.json.
Ưu tiên luồng [LUỒNG CHÍNH]; có trạng thái rỗng/lỗi và nút thao tác thực sự hoạt động.
Nếu đề cần AI, frontend gọi serverless /api/assist; không đưa key vào bundle.
Chỉ dùng stack đã chốt, không thêm auth, thanh toán hay RAG ngoài yêu cầu.
Xong khi build đạt và chạy trọn luồng trên viewport 390px và desktop.
```

**Prompt QA riêng:** `Thử [LUỒNG CHÍNH], refresh, dữ liệu rỗng, mạng/API lỗi, link trực tiếp và viewport nhỏ. Báo bước tái hiện; kiểm bundle không chứa key. Phân biệt dữ liệu minh họa với dữ liệu địa phương thật.`
