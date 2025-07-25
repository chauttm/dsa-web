**Cấu trúc cơ bản của một chương trình Java**

Một chương trình Java (lớp) có thể là thư viện các phương thức tĩnh (hàm) hoặc định nghĩa một kiểu dữ liệu. Để tạo ra các thư viện phương thức tĩnh và định nghĩa kiểu dữ liệu, ta sử dụng năm thành phần sau – nền tảng của lập trình trong Java và nhiều ngôn ngữ hiện đại khác:

* **Kiểu dữ liệu nguyên thủy (primitive data types)** xác định rõ ý nghĩa của các khái niệm như số nguyên, số thực và giá trị boolean trong một chương trình máy tính. Định nghĩa của chúng bao gồm tập hợp các giá trị có thể có và các phép toán trên những giá trị đó, có thể được kết hợp thành các biểu thức giống như biểu thức toán học để xác định giá trị.

* **Câu lệnh (statements)** cho phép chúng ta xác định một phép tính bằng cách tạo và gán giá trị cho các biến, điều khiển luồng thực thi hoặc tạo ra các hiệu ứng phụ. Chúng ta sử dụng sáu loại câu lệnh: khai báo, gán, điều kiện, vòng lặp, gọi hàm và trả về.

* **Mảng (arrays)** cho phép chúng ta làm việc với nhiều giá trị cùng kiểu.

* **Phương thức tĩnh (static methods)** cho phép đóng gói và tái sử dụng mã nguồn, cũng như phát triển chương trình dưới dạng tập hợp các mô-đun độc lập.

* **Chuỗi (strings)** là các dãy ký tự. Một số thao tác trên chuỗi được tích hợp sẵn trong Java.

* **Nhập/xuất (input/output)** thiết lập sự giao tiếp giữa chương trình và thế giới bên ngoài.

* **Trừu tượng hóa dữ liệu (data abstraction)** mở rộng khái niệm đóng gói và tái sử dụng để cho phép chúng ta định nghĩa các kiểu dữ liệu không nguyên thủy, hỗ trợ lập trình hướng đối tượng.

Trong phần này, chúng ta sẽ xem xét lần lượt năm thành phần đầu tiên. Trừu tượng hóa dữ liệu sẽ được bàn đến trong phần tiếp theo.

Việc chạy một chương trình Java liên quan đến việc tương tác với hệ điều hành hoặc môi trường phát triển chương trình. Để dễ hiểu và đơn giản, chúng tôi mô tả các hành động đó theo kiểu **terminal ảo**, nơi chúng ta tương tác với chương trình bằng cách gõ các lệnh vào hệ thống. Xem trang sách điện tử (booksite) để biết thêm chi tiết về cách sử dụng terminal ảo trên hệ thống của bạn hoặc tìm hiểu về các môi trường phát triển chương trình nâng cao hơn hiện có trên các hệ thống hiện đại.

Ví dụ, chương trình **BinarySearch** gồm hai phương thức tĩnh là `rank()` và `main()`. Phương thức tĩnh đầu tiên `rank()` gồm bốn câu lệnh: hai khai báo, một vòng lặp (bản thân nó bao gồm một câu lệnh gán và hai câu điều kiện), và một lệnh trả về. Phương thức thứ hai `main()` gồm ba câu lệnh: một khai báo, một lệnh gọi và một vòng lặp (bao gồm một phép gán và một điều kiện).

Để chạy một chương trình Java, trước tiên ta **biên dịch** nó bằng lệnh `javac`, sau đó **chạy** nó bằng lệnh `java`. Ví dụ, để chạy chương trình BinarySearch, ta gõ lệnh:

```
javac BinarySearch.java
```

(Lệnh này sẽ tạo ra tập tin `BinarySearch.class`, chứa phiên bản cấp thấp của chương trình dưới dạng **bytecode Java**).

Sau đó, ta gõ:

```
java BinarySearch
```

(kèm theo tên tập tin danh sách trắng nếu cần) để chuyển quyền điều khiển sang phiên bản bytecode của chương trình.

Để xây dựng nền tảng hiểu biết về hiệu ứng của các hành động này, tiếp theo chúng ta sẽ tìm hiểu chi tiết về **kiểu dữ liệu nguyên thủy và biểu thức**, các **loại câu lệnh Java**, **mảng**, **phương thức tĩnh**, **chuỗi** và **nhập/xuất**.
