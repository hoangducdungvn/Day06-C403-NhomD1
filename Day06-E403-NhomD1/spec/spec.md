# SPEC sản phẩm

---

## 1. Bằng chứng

- **Trải nghiệm trực tiếp** — chính nhóm trải nghiệm trên LMS của trường và khi cần tra khái niệm trong slide thì phải bật tab khác ra ngoài để tìm câu trả lời ==> mất time tầm 20s
- **Nguồn từ bên ngoài nhóm** — Phỏng vấn nhanh bạn Minh Hiếu: 1 người làm trái ngành IT cũng thấy lúng túng khi gặp các định nghĩa phức tạp, cần tra lập tức để follow bài giảng

.

## 2. Lát cắt để build

Cho học viên khoá AI thực chiến đang đọc slide bài giảng, prototype dùng AI để augment bước tạo analogy cá nhân hóa:


## 3. AI Product Canvas

Canvas là một trang giúp sản phẩm không trôi ngược về "một demo cho vui". Nhóm trả lời lần lượt bốn ô:

| Ô | Câu hỏi cần trả lời |
|---|---------------------|
| **Value** — Giá trị |  Sản phẩm dành cho học viên khóa học AI thực chiến, đau khi cần tra cứu các khái niệm lập tức mà vẫn cần bám sát bài giảng |
| **Trust** — Niềm tin | Khi AI trả lời sai, người dùng nhận ra bằng cách nào, và họ sửa lại, hoàn tác hay chuyển sang người thật ra sao? |
| **Feasibility** — Tính khả thi | Có đáng để build không? Hãy cân nhắc chi phí mỗi lượt gọi, độ trễ, dữ liệu cần có, rủi ro lớn nhất, và ngưỡng mà nhóm sẵn sàng dừng lại. |
| **Tín hiệu học** | Khi người dùng chỉnh sửa kết quả, dữ liệu đó đi về đâu và giúp sản phẩm khá lên nhờ tín hiệu nào? |

## 4. Tăng năng lực hay tự động hóa

Tăng năng lực: Analogy về khái niệm kỹ thuật có thể bỏ sót thành phần quan trọng mà user không nhận ra ngay. Cần user tự kiểm tra bảng mapping trước khi "tin" vào analogy. AI là công cụ tạo cầu nối, user là người chịu trách nhiệm học và kiểm chứng.

Human role: reviewer — đọc analogy, kiểm tra bảng mapping, tự đánh giá có hiểu hơn không, quyết định dùng lại hay sửa input.

## 5. Bốn đường đi của trải nghiệm

| Đường đi | Câu hỏi | Ví dụ cách xử lý |
|----------|---------|------------------|
| **Đường thuận** | User nhập khái niệm rõ (VD: "Embedding") + sở thích cụ thể (VD: "bóng đá")  |  AI sinh analogy narrative đầy đủ + bảng mapping rõ ràng → User đọc, hiểu, hài lòng. |
| **Khi AI không chắc** | User nhập sở thích quá chung chung ("thể thao") |  AI detect và hỏi lại "Bạn thích môn nào cụ thể?" → User bổ sung → AI sinh analogy tốt hơn. |
| **Khi AI sai** | AI không nhận ra khái niệm user nhập (VD: 12314343) | AI báo không nhận ra + gợi ý khái niệm gần nhất. Hoặc: confidence < 60% → hiện fallback card với lý do cụ thể + 3 gợi ý sửa prompt. |
| **Khi người dùng sửa** | User đọc analogy, thấy bảng mapping bỏ sót thành phần quan trọng | User sửa lại input hoặc thêm yêu cầu → AI regenerate analogy có mapping đủ hơn. |

## 6. Những kiểu lỗi đáng lo nhất

AI sinh analogy nghe hay nhưng bỏ sót chiều vector space của Embedding -> Không giải thích đúng thuật ngữ → User hiểu sai mà nghĩ mình hiểu đúng → Dạng hallucination "nghe hợp lý" — nguy hiểm nhất.


## 7. Kế hoạch kiểm thử và bằng chứng demo

Nếu user đọc analogy narrative nghe hay và không kiểm tra bảng mapping,
AI có thể đã bỏ sót thành phần kỹ thuật quan trọng (VD: chiều vector space
trong Embedding) mà không ai nhận ra,
hậu quả là user hiểu sai khái niệm mà nghĩ mình đã hiểu đúng —
đây là dạng hallucination nguy hiểm nhất vì "nghe hợp lý".

Prototype sẽ xử lý bằng: luôn hiển thị bảng mapping rõ ràng kèm analogy,
kèm ghi chú "Kiểm tra xem AI đã map đủ thành phần chưa trước khi dùng".
Fallback card khi confidence < 60%.

Owner kiểm thử path này là: [tên thành viên phụ trách test/failure path].

## 8. Phân công

Dũng: giữ repo, evidence, slide
Phú: Code FE
Khôi: Code BE
Vinh: Code AI core
Kiên: Viết system prompt