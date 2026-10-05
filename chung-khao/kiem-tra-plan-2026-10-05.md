# Rà soát plan chuẩn bị chung khảo — 05/10/2026

**Kết luận:** hướng chuẩn bị MCP, skill, base, harness và prompt phù hợp với thông tin training đội cung cấp. Chưa thấy kiến trúc của 10 plan bắt buộc gọi AI ngoài BTC. Tuy nhiên repo hiện chưa đủ bằng chứng để xác nhận sẵn sàng thi: launcher Python của hook thất bại, chưa có base chạy được, checklist thiếu hồ sơ ghi hình, và tài liệu vòng đang nằm ngoài thư mục quy định.

Đã rà bộ 68 tệp Markdown trong `plan/`, README repo/vòng, cấu hình hook và các script logging liên quan. Các nhận xét về thời gian và chất lượng là đánh giá kỹ thuật của đội, không phải barem của BTC.

**Căn cứ và giới hạn đối chiếu**

- Website [docs.thucchien.ai](https://docs.thucchien.ai/) và các trang chuyên biệt liên kết bên dưới: đã đọc ngày 05/10/2026.
- Training ngày 04/10/2026: theo thông tin người dùng, được chuẩn bị MCP/skill/base trước, dùng harness, Google Search và push liên tục; khi thi chỉ dùng nguồn AI BTC cho phép. Đây là thông tin đội cung cấp, chưa phải trích dẫn từ slide.
- [Hướng dẫn kỹ thuật – Vòng Chung Khảo.pdf](https://drive.google.com/file/d/1o2GLu2peUeruIq3zD8oUDHURpyrL83YU/view): đã xác minh tên/MIME PDF qua metadata; nội dung trả 403 và tải file bị từ chối cho tài khoản kết nối. Chưa đọc được PDF, chưa xác nhận các chi tiết chỉ có trong tài liệu này.
- Việc thiếu cấu hình provider trong repo không chứng minh máy đang dùng sai provider: cấu hình cá nhân ngoài repo chưa được kiểm tra. Các API trả phí, endpoint đọc log và tài khoản Suno chưa được gọi thử trong lần rà soát.

**Phần nào được chuẩn bị và sử dụng?**

| Hạng mục | Đánh giá | Điều kiện thực hiện |
| --- | --- | --- |
| Prompt, skill, khung source, template xuất file | Phù hợp thông tin training | Lưu nguồn và phiên bản chuẩn bị; nhận đề rồi điền yêu cầu thực tế |
| MCP tự thiết kế | Phù hợp thông tin training | Mọi chức năng có suy luận/sinh nội dung phải đi nguồn AI BTC cho phép; kiểm cả dịch vụ bên trong MCP |
| Harness, PM/worker/reviewer, nhiều agent | Có thể dùng | Chọn provider BTC cho từng agent, kể cả worker/reviewer và retry |
| Tìm kiếm Google thông thường | Được theo training đội cung cấp | Trích nguồn; phân biệt kết quả tìm kiếm với dịch vụ trả lời bằng AI |
| Tìm kiếm có AI/grounding | BTC có hỗ trợ | Dùng cơ chế grounding/search tại Gateway và giữ nguồn trả về. [Hướng dẫn search](https://docs.thucchien.ai/docs/round-2/user-guide/google-search-grounding) |
| Commit/push liên tục | Được theo training; phù hợp quy trình log | Một người tích hợp, commit nhỏ, kiểm việc gửi log ở các mốc bàn giao |
| Python/Node/FFmpeg, HTML/CSS, phép tính, render, Git | Công cụ xử lý thông thường trong các plan | Rà plugin/bộ lọc để biết có gọi AI ngầm hay không |
| ChatGPT/Gemini/Claude web hoặc API cá nhân trong ca thi | Không phù hợp giới hạn Gateway | File hướng dẫn logging có nhắc các công cụ này không phải căn cứ cho phép sử dụng chúng. [Quy định AI Log](https://docs.thucchien.ai/docs/round-2/ai-log-guide) |
| Suno bằng tài khoản BTC cấp | Có hướng dẫn chính thức riêng | Dùng đúng tài khoản BTC; kiểm login/quota/tải file. Đây là luồng ngoài Gateway được BTC hướng dẫn. [Suno BTC](https://docs.thucchien.ai/docs/round-2/suno-login-guidelines) |
| AI local hoặc dịch vụ OCR/STT/embedding/ảnh phụ trợ bên ngoài | Không được tự coi là hợp lệ | Theo giới hạn training, chuyển chức năng AI sang BTC; thư viện xử lý thông thường xét theo chức năng thực tế |

“Dùng được mọi công cụ” vẫn đi kèm yêu cầu về giám sát, log, nguồn và quyền sử dụng tài nguyên. Điều lệ Điều 7.7 giới hạn dữ liệu/tài nguyên ngoài danh mục được phép; tài nguyên ngoài phạm vi đó cần khai báo và chấp thuận bằng văn bản. Quyền search/chuẩn bị theo training cần được ghi làm căn cứ, không tự suy ra quyền sử dụng mọi dataset hoặc asset. [Điều lệ](https://thucchien.ai/the-le-cuoc-thi/)

**Các phát hiện cần xử lý theo thứ tự**

P0 là việc phải xử lý trước ca thi; P1 ảnh hưởng khả năng hoàn thành; P2 là cải thiện vận hành.

| Mức | Phát hiện và bằng chứng | Việc cần làm |
| --- | --- | --- |
| P0 | `.env.example:12` chứa giá trị giống token AI Log thật; file được Git theo dõi. Giá trị đã bị xuất ra khi đọc file mẫu trong lần rà soát này | Xác minh với đội/BTC. Nếu là token thật, thu hồi/cấp lại và thay bản mẫu bằng placeholder; thay file hiện tại không thu hồi token trong lịch sử. Không lặp lại giá trị trong báo cáo |
| P0 | `py -3 --version` báo `No installed Python found!`; Git Bash chạy `scripts/_pyrun.sh --version` thất bại với exit 112 | Cài hoặc cấu hình Python >=3.10 cho đúng môi trường hook trên cả hai máy; kiểm thêm `python-dotenv`. Đây là lỗi đã tái hiện trong shell hiện tại |
| P0 | `.ai-log/` hiện chỉ có `.gitkeep`; pre-push tồn tại nhưng bỏ qua lỗi bằng `|| true` | Diễn tập một phiên thật và đọc lại log đã gửi. Thư mục trống không chứng minh server không có log; push thành công không chứng minh gửi log thành công |
| P0 | Chưa có adapter/log được kiểm chứng cho harness/MCP tự viết; `plan/_chung/01_harness.md:38` mới mô tả log bổ sung | Kiểm event thật của công cụ được chọn. Logger phụ trong `chung-khao/logs/` cần có đường gửi tới BTC nếu dùng làm nguồn event cho harness |
| P0 | `plan/_chung/05_qa_nop_bai.md:5` thiếu video ghi hình cả buổi thi và checklist hai điện thoại | Bổ sung người phụ trách quay, dung lượng, sạc, kiểm file, link tải và biên nhận; tách video giám sát khỏi video thuyết trình |
| P1 | `plan/` đang ở gốc; `chung-khao/README.md:7` yêu cầu tài liệu vòng ở `chung-khao/` | Đưa bộ tài liệu vòng vào `chung-khao/plan/`, sửa liên kết nếu cần; bộ hook dùng chung vẫn ở gốc |
| P1 | `plan/README.md:43,45` và `plan/_chung/04_quy_dinh_nguon.md:7` còn ghi quyền chuẩn bị chưa rõ | Cập nhật căn cứ training người dùng vừa cung cấp; giữ các thông số chưa đọc được PDF ở trạng thái chưa xác minh |
| P1 | `chung-khao/AGENTS.md`, base, MCP, source sản phẩm và script media chưa có; `plan/README.md:43` cũng nói đây chỉ là cấu trúc dự kiến | Chuẩn bị bộ khung và chạy thử trước thi. Chưa có mã không phải vi phạm, nhưng chưa đạt mục tiêu tận dụng quyền chuẩn bị trước |
| P1 | `plan/_chung/01_harness.md:36` đề xuất sáu request đồng thời; key test chỉ cho năm | Cấu hình riêng test/official, đặt mặc định test <=4; có giới hạn RPM/TPM và semaphore cho từng key |
| P1 | Không tìm thấy `ffmpeg`/`ffprobe` trên PATH hiện tại; nhiều plan cần export/mix/render | Chốt dependency, font tiếng Việt và chạy mẫu xuất PDF/PNG/MP3/MP4 trên cả hai máy. Chưa kết luận các chương trình này không được cài ở vị trí khác |
| P1 | Video có trần USD nhưng chưa lượng hóa số clip, giây, độ phân giải và retry | Chốt storyboard theo chi phí; lưu job ID để tiếp tục poll/download thay vì tạo lại tác vụ khi timeout |
| P2 | Lịch dùng chung chỉ nhắc push/gửi log rõ ở T+100–120 | Thêm nhịp commit/push sau bàn giao hoặc mỗi 10–15 phút; kiểm tình trạng log trước T+100 |
| P2 | Hướng dẫn worker cấm sửa hook quá rộng khi áp dụng cho task chuẩn bị harness | Giữ cấm can thiệp nội dung log; cho phép task có phạm vi rõ để sửa lỗi/thêm tích hợp. Website BTC cho phép chỉnh script/hook với event đầy đủ, đúng thật |

`AI-LOG.md:76` và `.agents/workflows/log.md` nhắc log thủ công cho web AI. `scripts/log_manual.py:90` tạo `ManualLog`; không dùng cách này để thay toàn bộ event prompt/tool/kết thúc phiên của harness.

BTC yêu cầu log thật và cho phép bổ sung tích hợp, đổi lịch gửi hoặc sửa lỗi script. Một phép thử đạt nên có prompt, tool, kết thúc lượt; gửi thành công rồi đọc lại trên [API log của BTC](https://docs.thucchien.ai/docs/round-2/api-reference/ai-log-entries). [Quy định logging](https://docs.thucchien.ai/docs/round-2/ai-log-guide)

**Các yêu cầu giám sát cần đưa vào checklist**

Ba thành viên, hai máy tính; không có người thứ tư. Hai điện thoại cố định, quay ngang, sạc liên tục: máy 1 quay offline ở chế độ máy bay, tối thiểu Full HD MP4/MOV; máy 2 truyền trực tiếp, tắt thông báo/khóa màn hình. Kiểm góc máy bằng đoạn quay thử. Video máy 1 là thành phần nộp bắt buộc; link phải cho tải. Có 10 phút nộp sau thời gian làm bài. [Quy định kỹ thuật vòng chung khảo](https://docs.thucchien.ai/docs/round-2/regulations-and-technical-guidelines)

Đề xuất riêng của đội: tính trước dung lượng video và thời gian upload theo băng thông thực; diễn tập cả thao tác lấy file điện thoại. Không mặc định video dài cả ca có thể truyền xong trong vài phút.

**Rà 10 dạng đề**

| Plan | Phần hợp lý đang có | Phần nên chuẩn bị trước |
| --- | --- | --- |
| 01 Website/webapp | Frontend gọi serverless, key phía server, kết quả được kiểm | Base deploy được; route API BTC; kiểm link bằng trình duyệt khác; cấu hình lỗi/timeout |
| 02 Game giáo dục | Luồng chơi trọn vẹn, giải thích và chơi lại | Base game có state/score/restart; mẫu dữ liệu; thao tác bàn phím/cảm ứng và bài kiểm luồng |
| 03 Báo cáo dữ liệu | Code tính số, chart cùng nguồn, nhận định trỏ metric | Bộ nhập dữ liệu và công thức mẫu; xử lý số thiếu/đơn vị; renderer đúng loại file |
| 04 Infographic | Nội dung có nguồn, bố cục và chữ tách khỏi ảnh AI | Template đúng viewport/khổ, font tiếng Việt, xuất PNG/PDF và kiểm tràn chữ |
| 05 Truyện tranh | Nhân vật tham chiếu, ảnh không chữ, layout thoại riêng | Thử đường gửi ảnh tham chiếu thật qua BTC; template panel/bóng thoại; kiểm nhất quán nhiều cảnh |
| 06 Video | Lưu job ID, timing từ audio thực, lắp ghép và QA | Queue có resume, giới hạn retry, FFmpeg preset, subtitle, mẫu render cả pipeline |
| 07 Tờ gấp | Hai mặt và thứ tự gấp được quan tâm | Base ba panel mỗi mặt, thử gấp bản preview/in; khóa page size/margin/font |
| 08 Podcast | TTS từng đoạn, manifest có duration, nghe toàn bộ | Map voice/model đã thử tiếng Việt; nối/mix âm; đo mức âm và chuẩn codec |
| 09 Bài hát | Dùng Suno BTC riêng, giữ audio hát và lời đối chiếu | Kiểm tài khoản/quota/tải file sớm; quy tắc chọn bản và sửa từ sai. TTS chưa đáp ứng yêu cầu hát |
| 10 Chiến dịch | Dùng chung thông điệp/style, ma trận đầu ra | Bộ template có cùng token thiết kế; kiểm đủ từng deliverable; budget chung giữa các nhánh |

Các fallback hiện đều có điều kiện giữ yêu cầu bắt buộc. Chưa thấy fallback nào cho phép tự bỏ thành phần đề yêu cầu. Các mẫu “6 khung”, “3 biểu đồ”, “90 giây” là cấu hình luyện tập; cần thay theo đề.

**Các điểm kỹ thuật cần khóa vào base**

Các model `gpt-6.1-sol`, `gpt-6-luna`, `nano-banana-2-lite` và Veo Lite trong plan có trong tài liệu BTC. Chọn model theo vai là hợp lý; nên ghi rõ model TTS/Flash thay cho tên họ model chung chung. [Bảng giá](https://docs.thucchien.ai/docs/round-2/user-guide/pricing)

| Chức năng | Điểm cần khóa | Nguồn |
| --- | --- | --- |
| Coding agent | Provider BTC, base `https://api.thucchien.ai/v1`, giao thức Responses; không dùng tên model làm bằng chứng duy nhất về provider | [Codex qua BTC](https://docs.thucchien.ai/docs/round-2/vibe-coding/codex-integration) |
| Harness khác | DeepSeek Harness dùng custom Responses; Hermes Chat Completions có hạn chế GPT-6 gọi tool, cần chọn model/protocol phù hợp | [DeepSeek Harness](https://docs.thucchien.ai/docs/round-2/vibe-coding/deepseek-harness-integration), [Hermes](https://docs.thucchien.ai/docs/round-2/vibe-coding/hermes-agent-integration) |
| GPT-6 trực tiếp | Chat dùng `max_completion_tokens`; Responses dùng `max_output_tokens`; mức reasoning phải phù hợp model | [Tham số model](https://docs.thucchien.ai/docs/round-2/user-guide/openai-deepseek) |
| Ảnh | Nano Banana nhận `n=1`, dùng `aspect_ratio`, giải mã base64; thử reference trước. Tránh alias cũ `nano-banana` đã được tài liệu báo ngừng hỗ trợ | [Sinh ảnh](https://docs.thucchien.ai/docs/round-2/user-guide/image-generation) |
| Video | `/v1/videos` → trạng thái theo ID → tải content; có deadline và lưu trạng thái khi restart | [Veo](https://docs.thucchien.ai/docs/round-2/user-guide/video-generation-veo3) |
| TTS/STT | `/audio/speech`; STT upload multipart vào `/audio/transcriptions`; nghe/đọc kiểm đầu ra thật | [TTS](https://docs.thucchien.ai/docs/round-2/user-guide/text-to-speech), [STT](https://docs.thucchien.ai/docs/round-2/user-guide/speech-to-text) |
| Search | Gemini dùng `googleSearch`; OpenAI dùng `web_search` qua Responses; giữ metadata/nguồn | [Search](https://docs.thucchien.ai/docs/round-2/user-guide/google-search-grounding) |
| Embedding nếu đề cần RAG | Cùng model cho index/query; `gemini-embedding-2` phải gọi từng đoạn riêng | [Embedding](https://docs.thucchien.ai/docs/round-2/user-guide/embeddings) |
| Budget | `/key/info` cho chi tiêu riêng key; lấy `team_id` rồi `/team/info` để xem tổng đội; `/v1/models` để kiểm model thực được cấp | [Chi tiêu](https://docs.thucchien.ai/docs/round-2/api-reference/spend-checking) |

Budget chính thức là 50 USD chung đội; test là 1 USD. Đồng thời mỗi key: chính thức 10, test 5; RPM/TPM dùng chung đội và còn giới hạn theo model. Giữ chỗ token phụ thuộc giới hạn output đã yêu cầu. Lỗi hết budget không giải quyết bằng chờ/retry. [Rate limits](https://docs.thucchien.ai/docs/round-2/user-guide/rate-limits)

Ví dụ tính riêng để chốt plan video: 12 clip × 8 giây = 96 giây nguồn. Theo giá 720p đã đọc, một lượt sinh toàn bộ có chi phí Lite 4,80 USD, Fast 9,60 USD, bản thường 38,40 USD. Hai lượt Fast là 19,20 USD. Đây là phép tính ước lượng, chưa gồm chi phí LLM/ảnh/TTS và không bảo đảm đủ 90 giây sau khi cắt dựng. Trần video 24 USD hiện tại cần đi kèm giới hạn scene/model/retry. [Giá Veo](https://docs.thucchien.ai/docs/round-2/user-guide/pricing)

**Bộ chuẩn bị trước nên có**

Không cần dựng mười ứng dụng riêng. Có thể chuẩn bị bốn nhóm base tái sử dụng: web/game; dữ liệu/báo cáo; ấn phẩm HTML; audio/video, cộng lớp API và logging chung.

| Thành phần | Điều kiện được coi là chuẩn bị xong |
| --- | --- |
| Tài liệu và skill | Agent đọc được hướng dẫn gốc và `chung-khao/AGENTS.md`; skill gọi đúng script BTC, không kích hoạt AI khác |
| Client API chung | Không chứa key; rõ provider/model/endpoint; timeout; lỗi 401/429/5xx; kiểm schema đầu ra |
| MCP tối thiểu | Các tool cần dùng có input/output rõ; AI qua BTC; lưu asset theo ID; lưu event thật; chạy thử từ client harness |
| Harness | Task có owner/path; worker không đụng cùng file; PM/reviewer cũng dùng BTC; task lỗi có điểm dừng |
| Logger | Đủ event thật, gửi được và đọc lại được; hai máy có danh tính phiên riêng; không chứa token |
| Queue media | Giới hạn phù hợp key; budget chung; job ID persist; resume; không tự tạo lại job tính phí khi mất kết nối |
| Render/export | Mẫu PDF/PNG/MP3/MP4 mở được; chữ Việt đủ dấu; đúng khổ/codec; asset/font có căn cứ sử dụng |
| Nộp bài | Requirements → artifact/link; commit đã nộp; checksum nếu cần; video giám sát/link tải; xác nhận tiếp nhận |

Đề xuất thứ tự làm trước ngày thi:

1. Xử lý token bản mẫu và sửa môi trường Python/hook; kiểm provider/log trên cả hai máy.
2. Ghi lại căn cứ training, chuyển tài liệu vòng về đúng thư mục, thêm hướng dẫn agent.
3. Dựng client/queue/logging và MCP cho các thao tác thực sự cần; chạy một luồng end-to-end.
4. Chuẩn bị bốn nhóm renderer/base và đầu vào minh họa có nhãn, thay được bằng dữ liệu đề.
5. Diễn tập hai máy, ba người theo thời lượng đề; chốt bản đủ, review, push/log và nộp cả video giám sát.

Ghi commit chuẩn bị trước khi bắt đầu ca; lưu đề/spec và commit cuối của bài thi. Cách này giúp trình bày rõ phần tái sử dụng và phần được đội xây theo đề.

**Các điểm còn cần PDF/thông báo ca thi**

Chưa xác nhận từ văn bản đã đọc: 120 phút làm bài; giới hạn 20 file/500 MB; video thuyết trình 3–6 phút trong 24 giờ; lịch thi cụ thể, cổng nộp và trọng số chấm. Không dùng các con số này như quy định chính thức trước khi đọc được PDF/đề. Quyền chuẩn bị trước được dùng làm căn cứ vận hành theo lời training người dùng cung cấp; cần bổ sung vị trí trang/slide khi có nội dung tài liệu.

Bản rà soát này bổ sung bằng chứng và danh sách việc cần làm. Các plan, hook, token và lịch sử Git chưa được chỉnh sửa; chưa commit/push hoặc gửi log lên BTC trong lần rà soát.
