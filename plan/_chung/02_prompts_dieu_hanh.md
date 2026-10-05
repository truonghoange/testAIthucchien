# Prompt điều hành P0–P4

[Mục lục plan](../README.md) · [Hướng dẫn chung](README.md)

**P0 — Mổ xẻ đề, trước T+8.** Thành đọc đề bằng mắt và đối chiếu kết quả AI.

```text
Phân tích đề dưới đây, chưa đề xuất sản phẩm.
Xuất bảng: ID yêu cầu | nguyên văn | bắt buộc hay tùy chọn | bằng chứng cần nộp.
Liệt kê người dùng, định dạng, số lượng, kích thước/thời lượng, hạn nộp và nguồn có sẵn.
Tách dữ kiện đề nêu khỏi giả định. Với chỗ mơ hồ, ghi cần hỏi gì và cách làm ít rủi ro.
Không tự tạo yêu cầu, số liệu hoặc tiêu chí chấm.
[ĐỀ NGUYÊN VĂN]
```

**P1 — Chốt phương án và task card, T+8–15.** Chỉ cần ba ý tưởng nếu đội chưa có hướng.

```text
Đọc chung-khao/brief.md và chung-khao/requirements.json.
Đề xuất 3 hướng giải đáp ứng đủ đề; mỗi hướng ghi lợi ích cho người dùng,
điểm khác biệt, đầu ra tối thiểu và rủi ro thời gian. Khuyến nghị 1 hướng.
Sau khi người phụ trách chốt, chia 3–6 task card, mỗi task không quá 15 phút.
Ghi file được sửa, đầu vào, đầu ra, phụ thuộc và cách kiểm tra.
Mục tiêu: bản đủ ở T+60; đóng băng tính năng/nội dung ở T+100.
Không triển khai trước khi hướng giải được chốt; không thêm thành phần ngoài đề.
```

**P2 — Giao worker.** Thay tên task và đường dẫn bằng file thật.

```text
Đọc chung-khao/AGENTS.md và chung-khao/tasks/[TASK].md.
Chỉ sửa các file được giao. Giữ schema đã chốt và nội dung đã duyệt.
Thực hiện nhiệm vụ, chạy kiểm tra trong task và sửa lỗi trong phạm vi.
Không mở/in secret, không sửa hook/log BTC, không tự deploy, commit hay push.
Nếu bị chặn, báo nguyên lỗi và file liên quan; không mở rộng kiến trúc.
Trả về tối đa 5 dòng: đã làm, file sửa, kiểm tra và vấn đề còn lại.
```

**P3 — Reviewer tại T+60/T+95.** Phần đúng sai nội dung vẫn do người phụ trách xác nhận.

```text
Đối chiếu đề, requirements.json, nguồn đã duyệt và bản sản phẩm được đưa.
Với từng ID yêu cầu: đạt/chưa đạt, bằng chứng file hoặc màn hình.
Kiểm tra nội dung sai/thiếu nguồn, lỗi luồng chính và định dạng nộp.
Chỉ liệt kê tối đa 5 lỗi chặn nộp, theo mức ưu tiên; không thêm tính năng.
Không kết luận đã xem/nghe/chạy sản phẩm nếu chưa có bằng chứng thực hiện.
```

**P4 — Chốt gói nộp, trước T+120.**

```text
Lập chung-khao/submission.md: ID yêu cầu → file/link → cách mở → trạng thái.
Kiểm tra file tồn tại, đúng loại/kích thước/thời lượng theo đề; link không cần tài khoản đội.
Ghi lệnh chạy, pipeline, model và chi phí thực đã được cung cấp vào README vòng này.
Liệt kê việc người cần kiểm cuối. Không tự nộp, không tự push, không sửa sản phẩm mới.
```
