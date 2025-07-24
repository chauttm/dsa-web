# Ký hiệu Big O, Omega và Theta

## Theta
**Θ** (Theta) là ký hiệu chỉ **tốc độ tăng** (order of growth / rate of growth) của thời gian chạy, hay còn gọi là **cận chặt** (tight bound).
Với hàm $g(n)$ cho trước, ta ký hiệu $Θ(g(n))$ là tập hợp các hàm $f(n)$ thỏa mãn điều kiện: tồn tại các hằng số dương $n₀$ ,$c₁$, $c₂$ sao cho $c₁g(n) <= f(n) <= c₂g(n)$với mọi  $n >= n₀$.
Ví dụ, các hàm có dạng $f(n) = an^2 + bn + c$, với $a$, $b$, $c$ là các hằng số nào đó, đều thuộc tập hợp $Θ(g(n))$.
Ta viết $f(n) ∈ Θ(g(n))$, hoặc viết là $f(n) = Θ(g(n))$ cũng chấp nhận được và tiện lợi trong một số trường hợp.


Ví dụ: 
- Thuật toán linear search (tìm kiếm mảng bằng cách duyệt toàn bộ) có:
    - thời gian chạy trong trường hợp tốt nhất là $Θ(1)$ - best-case running time of $Θ(1)$
    - thời gian chạy trong trường hợp tồi nhất là $Θ(n)$ - worst-case running time of $Θ(n)$
    - thời gian chạy trong trường hợp trung bình là $Θ(n)$ - average-case running time of $Θ(n)$

- Thuật toán insertion sort có:
    - thời gian chạy trong trường hợp tốt nhất là $Θ(n)$ - best-case running time of $Θ(n)$
    - thời gian chạy trong trường hợp tồi nhất là $Θ(n^2)$ - worst-case running time of $Θ(n^2)$
    - thời gian chạy trong trường hợp trung bình là $Θ(n^2)$ - average-case running time of $Θ(n^2)$

## Big-Oh và Omega
**Θ** mô tả cả cận trên và cận dưới của một hàm, cho ta giới hạn chặt chẽ về hàm đó. Nhưng khi ta chỉ có được **cận trên** của hàm, ta dùng ký hiệu **Ο**. Hoặc khi ta chỉ muốn nói về **cận dưới** của hàm, ta dùng ký hiệu **Ω**. 

Với hàm $g(n)$ cho trước, 
- $Ω(g(n))$ là tập hợp các hàm $f(n)$ thỏa mãn điều kiện: tồn tại các hằng số dương $n₀$ và $c$ sao cho $f(n) >= cg(n)$ với mọi  $n >= n₀$.
- $O(g(n))$ là tập hợp các hàm $f(n)$ thỏa mãn điều kiện: tồn tại các hằng số dương $n₀$ và $c$ sao cho $f(n) <= cg(n)$ với mọi  $n >= n₀$.

Hai ký hiệu này có thể được áp dụng cho cả trường hợp tốt nhất và trường hợp xấu nhất cho thuật toán tìm kiếm nhị phân:

Ví dụ: Tìm kiếm Nhị phân
- Trường hợp tốt nhất: Phần tử đầu tiên bạn tìm chính là phần tử bạn đang tìm kiếm
  - $Ω(1)$: ta cần ít nhất một lần tra cứu
  - $Ο(1)$: ta cần nhiều nhất một lần tra cứu

- Trường hợp xấu nhất: Phần tử không có trong mảng
  - $Ω(log n)$: ta cần ít nhất $log n$ bước để có thể nói rằng phần tử bạn đang tìm không có trong mảng
  - $Ο(log n)$: ta cần nhiều nhất $log n$ bước để có thể nói rằng phần tử bạn đang tìm không có trong mảng

Có thể thấy ở đây các cận trên và dưới trùng nhau. Trong trường hợp đó, ta có thể mô tả bằng **cận chặt**:
- Trường hợp tốt nhất là $Θ(1)$
- Trường hợp xấu nhất là $Θ(log n)$

Nhưng thường thì chúng ta chỉ muốn biết **cận trên** hoặc **cận chặt** vì cận dưới không có nhiều giá trị trực tiễn.

# Sử dụng trong thực tế
Nhiều người nói/viết theo kiểu "Thời gian chạy của insertion sort là $Θ(n^2)$. Nghĩa chính xác và đầy đủ của câu trên là "Có một cái hàm $f(n)$ thuộc loại $Θ(n^2)$ mà insertion sort với input kiểu gì cũng không chạy chậm hơn $f(n)$".
Phát biểu đó tương đương với "Thời gian chạy trong trường hợp xấu nhất của insertion sort là $Θ(n^2)$".
Tương tự, khi có người nói "thời gian chạy của insertion sort là $Ω(n)$", ý của họ thực ra là "với bất kể input nào với kích thước $n$, thời gian chạy của insertion sort cho input đó không ít hơn $n$ nhân với một hằng số, với $n$ đủ lớn". Phát biểu này tương đương với "Thời gian chạy trong trường hợp tốt nhất của insertion sort là $Ω(n)$".

Theo [^1], về kỹ thuật, cách nói trên là lạm dụng. Thực tế là nó gây ra rất nhiều hiểu lầm. Tuy nhiên, đây lại là cách nói rất thông dụng.

[^1]Cornel et al., Introduction to Algorithms, 3rd ed., The MIT Press.