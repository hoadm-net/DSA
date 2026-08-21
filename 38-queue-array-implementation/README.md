# Cài đặt Queue bằng mảng (dạng vòng)

## Khái niệm

Nếu cài đặt Queue bằng mảng theo cách đơn giản nhất (Enqueue thêm vào cuối, Dequeue lấy ở đầu rồi dịch chuyển toàn bộ phần tử còn lại lên một vị trí), thao tác Dequeue sẽ tốn O(n) — rất kém hiệu quả. **Hàng đợi vòng (circular queue)** giải quyết vấn đề này bằng cách coi mảng như một **vòng tròn khép kín**: khi chỉ số vượt quá cuối mảng, nó "quay vòng" về đầu mảng (dùng phép chia lấy dư `mod capacity`).

## Giải thích chi tiết

### Vấn đề của cài đặt mảng "ngây thơ"

Nếu chỉ dùng hai chỉ số `front` và `rear` tăng dần mà không dịch chuyển phần tử: sau vài lần Dequeue, các vị trí đầu mảng bị "bỏ trống" vĩnh viễn, trong khi `rear` tiếp tục tiến về cuối mảng — dẫn đến báo Overflow dù mảng vẫn còn nhiều chỗ trống (chỉ là trống ở đầu, không dùng lại được).

### Giải pháp: đánh chỉ số theo vòng (modulo)

Giữ ba biến: `front` (chỉ số phần tử đầu), `count` (số phần tử hiện có), và `capacity` (kích thước mảng). Khi tính vị trí cần ghi/đọc, luôn lấy phần dư cho `capacity` để "quay vòng":

- **Enqueue(x)**: nếu `count == capacity` → Overflow; ngược lại, ghi `x` vào vị trí `(front + count) % capacity`, rồi `count++`.
- **Dequeue()**: nếu `count == 0` → Underflow; ngược lại, lấy giá trị tại `items[front]`, rồi `front = (front + 1) % capacity`, `count--`.
- **Front()**: nếu `count == 0` → lỗi; ngược lại, trả về `items[front]`.

Nhờ phép `mod capacity`, các vị trí đã được Dequeue (trống ở đầu mảng) sẽ được **tái sử dụng** khi `rear` "quay vòng" lại từ đầu — không còn lãng phí bộ nhớ như cài đặt ngây thơ.

Dùng biến `count` riêng (thay vì suy ra từ `front`/`rear`) giúp **phân biệt rõ ràng** hai trường hợp `front == rear` dễ gây nhầm lẫn: hàng đợi **rỗng** (`count == 0`) và hàng đợi **đầy** (`count == capacity`) — nếu không có `count`, hai trường hợp này có cùng biểu diễn `front == rear` và không thể phân biệt được.

### Ưu điểm và nhược điểm

**Ưu điểm**: mọi thao tác O(1), tận dụng tối đa không gian mảng đã cấp phát, không lãng phí như cài đặt ngây thơ.

**Nhược điểm**: vẫn có kích thước cố định (`capacity`) — có thể Overflow nếu số phần tử vượt quá dự tính; cần cấp phát mảng động (tự mở rộng) nếu muốn linh hoạt hơn.

## Độ phức tạp

| Thao tác | Big-O |
|---|---|
| Enqueue | O(1) |
| Dequeue | O(1) |
| Front | O(1) |
| IsEmpty / IsFull | O(1) |

## Ví dụ

```csharp
class CircularQueue
{
    private int[] items;
    private int front = 0, count = 0;
    private readonly int capacity;

    public CircularQueue(int capacity)
    {
        this.capacity = capacity;
        items = new int[capacity];
    }

    public bool IsEmpty() => count == 0;
    public bool IsFull() => count == capacity;

    public void Enqueue(int x)
    {
        if (IsFull()) throw new InvalidOperationException("Queue overflow");
        int rearIndex = (front + count) % capacity;
        items[rearIndex] = x;
        count++;
    }

    public int Dequeue()
    {
        if (IsEmpty()) throw new InvalidOperationException("Queue underflow");
        int value = items[front];
        front = (front + 1) % capacity;
        count--;
        return value;
    }

    public int Front()
    {
        if (IsEmpty()) throw new InvalidOperationException("Queue underflow");
        return items[front];
    }
}
```

## Demo

Xem file [demo.html](./demo.html) — chọn dung lượng, thử Enqueue/Dequeue nhiều lần để thấy chỉ số "quay vòng" về đầu mảng, và các vị trí đã Dequeue được tái sử dụng.
