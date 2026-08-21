# Cài đặt Stack bằng mảng

## Khái niệm

Cách cài đặt Stack đơn giản và phổ biến nhất là dùng một mảng có kích thước cố định (`capacity`), cùng một biến `top` lưu **chỉ số của phần tử ở đỉnh stack**.

## Giải thích chi tiết

### Cấu trúc dữ liệu

```csharp
class ArrayStack
{
    private int[] items;
    private int top;       // chỉ số phần tử đỉnh; top = -1 nghĩa là stack rỗng
    private int capacity;
}
```

Quy ước: `top = -1` khi stack rỗng. Mỗi lần `Push`, `top` tăng lên 1 rồi ghi giá trị vào `items[top]`. Mỗi lần `Pop`, lấy giá trị tại `items[top]` rồi giảm `top` đi 1 (không cần xóa giá trị cũ trong mảng, chỉ cần "quên" nó bằng cách giảm `top`).

### Cài đặt các thao tác

- **Push(x)**: nếu `top == capacity - 1` (đầy) → báo lỗi Overflow; ngược lại `top++; items[top] = x;`
- **Pop()**: nếu `top == -1` (rỗng) → báo lỗi Underflow; ngược lại lấy `items[top]`, sau đó `top--`.
- **Top()**: nếu `top == -1` → báo lỗi; ngược lại trả về `items[top]` (không đổi `top`).
- **IsEmpty()**: trả về `top == -1`.
- **IsFull()**: trả về `top == capacity - 1`.

### Ưu điểm và nhược điểm

**Ưu điểm**: cài đặt đơn giản, mọi thao tác đều O(1), tận dụng tốt bộ nhớ đệm (cache) vì dữ liệu liên tục.

**Nhược điểm**: kích thước cố định — nếu `capacity` đặt quá nhỏ sẽ bị Overflow khi cần nhiều phần tử hơn; nếu đặt quá lớn sẽ lãng phí bộ nhớ. Có thể khắc phục bằng mảng động (tự cấp phát lại mảng lớn hơn khi đầy, giống `List<T>` trong C#), nhưng khi đó chi phí `Push` thỉnh thoảng sẽ là O(n) thay vì O(1) (mỗi lần cấp phát lại và sao chép toàn bộ phần tử).

## Độ phức tạp

| Thao tác | Big-O |
|---|---|
| Push | O(1) |
| Pop | O(1) |
| Top | O(1) |
| IsEmpty / IsFull | O(1) |

## Ví dụ

```csharp
class ArrayStack
{
    private int[] items;
    private int top = -1;

    public ArrayStack(int capacity) { items = new int[capacity]; }

    public bool IsEmpty() => top == -1;
    public bool IsFull() => top == items.Length - 1;

    public void Push(int x)
    {
        if (IsFull()) throw new InvalidOperationException("Stack overflow");
        items[++top] = x;
    }

    public int Pop()
    {
        if (IsEmpty()) throw new InvalidOperationException("Stack underflow");
        return items[top--];
    }

    public int Top()
    {
        if (IsEmpty()) throw new InvalidOperationException("Stack underflow");
        return items[top];
    }
}
```

## Demo

Xem file [demo.html](./demo.html) — chọn dung lượng stack, thử Push/Pop/Top và quan sát con trỏ `top` cùng các trường hợp Overflow/Underflow.
