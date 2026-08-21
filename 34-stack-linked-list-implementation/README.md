# Cài đặt Stack bằng danh sách liên kết

## Khái niệm

Stack cũng có thể cài đặt bằng [danh sách liên kết đơn](../23-linked-list-fundamentals/), trong đó **node đầu (head)** của danh sách đóng vai trò là **đỉnh (top)** của stack. Cách cài đặt này khắc phục nhược điểm về kích thước cố định của [cài đặt bằng mảng](../33-stack-array-implementation/).

## Giải thích chi tiết

### Ý tưởng

Vì Stack chỉ thao tác ở một đầu (đỉnh), và danh sách liên kết đơn có thao tác **thêm/xóa ở đầu (head) với chi phí O(1)** (xem [Thêm node vào đầu/cuối](../26-insert-node-at-head-tail/) và [Xóa node](../28-delete-node/)), nên head của danh sách được chọn làm top của stack một cách tự nhiên:

- **Push(x)** ⟺ thêm node mới vào **đầu** danh sách, node mới trở thành `head` (= top).
- **Pop()** ⟺ lấy giá trị của `head`, sau đó xóa node đầu, `head = head.Next`.
- **Top()** ⟺ đọc giá trị `head.Data` mà không thay đổi gì.

### So sánh với cài đặt bằng mảng

| | Mảng | Danh sách liên kết |
|---|---|---|
| Kích thước | Cố định (dễ Overflow) hoặc phải cấp phát lại | Linh hoạt, chỉ giới hạn bởi bộ nhớ máy |
| Push/Pop | O(1) | O(1) |
| Bộ nhớ phụ | Không cần | Cần thêm con trỏ `Next` ở mỗi node |
| Overflow | Có thể xảy ra nếu capacity cố định | Gần như không xảy ra (chỉ khi hết bộ nhớ) |

Vì Push/Pop chỉ thao tác ở head — **không cần duyệt** — nên cả hai cách cài đặt đều đạt O(1) cho các thao tác chính; lựa chọn giữa hai cách chủ yếu dựa vào việc có biết trước giới hạn kích thước hay không.

## Độ phức tạp

| Thao tác | Big-O |
|---|---|
| Push (thêm vào head) | O(1) |
| Pop (xóa khỏi head) | O(1) |
| Top (đọc head) | O(1) |
| IsEmpty | O(1) |

## Ví dụ

```csharp
class Node
{
    public int Data;
    public Node Next;
}

class LinkedStack
{
    private Node top;   // top chính là head của danh sách

    public bool IsEmpty() => top == null;

    public void Push(int x)
    {
        Node newNode = new Node { Data = x, Next = top };
        top = newNode;
    }

    public int Pop()
    {
        if (IsEmpty()) throw new InvalidOperationException("Stack underflow");
        int value = top.Data;
        top = top.Next;
        return value;
    }

    public int Top()
    {
        if (IsEmpty()) throw new InvalidOperationException("Stack underflow");
        return top.Data;
    }
}
```

## Demo

Xem file [demo.html](./demo.html) — thử Push/Pop/Top trên stack cài đặt bằng danh sách liên kết, quan sát node mới luôn được thêm vào (và lấy ra từ) đầu danh sách.
