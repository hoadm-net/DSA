# Khởi tạo và duyệt danh sách liên kết đơn

## Khái niệm

Khởi tạo danh sách liên kết là quá trình tạo các node và nối chúng lại bằng con trỏ `Next` để hình thành danh sách. Duyệt danh sách (traverse) là quá trình đi qua lần lượt từng node, bắt đầu từ `head`, theo con trỏ `Next` cho đến khi gặp `NULL`.

## Giải thích chi tiết

### Khởi tạo

Danh sách rỗng được khởi tạo bằng cách đặt `head = NULL`. Để xây dựng danh sách từ một tập giá trị, cách đơn giản nhất là **thêm lần lượt từng phần tử vào cuối** (xem [Thêm node vào đầu/cuối](../26-insert-node-at-head-tail/)), hoặc tạo node đầu tiên làm `head` rồi nối tiếp các node còn lại.

### Duyệt danh sách

Dùng một con trỏ tạm `p`, khởi tạo `p = head`, rồi lặp lại: xử lý node `p` hiện tại (in giá trị, đếm, tìm kiếm...), sau đó di chuyển `p = p.Next`. Vòng lặp dừng khi `p == NULL` — nghĩa là đã đi hết danh sách.

Đây là thao tác **nền tảng** cho hầu hết các thao tác khác trên danh sách liên kết: tìm kiếm một giá trị, đếm số node, tính tổng, in toàn bộ danh sách... đều dựa trên việc duyệt tuần tự này, vì danh sách liên kết **không hỗ trợ truy xuất ngẫu nhiên** theo chỉ số như mảng (xem [Khái niệm danh sách liên kết](../23-linked-list-fundamentals/)).

**Lưu ý quan trọng**: duyệt danh sách liên kết đơn chỉ đi được **một chiều** (từ head đến cuối), không thể quay ngược lại — nếu cần lùi về node trước đó phải duyệt lại từ đầu, hoặc dùng [danh sách liên kết đôi](../30-doubly-linked-list/).

## Độ phức tạp

| Thao tác | Big-O |
|---|---|
| Duyệt toàn bộ n node | O(n) |
| Truy xuất node thứ k (phải duyệt từ đầu) | O(k) |

## Ví dụ

```
FUNCTION Traverse(head)
    p = head
    WHILE p != NULL
        Xử lý (ví dụ: in) giá trị p.Data
        p = p.Next
    END WHILE
END FUNCTION
```

```csharp
class Node
{
    public int Data;
    public Node Next;
}

void Traverse(Node head)
{
    Node p = head;
    while (p != null)
    {
        Console.Write(p.Data + " ");
        p = p.Next;
    }
}
```

## Demo

Xem file [demo.html](./demo.html) — nhập các giá trị để khởi tạo danh sách, sau đó chạy từng bước để xem con trỏ `p` di chuyển từ `head` qua từng node cho đến `NULL`.
