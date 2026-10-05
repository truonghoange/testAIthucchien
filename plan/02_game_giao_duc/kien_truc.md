# Kiến trúc chương trình — Game giáo dục

[Mục lục plan](../README.md) · [Plan này](README.md) · [Điều hành chung](../_chung/README.md)

Các file dưới đây là cấu trúc chương trình dự kiến khi làm đề này. Folder `plan/` chỉ chứa tài liệu. Không cần tạo module tùy chọn nếu đề không dùng tới.

## Thành phần

| Thành phần | Hợp đồng | Owner |
| --- | --- | --- |
| `data/questions.json` | `id, prompt, choices, correct_id, explanation, source_id` | Hoàng ghi, Thành duyệt |
| `src/game/logic.js` | Trạng thái, điểm và điều kiện kết thúc | Worker 1 |
| `src/game/ui.js`, CSS | Nút/chạm, màn chơi/kết quả | Worker 2 |
| `assets/` và manifest | Sprite, icon, âm tùy chọn | Hoàng |

Game quiz đơn giản dùng DOM/Canvas; chỉ dùng Phaser nếu đã luyện hoặc cơ chế cần scene/sprite. Game không gọi LLM để quyết định đúng sai lúc chơi nếu đề không bắt buộc.

## Cấu trúc file chương trình

| Đường dẫn dưới chung-khao/ | Trách nhiệm | Đọc/phụ thuộc | Owner |
| --- | --- | --- | --- |
| `src/main.js` | Khởi tạo game | logic.js; ui.js | Đức |
| `src/game/logic.js` | State machine, điểm, khóa input, kết thúc | questions.json | Worker code 1 |
| `src/game/ui.js` | Start/play/feedback/result/restart; điều khiển chạm | State do logic trả về | Worker code 2 |
| `src/game/fx.js` | Phản hồi hình/âm, nút tắt âm | Sự kiện đúng/sai/thắng | Worker code 2; sau bản đủ |
| `data/questions.json` | Câu hỏi, đáp án và giải thích có nguồn | Nguồn kiến thức duyệt | Hoàng; Thành duyệt |
| `assets/` | Sprite/icon; thiếu hình dùng hình đơn giản | Style duyệt | Hoàng |
| `src/styles.css` | Bố cục màn và vùng chạm | Thiết kế UI | Worker code 2 |
| `package.json` | Build/deploy; Phaser chỉ khi cơ chế cần | Stack đã luyện | Đức |

## Hợp đồng dữ liệu

Ví dụ schema cho `data/questions.json`. Giá trị trong ngoặc vuông là trường thay thế, không phải dữ kiện thật. `null` nghĩa là chưa có thông tin; không mặc định đó là số không. Khi chốt spec, điền dữ liệu thật và ghi rõ trường bắt buộc.

```json
[
  {
    "id": "Q01",
    "prompt": "[TÌNH HUỐNG]",
    "choices": [
      {
        "id": "A",
        "text": "[LỰA CHỌN A]"
      },
      {
        "id": "B",
        "text": "[LỰA CHỌN B]"
      }
    ],
    "correct_id": "A",
    "explanation": "[GIẢI THÍCH ĐÃ DUYỆT]",
    "source_id": "SRC-01"
  }
]
```

## Quy tắc giữa các module

- State: start → playing → feedback → result → restart.
- Chỉ logic.js quyết định điểm/đáp án; UI không tăng điểm độc lập.
- Câu hỏi có correct_id hợp lệ, đúng một đáp án và giải thích khớp.

## Chia task không đè file

Đức khóa schema và chia owner trước. Worker chỉ sửa file trong task; không tự thay dữ liệu đã duyệt. Nếu đổi schema, người tích hợp báo cả hai nhánh trước khi merge. Task 10–15 phút, có input/output và cách kiểm. Nội dung chờ duyệt thì worker tiếp tục dựng khung bằng dữ liệu minh họa có nhãn.

`AGENTS.md`, `requirements.json`, `sources.md`, `prompts/`, `assets/manifest.json`, `qa/` và `submission.md` dùng theo [harness chung](../_chung/01_harness.md). Hook BTC vẫn ở gốc repo; không chuyển vào thư mục plan.
