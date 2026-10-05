# Quy định, giả định và nguồn

[Mục lục plan](../README.md) · [Hướng dẫn chung](README.md)

Đây là kế hoạch diễn tập cho các dạng sản phẩm trong tài liệu hiện có, chưa phải danh sách đề vòng này. Khi nhận đề, thay các trường `[ĐỀ]`, `[ĐỐI TƯỢNG]`, `[THỜI LƯỢNG]`, `[ĐỊNH DẠNG]` bằng yêu cầu thực tế. Những con số như sáu khung tranh, ba biểu đồ hay video chín mươi giây bên dưới là cấu hình gợi ý khi đề không quy định; yêu cầu đề luôn được ưu tiên.

Lịch lấy **120 phút làm bài** từ file chiến lược đã có; hướng dẫn công khai xác nhận có **10 phút nộp sau giờ làm bài**. Chưa đọc được PDF training dẫn trong tài liệu cũ, nên các chi tiết “tối đa 20 file/500 MB”, “video thuyết trình 3–6 phút trong 24 giờ”, quyền mang prompt/code/tài liệu chuẩn bị trước và phạm vi cấm công cụ phải đối chiếu lại với thông báo gửi đội. Không coi mẫu luyện tập này là tài liệu mặc nhiên được mang vào ca thi. [BTC-01]

| Căn cứ | Áp dụng vào plan |
| --- | --- |
| Quy định công khai: 3 thí sinh, 2 máy tính, 2 điện thoại giám sát | Chia ba vai người; giới hạn việc vận hành trên hai máy. File nộp và đường nộp theo đề. [BTC-01] |
| README repo đính kèm | Thành là đội trưởng; Hoàng phụ trách AI/Data; Đức phụ trách Systems/Backend. Toàn bộ source, tài liệu và demo vòng này đặt dưới `chung-khao/`; giữ cấu trúc BTC tạo. |
| Hướng dẫn AI Log | Kiểm tra prompt/tool/kết thúc lượt có log thật và gửi thành công; mở agent ở gốc repo. Push thành công chưa chứng minh log đã gửi. Không để AI mở hoặc in file chứa secret. [BTC-02] |
| Bảng giá và rate limit | Hạn mức chính thức 50 USD; hai key cùng đội chia sẻ bộ đếm tốc độ, mỗi key tối đa 10 request đồng thời. Phân biệt 429 tốc độ với 429 hết budget. [BTC-03, BTC-04] |
| VibeCoding và Codex | Kế hoạch → task nhỏ → kiểm tra → duyệt diff; chọn model nhỏ cho worker. Codex qua provider Gateway và Responses API, không chỉ dựa vào việc đã đăng nhập ứng dụng. [BTC-05, BTC-06] |
| Ảnh và Veo | `nano-banana-2-lite` cho thử ảnh; Veo phải lưu ID, theo dõi trạng thái, tải kết quả. Giá video bị trừ lúc tạo tác vụ. [BTC-07, BTC-08] |

**Quyết định vận hành:** luyện bằng tài khoản cá nhân có thể giúp học công cụ, nhưng khi thi dùng đúng provider/key và công cụ BTC cho phép. Nếu key BTC hết hạn, báo BTC; chỉ đổi sang API cá nhân trong ca thi khi có chấp thuận rõ ràng. File này không triển khai hay gọi thử API có tính phí.

**Tra nhanh:**

| Plan | Khi gặp đề | Bản đủ đầu tiên |
| --- | --- | --- |
| [1] | Website, web app, công cụ AI | Link mở được và hoàn thành luồng chính |
| [2] | Game giáo dục | Một lượt chơi trọn vẹn, giải thích được đáp án |
| [3] | Báo cáo dữ liệu/tài chính | Số đã đối chiếu, biểu đồ và bản PDF/DOCX đọc được |
| [4] | Infographic pháp luật/chính sách | Đúng nội dung, nguồn, kích thước |
| [5] | Truyện tranh | Đủ khung, nhân vật nhất quán, thoại đọc rõ |
| [6] | Bản tin, quảng cáo, phim ngắn | File video có hình, giọng, phụ đề theo đề |
| [7] | Tờ gấp truyền thông | Hai mặt đúng thứ tự, đọc được sau khi gấp |
| [8] | Podcast | File âm thanh hoàn chỉnh, rõ lời, đúng thời lượng |
| [9] | Bài hát | Audio hát rõ, đúng chủ đề, có lời đối chiếu |
| [10] | Chiến dịch đa định dạng | Đủ từng sản phẩm đề yêu cầu, cùng một thông điệp |

## Nguồn đối chiếu

Các nguồn BTC dưới đây đã đọc ngày 05/10/2026. Chỉ dùng chúng cho các thông tin ghi rõ đã đối chiếu trong phần này; thông báo riêng gửi đội và đề chính thức có thể bổ sung yêu cầu. PDF training dẫn trong tài liệu cũ chưa đọc được ở lần đối chiếu này.

| Mã | Nguồn | Dùng để đối chiếu |
| --- | --- | --- |
| BTC-01 | [Quy định & Hướng dẫn kỹ thuật](https://docs.thucchien.ai/docs/round-2/regulations-and-technical-guidelines) | Thiết bị/không gian giám sát, 10 phút nộp, thành phần và cách chấm công khai |
| BTC-02 | [Cấu hình AI Log](https://docs.thucchien.ai/docs/round-2/ai-log-guide) | Hook, event, gửi log, bí mật và lỗi thường gặp |
| BTC-03 | [Bảng giá model](https://docs.thucchien.ai/docs/round-2/user-guide/pricing) | Tên model, chi phí tham khảo và cách theo dõi |
| BTC-04 | [Giới hạn tốc độ](https://docs.thucchien.ai/docs/round-2/user-guide/rate-limits) | Budget 50 USD, bộ đếm đội, trần đồng thời, 429 |
| BTC-05 | [VibeCoding Best Practices](https://docs.thucchien.ai/docs/round-2/vibe-coding/best-practices) | AGENTS.md, task nhỏ, kiểm tra, duyệt diff, bí mật |
| BTC-06 | [Tích hợp Codex](https://docs.thucchien.ai/docs/round-2/vibe-coding/codex-integration) | Provider Gateway, Responses và công cụ agent |
| BTC-07 | [Sinh hình ảnh](https://docs.thucchien.ai/docs/round-2/user-guide/image-generation) | Model ảnh, tham chiếu/cơ chế sinh và đầu ra |
| BTC-08 | [Sinh video Veo](https://docs.thucchien.ai/docs/round-2/user-guide/video-generation-veo3) | Tạo → theo dõi → tải; tính phí tác vụ |
| BTC-09 | [Text-to-Speech](https://docs.thucchien.ai/docs/round-2/user-guide/text-to-speech) | Model TTS, voice và endpoint |

**Tài liệu đội cung cấp:** “Chiến lược Vòng Chung khảo” làm nền cho nhóm đề, thời gian và chiến thuật; “Bộ prompt và phong cách” làm nền cho prompt nội dung/style/xuất file; “Harness agent” làm nền cho PM/worker/reviewer và task card. README của ZIP `aitc2026-team-966-medmeetai-main` xác định vai thành viên và nơi đặt bài vòng này. Phần plan là đề xuất triển khai mới, không phải barem chấm do BTC công bố.
