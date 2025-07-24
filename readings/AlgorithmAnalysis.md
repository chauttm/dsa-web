# Phân tích độ phức tạp thuật toán
Khi làm việc với các chương trình giải quyết các vấn đề khó hoặc xử lý lượng lớn dữ liệu, ta chắc chắn sẽ đặt ra những câu hỏi như thế này:
Chương trình của tôi sẽ mất bao lâu để chạy?
Tại sao chương trình của tôi lại hết bộ nhớ?

Những câu hỏi này quá mơ hồ để có thể trả lời một cách chính xác, các câu trả lời phụ thuộc vào nhiều yếu tố như đặc tính của máy tính cụ thể đang được sử dụng, dữ liệu cụ thể đang được xử lý, và chương trình cụ thể đang thực hiện công việc (thực thi một thuật toán nào đó). Tất cả những yếu tố này để lại cho chúng ta một lượng thông tin khổng lồ cần phân tích.

Bất chấp những thách thức này, cách xây dựng các câu trả lời hữu ích cho những câu hỏi cơ bản này thường khá rõ ràng, như bạn sẽ thấy trong phần này. Quá trình này dựa trên *phương pháp khoa học*, là các kỹ thuật được khoa học chấp nhận rộng rãi để phát triển kiến thức về thế giới tự nhiên. Chúng ta áp dụng *phân tích toán học* để xây dựng các mô hình chi phí ngắn gọn và thực hiện các *nghiên cứu bằng thực nghiệm* để thẩm định các mô hình này.

### Phương pháp khoa học
Chính cách tiếp cận mà các nhà khoa học sử dụng để hiểu thế giới tự nhiên cũng áp dụng được cho việc tìm hiểu về thời gian chạy của các chương trình:
- *Quan sát* một đặc điểm nào đó của thế giới tự nhiên, thường là với các phép đo chính xác.
- *Đưa ra giả thuyết* là một mô hình phù hợp với các quan sát.
- *Dự đoán* các sự kiện bằng cách áp dụng giả thuyết.
- *Xác minh* các dự đoán bằng cách thực hiện các quan sát tiếp theo.
- *Thẩm định* bằng cách lặp lại quá trình cho đến khi giả thuyết khớp với các quan sát.

Một trong những nguyên tắc quan trọng của phương pháp khoa học là các thí nghiệm mà chúng ta thiết kế phải có *khả năng tái lập*, để người khác có thể tự thuyết phục về tính đúng đắn của giả thuyết. Các giả thuyết cũng phải có *khả năng bị phản chứng*, để chúng ta có thể chắc chắn khi xác định một giả thuyết là sai (và do đó cần được sửa đổi). Như một câu nói nổi tiếng được cho là của Einstein ("*Không có số lượng thí nghiệm nào là đủ để có thể chứng minh là tôi đúng; chỉ cần một thí nghiệm là có thể chứng minh tôi sai*"), chúng ta không bao giờ có thể chắc chắn rằng một giả thuyết nào đó là hoàn toàn đúng; chúng ta chỉ có thể thẩm định rằng nó nhất quán với các quan sát của chúng ta.

### Quan sát
Thách thức đầu tiên của chúng ta là quan sát định lượng: làm cách nào để đo thời gian chạy của các chương trình. Nhiệm vụ này dễ dàng hơn nhiều so với các ngành khoa học tự nhiên. Chúng ta không cần phóng tên lửa lên sao Hỏa hay giết động vật thí nghiệm hay phân rã một nguyên tử — chúng ta chỉ cần chạy chương trình. Thật vậy, *mỗi* khi bạn chạy một chương trình, bạn đang thực hiện một thí nghiệm khoa học, mà trong đó chương trình của bạn là thế giới tự nhiên, để trả lời một trong những câu hỏi cốt lõi của chúng ta: *Chương trình của tôi sẽ chạy mất bao lâu?*

Quan sát định tính đầu tiên của chúng ta về hầu hết các chương trình là: *kích thước bài toán* là một đặc trưng cho độ khó của nhiệm vụ tính toán. Thông thường, kích thước bài toán là kích thước của đầu vào hoặc giá trị của một đối số dòng lệnh. Theo trực giác, thời gian chạy sẽ tăng theo kích thước bài toán, nhưng "nó tăng *bao nhiêu*" mới là câu hỏi xuất hiện một cách tự nhiên mỗi khi chúng ta phát triển và chạy một chương trình.

Một quan sát định tính khác đối với nhiều chương trình là: thời gian chạy nói chung là không bị ảnh hưởng bởi nội dung đầu vào; nó phụ thuộc vào kích thước bài toán là chính. Nếu quan sát này không đúng, chúng ta cần thực hiện các bước để hiểu rõ hơn và có lẽ kiểm soát tốt hơn độ nhạy của thời gian chạy đối với đầu vào. Nhưng điều này thường đúng, vì vậy bây giờ chúng ta tập trung vào mục tiêu định lượng tốt hơn mối quan hệ giữa kích thước bài toán và thời gian chạy.

***Ví dụ.*** Ta sẽ dùng chương trình `ThreeSum` đưới đây làm ví dụ để thảo luận. Chương trình này đọc một file chứa N số nguyên và đếm xem có bao nhiêu bộ ba trong đó có tổng bằng 0 (giả sử rằng không có tràn số). Công việc tính toán này có vẻ nhàm chán đối với bạn, nhưng nó liên quan rất sâu đến nhiều tác vụ tính toán mang tính nền tảng (ví dụ, xem Bài tập 1.4.26). Để làm dữ liệu thí nghiệm, hãy lấy file `1Mints.txt` từ trang web của sách, file này chứa 1 triệu giá trị int được tạo ngẫu nhiên. Các số thứ hai, thứ tám và thứ mười trong `1Mints.txt` có tổng bằng 0. Hỏi ngoài ra còn có bao nhiêu bộ ba như vậy trong tệp? Chương trình `ThreeSum` có thể cho chúng ta câu trả lời, nhưng liệu nó có thể làm vậy trong một khoảng thời gian hợp lý không? Kích thước bài toán N có quan hệ như thế nào với thời gian chạy của `ThreeSum`? Ở thí nghiệm đầu tiên, hãy chạy `ThreeSum` trên máy của bạn cho các file `1Kints.txt`, `2Kints.txt`, `4Kints.txt`, và `8Kints.txt`, chúng lần lượt chứa 1000, 2000, 4000, và 8000 số đầu tiên của `1Mints.txt`. Bạn có thể nhanh chóng thấy kết quả rằng có 70 bộ ba có tổng bằng 0 trong tệp `1Kints.txt` và có 528 bộ ba có tổng bằng 0 trong tệp `2Kints.txt`. Chương trình mất nhiều thời gian hơn đáng kể để xác định có 4.039 bộ ba có tổng bằng 0 trong tệp `4Kints.txt`, và khi bạn chờ chương trình hoàn thành cho tệp `8Kints.txt`, bạn sẽ thấy mình tự đặt câu hỏi: *Chương trình sẽ chạy mất bao lâu?* Như bạn sẽ thấy, trả lời câu hỏi này cho chương trình này hóa ra lại dễ dàng. Thật vậy, thường là bạn có thể đưa ra một dự đoán khá chính xác ngay trong khi chương trình đang chạy.

***Stopwatch.*** Việc đo thời gian chạy của một chương trình một cách chính xác và đáng tin cậy có thể khó khăn. May mắn là chúng ta thường hài lòng với các ước tính. Chúng ta muốn có thể phân biệt các chương trình sẽ hoàn thành trong vài giây hoặc vài phút với những chương trình có thể yêu cầu vài ngày hoặc vài tháng hoặc hơn. Khi có một chương trình nhanh gấp đôi một chương trình khác khi thực hiện cùng một tác vụ, chúng ta muốn biết được điều đó. Tuy nhiên, chúng ta vẫn cần các phép đo chính xác để tạo ra dữ liệu thực nghiệm mà chúng ta có thể sử dụng để thiết lập các giả thuyết về mối quan hệ giữa thời gian chạy với kích thước bài toán và kiểm tra tính đúng đắn của các giả thuyết đó. Với mục đích này, chúng ta sử dụng cấu trúc `Stopwatch`. Phương thức `elapsedTime()` của nó trả về thời gian (tính bằng giây) đã trôi qua kể từ khi nó được tạo. Phương thức này dùng hàm hệ thống `currentTimeMillis()` của Java, hàm này trả về thời gian hiện tại tính bằng miligiây, để lưu thời gian khi constructor của nó được gọi, sau đó gọi lại lần nữa để tính thời gian đã trôi qua khi `elapsedTime()` được gọi.

![Stopwatch API](https://algs4.cs.princeton.edu/14analysis/images/stopwatch-api.png "Stopwatch API")

***Phân tích dữ liệu thực nghiệm.*** Chương trình `DoublingTest` là một chương trình ứng dụng sử dụng `Stopwatch` một cách tinh vi hơn để tạo ra dữ liệu thực nghiệm cho `ThreeSum`. Nó tạo ra một chuỗi các mảng đầu vào ngẫu nhiên, mỗi bước lại tăng gấp đôi kích thước mảng, và in ra thời gian chạy của `ThreeSum.count()` cho mỗi kích thước đầu vào. Các thí nghiệm này chắc chắn có thể tái lập được — bạn cũng có thể chạy chúng trên máy tính của mình, bao nhiêu lần tùy thích. Khi bạn chạy `DoublingTest`, bạn sẽ thấy bản thân thực hiện một chu trình dự đoán-kiểm chứng: nó in ra vài dòng rất nhanh, nhưng sau đó chậm lại đáng kể. Mỗi khi nó in ra một dòng, bạn sẽ tự hỏi bao lâu nữa thì nó sẽ in dòng tiếp theo. Tất nhiên, vì máy tính của bạn khác với máy của chúng tôi, thời gian chạy thực tế mà bạn nhận được có thể sẽ khác với thời gian hiển thị trên máy tính của chúng tôi. Thật vậy, nếu máy tính của bạn nhanh gấp đôi máy của chúng tôi, thời gian chạy của bạn sẽ chỉ bằng khoảng một nửa của chúng tôi, điều này ngay lập tức dẫn đến giả thuyết có cơ sở vững chắc rằng thời gian chạy trên các máy tính khác nhau có thể khác nhau bởi một hệ số là hằng số. Tuy nhiên, bạn vẫn sẽ thấy mình đặt câu hỏi chi tiết hơn: *Chương trình của tôi sẽ chạy với thời gian là bao lâu, tính theo một hàm của kích thước đầu vào?* Để giúp trả lời câu hỏi này, chúng ta vẽ đồ thị dữ liệu. Các đồ thị dưới đây hiển thị kết quả trên hệ tọa độ thông thường và hệ log-log, với kích thước bài toán N trên trục x và thời gian chạy T(N) trên trục y. 

![log-log](https://algs4.cs.princeton.edu/14analysis/images/loglog.png "log-log")

Đồ thị log-log cho thấy ngay một giả thuyết về thời gian chạy: dữ liệu khớp với một đường thẳng có độ dốc 3 trên đồ thị log-log. Phương trình của đường thẳng đó là

$$lg(T(N)) = 3 lg N + lg a$$

trong đó, `a` là một hằng số. Phương trình trên tương đương với

$$T(N) = a N^3$$

đó là hàm của thời gian chạy với biến là kích thước đầu vào, cái mà ta đang cần. Chúng ta có thể sử dụng một trong các điểm dữ liệu của mình để giải phương trình tìm a — ví dụ, $T(8000) = 51.1 = a 8000^3$, vậy $a = 9.98 \times 10^{-11}$ — và sau đó sử dụng phương trình

$$T(N) = 9.98 \times 10^{-11} N^3$$

để dự đoán thời gian chạy cho N lớn. Một cách không chính thức, chúng ta đang kiểm chứng giả thuyết rằng các điểm dữ liệu trên biểu đồ log-log nằm gần đường thẳng này. Có thể dùng các phương pháp thống kê để phân tích cẩn thận hơn nhằm ước tính `a` và số mũ `b`, nhưng các phép tính nhanh của chúng ta đủ để ước tính thời gian chạy cho hầu hết các mục đích. Ví dụ, có thể ước tính thời gian chạy trên máy tính của chúng tôi  cho `N = 16.000` là khoảng $9.98 \times 10^{-11} \times 16000^3 = 408.8$ giây, hay là khoảng 6.8 phút (thời gian thực tế là 409.3 giây). Trong khi chờ máy tính của bạn in dòng cho `N = 16.000` trong `DoublingTest`, bạn có thể sử dụng phương pháp này để dự đoán khi nào nó sẽ kết thúc, sau đó kiểm tra kết quả bằng cách chờ xem liệu dự đoán của bạn có đúng không.

Cho đến nay, quá trình này phản ánh quá trình mà các nhà khoa học sử dụng khi cố gắng tìm hiểu các thuộc tính của thế giới thực. Một đường thẳng trên đồ thị log-log tương đương với giả thuyết rằng dữ liệu khớp với phương trình $T(N) = a \times N^b$. Một hiện tượng khớp như vậy được gọi là một luật lũy thừa (*power law*). Rất nhiều hiện tượng tự nhiên và tổng hợp được mô tả bằng luật lũy thừa, và việc giả thuyết rằng thời gian chạy của một chương trình cũng tuân theo luật này là hợp lý. Thật vậy, đối với việc phân tích thuật toán, chúng ta có các mô hình toán học hỗ trợ mạnh mẽ cho giả thuyết này và các giả thuyết tương tự, mà bây giờ chúng ta sẽ bàn đến.

## Các mô hình toán học

Trong những ngày đầu của khoa học máy tính, D. E. Knuth đã đưa ra giả thuyết rằng, bất chấp tất cả các yếu tố phức tạp trong việc tìm hiểu thời gian chạy của các chương trình, về nguyên tắc, có thể xây dựng một mô hình toán học để mô tả thời gian chạy của bất kỳ chương trình nào. Nhận định nền tảng của Knuth rất đơn giản: tổng thời gian chạy của một chương trình được xác định bởi hai yếu tố chính:
- Chi phí thực hiện mỗi câu lệnh
- Tần suất thực hiện mỗi câu lệnh

Yếu tố đầu tiên là một thuộc tính của máy tính, trình biên dịch Java và hệ điều hành; yếu tố sau là một thuộc tính của chương trình và dữ liệu vào. Nếu chúng ta biết cả hai yếu tố đó cho tất cả các chỉ thị trong chương trình, chúng ta có thể nhân chúng lại với nhau và tổng lại cho tất cả các chỉ thị trong chương trình để có được thời gian chạy.

Khó khăn chính trong việc xác định tần suất thực hiện của các lệnh. 
- Một số lệnh dễ phân tích: ví dụ, câu lệnh gán `cnt` bằng `0` trong `ThreeSum.count()` được thực thi đúng một lần. 

- Một số lệnh khác cần lập luận phức tạp hơn: ví dụ, lệnh `if` trong `ThreeSum.count()` được thực thi chính xác $N(N-1)(N-2)/6$ lần (số cách chọn ba số khác nhau từ mảng đầu vào — xem Bài tập 1.4.1). 

- Các lệnh khác phụ thuộc vào dữ liệu đầu vào: ví dụ, số lần lệnh `cnt++` trong `ThreeSum.count()` được chạy chính xác là số bộ ba có tổng bằng 0 trong dữ liệu vào, con số này có thể từ 0 đến số tất cả các bộ ba. Trong trường hợp của chương trình `DoublingTest`, do chúng ta tạo ra dữ liệu là các số ngẫu nhiên, nên có thể dùng phân tích xác suất để xác định giá trị kỳ vọng của đại lượng này (xem Bài tập 1.4.40).

***Ký hiệu xấp xỉ (~)***. Các phân tích tần suất kiểu này có thể dẫn đến các biểu thức toán học phức tạp và dài dòng. Ví dụ, xét số lần lệnh `if` trong `ThreeSum` được thực thi:
$$N (N-1)(N-2)/6 = N^3/6 - N^2/2 + N/3$$

Như thường lệ trong các biểu thức như vậy, các số hạng sau số hạng dẫn đầu là tương đối nhỏ (ví dụ, khi N = 1000, giá trị của $- N^2/2 + N/3$ là -499.667, chắc chắn không đáng kể so với $N^3/6 ≈ 166.666.667$). Để có thể bỏ qua các số hạng không đáng kể và nhờ đó đơn giản hóa đáng kể các công thức toán học cần tính, ta thường sử dụng một công cụ toán học được gọi là ký hiệu xấp xỉ (tilde notation ~). Ký hiệu này cho phép chúng ta làm việc với các công thức xấp xỉ, bỏ đi các số hạng bậc thấp vốn làm phức tạp công thức và đóng góp không đáng kể vào các giá trị đáng quan tâm:

Ta viết $~ f(N)$ để đại diện cho tất cả các hàm mà khi chia cho f(N) được kết quả có giới hạn là 1 khi N tiến đến vô cùng. Ta viết $g(N) ~ f(N)$ để hàm ý rằng $g(N) / f(N)$ tiến đến 1 khi N tăng.

![tilde](https://algs4.cs.princeton.edu/14analysis/images/tilde.png "tilde")
*Ví dụ về xấp xỉ*

Ví dụ, chúng ta sử dụng xấp xỉ $~N^3/6$ để mô tả số lần lệnh if trong ThreeSum được thực thi, vì $N^3/6 - N^2/2 + N/3$ chia cho $N^3/6$ tiến đến 1 khi N lớn. Thường xuyên nhất, chúng ta làm việc với các xấp xỉ có dạng
$g(N) ~ a * f(N)$, trong đó $f(N) = N^b * (log N)^c$
với a, b và c là các hằng số, và ta gọi $f(N)$ là *bậc tăng* (*order of growth*) của $g(N)$. Khi sử dụng lôgarit trong bậc tăng, chúng ta thường không chỉ định cơ số, vì hằng số a có thể hấp thụ chi tiết đó. Cách sử dụng này bao gồm một số tương đối nhỏ các hàm thường gặp khi nghiên cứu bậc tăng của thời gian chạy chương trình, như trong bảng bên trái (ngoại trừ hàm mũ mà chúng ta sẽ đề cập sau trong Chương CONTEXT). Sau khi hoàn thành nội dung về `ThreeSum`, ta sẽ mô tả các hàm này chi tiết hơn và thảo luận ngắn gọn lý do tại sao chúng xuất hiện trong phân tích thuật toán.

![classifications](https://algs4.cs.princeton.edu/14analysis/images/classifications.png "classifications") 
*Các phân loại bậc tăng điển hình*

***Xấp xỉ thời gian chạy.*** Để theo cách tiếp cận của Knuth nhằm xây dựng một biểu thức toán học cho tổng thời gian chạy của một chương trình Java, về nguyên tắc, chúng ta có thể tìm hiểu trình biên dịch Java mình đang dùng để tìm số lệnh máy tương ứng với mỗi lệnh Java và tìm hiểu thông số kỹ thuật máy của chúng ta để tìm thời gian thực thi của mỗi lệnh máy, rồi tính ra tổng cộng. Ta phân loại các khối lệnh Java theo tần suất thực thi của chúng, lấy các xấp xỉ số hạng dẫn đầu của các tần suất, xác định chi phí của mỗi lệnh, và sau đó tính tổng. Lưu ý rằng một số tần suất có thể phụ thuộc vào đầu vào. Trong trường hợp này, số lần `cnt++` được thực thi chắc chắn phụ thuộc vào đầu vào — đó là số bộ ba có tổng bằng 0, và có thể dao động từ $0$ đến $~N^3/6$. Chúng ta không đi sâu vào chi tiết (giá trị của các hằng số) cho bất kỳ hệ thống cụ thể nào, ngoại trừ việc nhấn mạnh rằng bằng cách sử dụng các hằng số $t_0$, $t_1$, $t_2$, ... đại diện cho thời gian cần thiết để chạy các khối lệnh, chúng ta đang giả định rằng mỗi khối lệnh Java tương ứng với các lệnh máy có chi phí là một lượng thời gian cố định cụ thể. Một quan sát quan trọng từ bài tập này là ghi nhận rằng chỉ những lệnh được thực thi thường xuyên nhất mới giữ vai trò trong tổng cuối cùng — chúng ta gọi những lệnh này là *vòng lặp bên trong* (*inner loop*) của chương trình. Đối với `ThreeSum`, vòng lặp bên trong là các câu lệnh tăng k và kiểm tra k nhỏ hơn N và các câu lệnh kiểm tra xem tổng của ba số đã cho có bằng 0 hay không (và có thể là câu lệnh thực hiện việc đếm, tùy thuộc vào đầu vào). Hành vi này là điển hình: thời gian chạy của rất nhiều chương trình chỉ phụ thuộc vào một tập hợp nhỏ các lệnh của chúng.

***Giả thuyết bậc tăng.*** Tổng kết lại, các thí nghiệm đo thời gian chạy và mô hình toán học ở phần trước đều hỗ trợ giả thuyết sau:
**Thuộc tính A.** Bậc tăng của thời gian chạy của ThreeSum (để tính số bộ ba có tổng bằng 0 trong N số) là $N^3$.
**Chứng minh:** Gọi $T(N)$ là thời gian chạy của `ThreeSum` cho $N$ số. Mô hình toán học vừa mô tả cho thấy rằng $T(N) ~ aN^3$ với $a$ là một hằng số phụ thuộc máy tính; các thí nghiệm trên nhiều máy tính (bao gồm máy của bạn và máy của chúng tôi) đã kiểm chứng xấp xỉ đó.
Trong suốt cuốn sách này, chúng ta sử dụng thuật ngữ *thuộc tính* để chỉ một giả thuyết cần được kiểm chứng bằng thực nghiệm. Kết quả cuối cùng của phân tích toán học của chúng ta giống hệt kết quả cuối cùng của phân tích thực nghiệm của chúng ta — thời gian chạy của `ThreeSum` là $~ aN^3$ với $a$ là một hằng số phụ thuộc máy. Sự trùng khớp này xác thực cả các thử nghiệm và mô hình toán học, nó cũng thể hiện thêm hiểu biết về chương trình vì nó không đòi hỏi phải có thí nghiệm xác định số mũ. Như vậy là với một chút nỗ lực, ta có thể kiểm chứng giá trị a cho một hệ thống cụ thể, tuy rằng hoạt động này thường chỉ dành cho các chuyên gia thực hiện trong các tình huống mà hiệu năng là yếu tố quyết định.

## Nguồn
Robert Sedgewick and Kevin Wayne, Algorithms, 4th ed., Addison-Wesley, Section 1.4