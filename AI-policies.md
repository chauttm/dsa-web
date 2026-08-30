# Mục tiêu của môn học Cấu trúc dữ liệu và giải thuật
Giá trị của người có kiến thức về Cấu trúc dữ liệu và giải thuật không còn nằm ở việc nhớ cú pháp và cài đặt cấu trúc dữ liệu và thuật toán, mà nằm ở **tư duy thuật toán, khả năng lựa chọn công cụ phù hợp để giải quyết bài toán hiệu quả nhất**. Các bạn cần hướng đến việc trở thành một **kiến trúc sư giải pháp** - người làm chủ, điều khiển và thẩm định AI, chứ không phải là người bắt chước AI.

# Chính sách sử dụng AI

**AI** (*chính xác hơn là các Mô hình ngôn ngữ lớn - LLM*) là công cụ vô cùng hữu ích, nhưng chúng cũng có thể trở thành một "chiếc nạng" khiến bạn ỷ lại. Chúng tôi muốn khuyến khích bạn sử dụng LLM một cách hiệu quả như một công cụ hỗ trợ học tập, đồng thời vẫn tạo động lực để bạn tự mình nắm vững kiến thức sau cùng.

**Đôi dòng ngoài lề:** *Tại sao bạn phải tự học kiến thức nếu LLM có thể làm thay phần lớn?* Hiện tại, LLM vẫn chưa thể thiết kế và phân tích thuật toán tốt như những chuyên gia ở trình độ cao nhất, và điều này có lẽ sẽ không thay đổi trong tương lai gần (hãy nhớ rằng con người sẽ càng mạnh mẽ hơn khi công cụ của chúng ta mạnh mẽ hơn). Nếu bạn muốn trở thành một người có kỹ năng thuật toán cao, bạn cần học những điều cơ bản để có thể vượt xa LLM (có thể bằng cách sử dụng chính LLM). Ngoài ra, trong ngắn hạn, LLM vẫn mắc sai lầm, và nếu bạn nộp một bài làm "rác AI" đầy lỗi, bạn sẽ nhận điểm kém.

Với tinh thần đó, chính sách của lớp học như sau:

* **Vi phạm quy tắc liêm chính học thuật (Honor Code):** Việc sao chép và dán kết quả từ LLM vào bài tập về nhà là vi phạm quy tắc liêm chính, tương tự như việc sao chép bài làm của nhóm khác. Mọi nội dung bạn nộp phải được viết bằng ngôn ngữ của chính nhóm bạn.
* **Ngoại lệ:** Bạn được phép sử dụng LLM để chỉnh sửa cú pháp và từ ngữ trong các bài tập (ngay cả khi việc đó bao gồm sao chép và dán kết quả từ LLM), miễn là nó không tạo ra hoặc thay đổi nội dung cốt lõi trong lời giải của bạn.

Việc sử dụng LLM để hỗ trợ lên ý tưởng (brainstorm) cho bài tập về nhà là được phép. Tuy nhiên, chúng tôi khuyến khích bạn hãy cân nhắc kỹ khi sử dụng và dùng chúng theo cách hỗ trợ tốt nhất cho việc học. Các phương pháp tối ưu bao gồm:

* **Tự suy nghĩ trước:** Hãy tự mình (hoặc cùng nhóm) suy nghĩ về bài toán trước khi bắt đầu hỏi LLM, giống như cách bạn nên động não trước khi đến giờ chữa bài tập.
* **Hỏi gợi ý, không hỏi đáp án:** Nếu bạn bị tắc và định tìm đến LLM, hãy yêu cầu nó đưa ra một **gợi ý (hint)** thay vì đáp án. Bạn có thể bắt đầu bằng cách yêu cầu một "gợi ý tối thiểu".
* **Giải bài toán tương tự:** Yêu cầu LLM đặt ra và giải một bài toán **tương tự**, hoặc yêu cầu nó đưa ra một bài toán "khởi động" dễ hơn để bạn làm quen.
* **Tìm lỗi sai (Debugging):** Một cách thú vị khác để học từ LLM là yêu cầu nó đưa ra một câu trả lời **sai** cho bài toán để bạn có thể tìm ra lỗi sai. Đây là một cách tuyệt vời để hiểu sâu về bài toán! Có lẽ sau đó, bạn sẽ có thể tự mình tìm ra đáp án đúng.

**Trong các kỳ thi:** LLM hoàn toàn không được phép sử dụng. Các kỳ thi chính là động lực để bạn sử dụng LLM theo cách **giúp bạn học** thay vì **học hộ bạn** — có lẽ bằng cách áp dụng một số gợi ý của chúng tôi ở trên.

# Hướng dẫn viết prompt để tự học

Để có thể tự luyện tập theo phương pháp **Bug Hunting (Sửa lỗi ngầm)** và nâng cao tư duy phản biện, các bạn cần biết cách ra lệnh cho AI đóng vai trò là một **"Giáo viên khó tính cố tình gài bẫy"**, thay vì một công cụ giải bài hộ.

Dưới đây là các mẫu cấu trúc Prompt được thiết kế theo các cấp độ tăng dần để các bạn có thể copy và sử dụng trực tiếp:

---

## Cấp độ 1: Tạo bài tập Bug Hunting (Tự luyện sửa lỗi)

Thay vì xin code chuẩn, sinh viên ép AI phải sinh ra code lỗi ngầm để mình tự đi tìm.

> **Prompt mẫu:**
> *"Tôi đang học môn Cấu trúc dữ liệu và Giải thuật về chủ đề **[Tên chủ đề, ví dụ: Cây nhị phân tìm kiếm BST]**. Bạn hãy đóng vai một giảng viên đại học tinh nghịch. Hãy viết cho tôi một đoạn code bằng ngôn ngữ **[Java/Python]** triển khai tính năng **[ví dụ: xóa một nút khỏi cây]**.
> **Yêu cầu:**
> 1. Đoạn code KHÔNG ĐƯỢC CÓ LỖI CÚ PHÁP (phải biên dịch được).
> 2. Đoạn code chạy đúng với các trường hợp cơ bản (Happy Cases).
> 3. Đoạn code PHẢI CHỨA MỘT LỖI LOGIC NGẦM hoặc lỗi ở trường hợp biên (Edge Case) khiến nó chạy sai hoặc sập bộ nhớ khi gặp dữ liệu đặc biệt.
> 4. Hãy giấu đáp án đi. Chỉ cung cấp đoạn code lỗi và một gợi ý nhỏ (Hint). Khi nào tôi tìm ra hoặc bỏ cuộc, tôi sẽ hỏi đáp án sau."*
> 
> 

---

## Cấp độ 2: Kiểm thử áp lực mã nguồn (Stress Test Code của chính mình)

Khi sinh viên tự viết xong một thuật toán và muốn AI tìm xem mình có sơ hở nào không, tránh việc "bị lừa" bởi các bộ test cơ bản.

> **Prompt mẫu:**
> *"Đây là đoạn code triển khai **[Tên thuật toán, ví dụ: Thuật toán Dijkstra]** do tôi tự viết bằng **[Java/Python]**:
> **[Dán code của sinh viên vào đây]**
> Đừng khen code của tôi. Hãy đóng vai một **Chuyên gia kiểm thử phần mềm độc ác (QA/Tester)**. Hãy tìm ra ít nhất 3 trường hợp dữ liệu cực đoan (Edge Cases), dữ liệu lỗi, hoặc dữ liệu siêu lớn (Big Data) có thể làm cho đoạn code trên của tôi bị:
> * Chạy sai kết quả.
> * Bị lặp vô hạn hoặc tràn bộ nhớ (StackOverflow / OutOfMemory).
> * Chạy quá thời gian quy định (Time Limit Exceeded - TLE).
> Hãy chỉ ra các kịch bản test đó và giải thích tại sao code của tôi lại 'sập'."*
> 
> 

---

## Cấp độ 3: Đối thoại Đánh đổi (Trade-off Analysis)

Prompt này giúp sinh viên luyện tư duy của một Kiến trúc sư hệ thống – biết cách chọn cấu trúc dữ liệu dựa trên sự đánh đổi về tài nguyên.

> **Prompt mẫu:**
> *"Tôi có một bài toán thực tế như sau: **[Mô tả bài toán, ví dụ: Thiết kế hệ thống lưu lịch sử duyệt web của người dùng để tính năng 'Back' hoạt động nhanh nhất nhưng tốn ít RAM nhất]**.
> Hãy cho tôi một bảng so sánh chi tiết nếu tôi sử dụng **[Cấu trúc dữ liệu A, ví dụ: Doubly Linked List]** so với **[Cấu trúc dữ liệu B, ví dụ: Dynamic Array]** cho bài toán này.
> Phân tích kỹ về: Độ phức tạp thời gian (Time), dung lượng bộ nhớ tiêu thụ thực tế (Space), khả năng mở rộng khi dữ liệu lên tới hàng triệu phần tử, và cơ chế dọn rác (Garbage Collection) của ngôn ngữ ảnh hưởng thế nào đến hệ thống."*

---

## Cấp độ 4: Học bản chất qua mô phỏng (Visual & Intuition)

AI không thể vẽ hình động, nhưng nó có thể dùng ký tự văn bản (ASCII Art) hoặc mô tả từng bước để sinh viên xây dựng "trực giác hình học" trước khi Code.

> **Prompt mẫu:**
> *"Tôi đang mơ hồ về cách hoạt động của **[Thuật toán, ví dụ: Quay trái/Quay phải của cây AVL]**. Hãy giải thích cho tôi thuật toán này bằng cách:
> 1. Vẽ một sơ đồ bằng ký tự (ASCII Art) mô tả trạng thái của cây TRƯỚC và SAU khi quay.
> 2. Đóng vai một người hướng dẫn, giải thích từng bước sự dịch chuyển của các con trỏ bằng ngôn ngữ bình dân, dễ hiểu nhất (đừng dùng thuật ngữ học thuật phức tạp).
> 3. Cho tôi một ví dụ thực tế trong đời sống có cơ chế hoạt động tương tự như thuật toán này."*
> 
> 

---

### 💡 **"Nguyên tắc 3 không"** khi chat với AI:

1. Không xin code có sẵn ngay từ đầu.
2. Không copy-paste code của AI mà không hiểu từng dòng.
3. Không tin tưởng hoàn toàn vào câu trả lời đầu tiên của AI (luôn đặt câu hỏi *"Bạn có chắc chắn đoạn code này tối ưu nhất chưa? Hãy tự phản biện chính bạn xem"*). AI hoàn toàn có thể trả lời sai, hãy kiểm chứng bằng cách so sánh với giáo trình.
