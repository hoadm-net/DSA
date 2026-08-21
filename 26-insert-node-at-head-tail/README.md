# Thêm node vào đầu/cuối danh sách

## Khái niệm

Thêm node vào đầu (head) hoặc cuối (tail) là hai thao tác thêm dữ liệu cơ bản nhất trên danh sách liên kết đơn. Nhờ đặc điểm không cần dịch chuyển phần tử như mảng, cả hai thao tác này đều có thể thực hiện với chi phí thời gian rất thấp.

## Giải thích chi tiết

### Thêm vào đầu danh sách (Insert at Head)

1. Tạo node mới `newNode`, gán `newNode.Data = giá trị cần thêm`.
2. Gán `newNode.Next = head` (node mới trỏ tới node đầu tiên hiện tại).
3. Cập nhật `head = newNode` (node mới trở thành đầu danh sách).

Không cần duyệt qua bất kỳ node nào — vì vậy thêm vào đầu luôn có chi phí **O(1)**, bất kể danh sách dài hay ngắn.

### Thêm vào cuối danh sách (Insert at Tail)

1. Tạo node mới `newNode`, gán `newNode.Next = NULL` (vì sẽ là node cuối).
2. Nếu danh sách rỗng (`head == NULL`): gán `head = newNode`.
3. Ngược lại: **duyệt từ head đến node cuối cùng** (node có `Next == NULL`), rồi gán `node_cuối.Next = newNode`.

Vì phải duyệt để tìm node cuối, thêm vào cuối có chi phí **O(n)** nếu chỉ có con trỏ `head`. Nếu cấu trúc danh sách có giữ thêm con trỏ `tail` riêng (trỏ trực tiếp tới node cuối), thao tác này cũng có thể đạt O(1) — đây là một tối ưu phổ biến trong thực tế.

### So sánh với thêm vào mảng

| | Mảng | Danh sách liên kết |
|---|---|---|
| Thêm vào đầu | O(n) — phải dịch chuyển toàn bộ phần tử | O(1) |
| Thêm vào cuối (không giữ tail) | O(1) trung bình (nếu còn chỗ trống) | O(n) — phải duyệt tìm node cuối |
| Thêm vào cuối (có giữ con trỏ tail) | O(1) | O(1) |

## Độ phức tạp

| Thao tác | Big-O |
|---|---|
| Thêm vào đầu | O(1) |
| Thêm vào cuối (chỉ có head) | O(n) |
| Thêm vào cuối (có giữ con trỏ tail) | O(1) |

## Ví dụ

```
FUNCTION InsertAtHead(head, value)
    newNode = Node(value)
    newNode.Next = head
    head = newNode
    RETURN head
END FUNCTION

FUNCTION InsertAtTail(head, value)
    newNode = Node(value)
    newNode.Next = NULL
    IF head == NULL THEN
        RETURN newNode
    END IF
    p = head
    WHILE p.Next != NULL
        p = p.Next
    END WHILE
    p.Next = newNode
    RETURN head
END FUNCTION
```

```csharp
Node InsertAtHead(Node head, int value)
{
    Node newNode = new Node { Data = value, Next = head };
    return newNode; // node mới trở thành head
}

Node InsertAtTail(Node head, int value)
{
    Node newNode = new Node { Data = value, Next = null };
    if (head == null) return newNode;
    Node p = head;
    while (p.Next != null) p = p.Next;
    p.Next = newNode;
    return head;
}
```

## Demo

Xem file [demo.html](./demo.html) — khởi tạo danh sách rồi thử thêm giá trị mới vào đầu hoặc cuối, quan sát node mới (màu xanh) và các liên kết được cập nhật.
