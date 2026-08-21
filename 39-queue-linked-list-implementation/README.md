# Cài đặt Queue bằng danh sách liên kết

## Khái niệm

Queue cũng có thể cài đặt bằng [danh sách liên kết đơn](../23-linked-list-fundamentals/), với hai con trỏ riêng biệt: **`front`** trỏ tới node đầu danh sách (đầu hàng đợi) và **`rear`** trỏ tới node cuối danh sách (cuối hàng đợi). Việc giữ cả hai con trỏ là điểm mấu chốt để đạt hiệu năng tốt.

## Giải thích chi tiết

### Vì sao cần giữ cả hai con trỏ `front` và `rear`?

Nếu chỉ giữ `front` (giống danh sách liên kết thông thường), thao tác `Enqueue` (thêm vào cuối) sẽ phải **duyệt từ đầu để tìm node cuối** — tốn O(n) (xem [Thêm node vào đầu/cuối](../26-insert-node-at-head-tail/)). Bằng cách giữ thêm con trỏ `rear` trỏ thẳng tới node cuối, `Enqueue` chỉ cần gán `rear.Next = newNode` rồi cập nhật `rear = newNode` — đạt O(1).

### Cài đặt các thao tác

- **Enqueue(x)**: tạo `newNode`; nếu hàng đợi rỗng (`front == NULL`): `front = rear = newNode`; ngược lại: `rear.Next = newNode; rear = newNode`.
- **Dequeue()**: nếu `front == NULL` → Underflow; ngược lại: lấy `front.Data`, rồi `front = front.Next`; nếu sau đó `front == NULL` (vừa lấy phần tử cuối cùng) thì phải đặt luôn `rear = NULL` (nếu không, `rear` sẽ trỏ tới node đã bị "mồ côi", không còn ai trỏ tới).
- **Front()**: trả về `front.Data` nếu không rỗng.

**Lưu ý quan trọng**: bước cập nhật `rear = NULL` khi hàng đợi trở nên rỗng sau Dequeue là chi tiết dễ bị bỏ sót nhưng bắt buộc — nếu quên, lần `Enqueue` tiếp theo sẽ gán `rear.Next = newNode` vào một node đã bị loại bỏ, làm mất `newNode` khỏi danh sách thực sự được `front` trỏ tới.

### So sánh với cài đặt bằng mảng

| | Mảng dạng vòng | Danh sách liên kết |
|---|---|---|
| Kích thước | Cố định (dễ Overflow) | Linh hoạt, chỉ giới hạn bởi bộ nhớ |
| Enqueue/Dequeue | O(1) | O(1) (nhờ giữ con trỏ `rear`) |
| Bộ nhớ phụ | Không cần | Cần thêm con trỏ `Next` mỗi node |

## Độ phức tạp

| Thao tác | Big-O |
|---|---|
| Enqueue (nhờ có con trỏ `rear`) | O(1) |
| Dequeue | O(1) |
| Front | O(1) |

## Ví dụ

```csharp
class Node
{
    public int Data;
    public Node Next;
}

class LinkedQueue
{
    private Node front, rear;

    public bool IsEmpty() => front == null;

    public void Enqueue(int x)
    {
        Node newNode = new Node { Data = x, Next = null };
        if (IsEmpty())
        {
            front = rear = newNode;
        }
        else
        {
            rear.Next = newNode;
            rear = newNode;
        }
    }

    public int Dequeue()
    {
        if (IsEmpty()) throw new InvalidOperationException("Queue underflow");
        int value = front.Data;
        front = front.Next;
        if (front == null) rear = null;   // hàng đợi vừa trở nên rỗng
        return value;
    }

    public int Front()
    {
        if (IsEmpty()) throw new InvalidOperationException("Queue underflow");
        return front.Data;
    }
}
```

## Demo

Xem file [demo.html](./demo.html) — thử Enqueue/Dequeue trên hàng đợi cài đặt bằng danh sách liên kết, quan sát con trỏ `front` và `rear` luôn trỏ đúng hai đầu danh sách.
