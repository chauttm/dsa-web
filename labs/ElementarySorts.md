# Bài tập về các thuật toán sắp xếp cơ bản.

Dưới đây là 5 bài tập dạng **Bug Hunting (Sửa lỗi ngầm)** cho 2 thuật toán **Insertion Sort** và **Selection Sort**.

Các đoạn mã này đều do AI viết (hoặc mô phỏng AI viết) – **chạy không bị lỗi cú pháp, vẫn ra kết quả đúng ở các test case cơ bản**, nhưng chứa các lỗi ngầm về logic, trường hợp biên (edge cases), tính ổn định (stability) hoặc hiệu năng ($O(n^2)$ bị đẩy thành tồi hơn).

---

## Bài 1: Insertion Sort – Lỗi mất phần tử do chèn sai chỗ (Bug ở vòng lặp trong)

**Ngữ cảnh:** Một sinh viên dùng AI để sinh code Insertion Sort sắp xếp mảng số nguyên tăng dần. AI trả về đoạn code Java dưới đây. Đoạn code chạy đúng với mảng `[5, 2, 4, 6, 1, 3]`.

```java
public class InsertionSortBuggy {

    public static void insertionSort(int[] arr) {
        int n = arr.length;
        for (int i = 1; i < n; i++) {
            int key = arr[i];
            int j = i - 1;

            // Vòng lặp dời các phần tử lớn hơn key sang phải
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }

            arr[j] = key; // Yêu cầu sinh viên tìm lỗi ở dòng này!
        }
    }

    public static void main(String[] args) {
        int[] arr = {5, 2, 4, 6, 1, 3};
    
        insertionSort(arr); 
    }
}

```

### Nhiệm vụ của sinh viên:

1. **Tìm Bug:** Chạy tay (Dry-run) đoạn code trên với mảng `[3, 1, 2]`. Cho biết mảng bị biến đổi thành gì sau vòng lặp đầu tiên (`i = 1`)?
2. **Giải thích:** Tại sao gán `arr[j] = key` ở cuối vòng lặp `while` lại gây ra lỗi index và ghi đè dữ liệu?
3. **Sửa lỗi:** Viết lại dòng code đúng và giải thích tại sao phải là `arr[j + 1] = key`.

---

## Bài 2: Insertion Sort – Lỗi vô hiệu hóa tính năng dừng sớm (Early Stop)

**Ngữ cảnh:** AI được yêu cầu viết thuật toán Insertion Sort tối ưu cho mảng *gần như đã sắp xếp*. AI trả về mã nguồn Java dưới đây:

```java
public static void insertionSort(int[] arr) {
    int n = arr.length;
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        
        while (j >= 0) {
            if (arr[j] > key) {
                arr[j + 1] = arr[j];
            } else {
                arr[j + 1] = key;
            }
            j--;
        }
        if (j < 0) {
            arr[0] = key;
        }
    }
}

```

### Nhiệm vụ của sinh viên:

1. **Tìm Bug:** Mã nguồn này vẫn sắp xếp ra kết quả đúng, nhưng nó đã làm hỏng **ưu điểm lớn nhất** của Insertion Sort. Đó là ưu điểm gì?
2. **Phân tích độ phức tạp:** Khi chạy mã nguồn này với một mảng **đã sắp xếp hoàn toàn** có $n$ phần tử (ví dụ: `[1, 2, 3, 4, 5]`), độ phức tạp thời gian thực tế là bao nhiêu? ($O(n)$ hay $O(n^2)$)? Tại sao?
3. **Sửa lỗi:** Tối ưu lại điều kiện dừng của vòng lặp `while` để khôi phục độ phức tạp $O(n)$ cho trường hợp tốt nhất (Best Case).

---

## Bài 3: Selection Sort – Lỗi làm mất tính ổn định (Loss of Stability)

**Ngữ cảnh:** Trong bài toán thực tế, ta cần sắp xếp danh sách Sinh viên theo **Điểm số (tăng dần)**. Nếu hai sinh viên bằng điểm nhau, **thứ tự ban đầu của họ phải được giữ nguyên** (Tính ổn định - Stable Sort). AI gợi ý đoạn code Python sau dùng Selection Sort:

```python
def selection_sort_students(students):
    n = len(students)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if students[j]['score'] < students[min_idx]['score']:
                min_idx = j
        
        # Hoán đổi phần tử nhỏ nhất tìm được về vị trí i
        students[i], students[min_idx] = students[min_idx], students[i]

```

### Nhiệm vụ của sinh viên:

1. **Tìm Bug:** Cho danh sách sinh viên ban đầu:
`[ {"name": "A", "score": 5}, {"name": "B", "score": 3}, {"name": "C", "score": 3} ]`
Hãy chạy tay thuật toán và ghi lại kết quả đầu ra. Thứ tự của **B** và **C** có bị thay đổi không?
2. **Phân tích:** Tại sao phép hoán đổi ngắt quãng `swap(students[i], students[min_idx])` lại phá vỡ tính ổn định (Unstable) của Selection Sort?
3. **Sửa lỗi/Đề xuất:** Làm thế nào để biến Selection Sort thành thuật toán ổn định (Stable)? *(Gợi ý: Thay phép Swap bằng hành động dời/chèn phần tử).*

---

## Bài 4: Selection Sort – Lỗi tối ưu hóa "ảo" gây lặp vô tận / Tràn mảng

**Ngữ cảnh:** AI muốn tối ưu Selection Sort bằng cách **tìm cả giá trị Nhỏ nhất (Min) và Lớn nhất (Max) trong cùng một vòng lặp** (Bidirectional Selection Sort / Double Selection Sort) để giảm số lần duyệt mảng xuống một nửa ($n/2$ bước).

```java
public class DoubleSelectionSortBuggy {

    public static void doubleSelectionSort(int[] arr) {
        int left = 0;
        int right = arr.length - 1;

        while (left < right) {
            int min_idx = left;
            int max_idx = right; // Lỗi ngầm tiềm ẩn từ việc khởi tạo?

            for (int i = left; i <= right; i++) {
                if (arr[i] < arr[min_idx]) min_idx = i;
                if (arr[i] > arr[max_idx]) max_idx = i;
            }

            // Swap phần tử nhỏ nhất về left
            int temp = arr[left];
            arr[left] = arr[min_idx];
            arr[min_idx] = temp;

            // Swap phần tử lớn nhất về right
            temp = arr[right];
            arr[right] = arr[max_idx];
            arr[max_idx] = temp;

            left++;
            right--;
        }
    }

    public static void main(String[] args) {
        // Test case bẫy khiến đoạn code trên xuất ra kết quả sai:
        int[] arr = {4, 1, 3, 2};

        System.out.println("Mảng ban đầu:");
        printArray(arr);

        doubleSelectionSort(arr);

        System.out.println("Mảng sau khi sắp xếp (Bị sai do lỗi ngầm):");
        printArray(arr); // Kết quả sẽ ra [1, 2, 4, 3] thay vì [1, 2, 3, 4]
    }

    private static void printArray(int[] arr) {
        for (int val : arr) {
            System.out.print(val + " ");
        }
        System.out.println();
    }
}

```

### Nhiệm vụ của sinh viên:

1. **Tạo Test case bẫy (Bug Hunting):** Tìm một mảng gồm 4 số nguyên khiến đoạn code trên xuất ra **kết quả sai hoàn toàn**. *(Gợi ý: Hãy thử trường hợp phần tử Lớn nhất ban đầu nằm ngay tại vị trí `left`).*
2. **Giải thích bẫy logic:** Tại sao sau khi thực hiện phép `swap` đưa `min_idx` về `left`, chỉ số `max_idx` có thể không còn trỏ đúng đến giá trị lớn nhất nữa?
3. **Sửa lỗi:** Thêm đoạn code xử lý cập nhật lại `max_idx` nếu `max_idx == left` trước khi thực hiện phép `swap` thứ hai.

---

## Bài 5: Insertion Sort & Selection Sort trên Danh sách liên kết (Pointer Bug)

**Ngữ cảnh:** Sinh viên yêu cầu AI chuyển thuật toán **Insertion Sort** sang chạy trên **Danh sách liên kết đơn (Singly Linked List)** bằng C++. AI viết đoạn mã dời con trỏ để chèn nút mới vào danh sách đã sắp xếp:

```java
class Node {
    int data;
    Node next;

    Node(int val) {
        this.data = val;
        this.next = null;
    }
}

public class InsertionSortLinkedListBuggy {

    public static Node insertionSortList(Node head) {
        if (head == null || head.next == null) return head;

        Node dummy = new Node(0); // Nút giả làm head
        Node curr = head;

        while (curr != null) {
            Node prev = dummy;

            // Tìm vị trí thích hợp để chèn curr vào danh sách mới (dưới dummy)
            while (prev.next != null && prev.next.data < curr.data) {
                prev = prev.next;
            }

            // Thực hiện chèn nút curr vào giữa prev và prev.next
            curr.next = prev.next;
            prev.next = curr;

            // Chuyển sang nút tiếp theo của danh sách ban đầu
            curr = curr.next; // Bug chí mạng ở đây!
        }

        return dummy.next;
    }

    public static void main(String[] args) {
        // Tạo danh sách liên kết: 4 -> 2 -> 1 -> 3
        Node head = new Node(4);
        head.next = new Node(2);
        head.next.next = new Node(1);
        head.next.next.next = new Node(3);

        System.out.println("Đang chạy Insertion Sort trên Danh sách liên kết...");
        
        Node sortedHead = insertionSortList(head);

        printList(sortedHead);
    }

    private static void printList(Node head) {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.data + " -> ");
            temp = temp.next;
        }
        System.out.println("null");
    }
}
```

### Nhiệm vụ của sinh viên:

1. **Tìm Bug:** Khi chạy đoạn code trên, chương trình bị rơi vào **Vòng lặp vô tận (Infinite Loop)** hoặc ngắt đột ngột (Segmentation Fault). Hãy chỉ ra chính xác dòng code gây ra lỗi này.
2. **Giải thích:** Dòng `curr->next = prev->next` đã làm thay đổi thuộc tính gì của nút `curr`? Tại sao bước `curr = curr->next` ở cuối vòng lặp lại không thể lấy được nút tiếp theo trong danh sách ban đầu nữa?
3. **Sửa lỗi:** Viết lại đoạn mã bằng cách dùng một biến tạm `Node* next_node` để lưu trước liên kết trước khi thực hiện chèn.

---

### 💡 Hướng dẫn cho giảng viên khi đưa 5 bài này vào Lab:

* **Không cung cấp đáp án trước.** Cho sinh viên chép đúng đoạn code trên vào IDE để tự biên dịch và chạy thử các bộ test do giảng viên gợi ý.
* Yêu cầu sinh viên **vẽ sơ đồ bộ nhớ/chạy tay (Dry-run) trên giấy** giải thích cơ chế bị lỗi trước khi sửa code.
* Các bài tập này rèn luyện cho sinh viên năng lực **Code Reviewing (Thẩm định mã nguồn)**
