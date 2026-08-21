# Danh sách liên kết đôi (giới thiệu)

## Khái niệm

Danh sách liên kết đôi (doubly linked list) là danh sách liên kết mà mỗi node có **hai con trỏ liên kết**: `Next` (trỏ tới node kế tiếp, giống danh sách đơn) và `Prev` (trỏ tới node đứng trước). Nhờ vậy, danh sách có thể được duyệt theo **cả hai chiều**.

## Giải thích chi tiết

### Cấu tạo Node

```csharp
class DNode
{
    public int Data;
    public DNode Next;    // trỏ tới node kế tiếp
    public DNode Prev;    // trỏ tới node đứng trước
}
```

Node đầu tiên có `Prev = NULL`, node cuối cùng có `Next = NULL`.

### Ưu điểm so với danh sách liên kết đơn

1. **Duyệt được hai chiều**: có thể đi từ đầu tới cuối hoặc từ cuối về đầu, hữu ích khi cần truy cập phần tử "trước đó" mà không phải duyệt lại từ head.
2. **Xóa một node dễ dàng hơn khi đã có con trỏ tới nó**: với danh sách đơn, muốn xóa node `curr` phải duyệt từ đầu để tìm `prev` (O(n)); với danh sách đôi, `curr.Prev` đã có sẵn, chỉ cần cập nhật liên kết trực tiếp (O(1)) — xem ví dụ bên dưới.
3. Cho phép cài đặt hiệu quả các cấu trúc cần duyệt ngược, ví dụ lịch sử "Back/Forward" của trình duyệt web.

### Đánh đổi

- Tốn thêm bộ nhớ cho con trỏ `Prev` ở mỗi node.
- Các thao tác thêm/xóa phải **cập nhật đồng thời cả hai con trỏ** `Next` và `Prev` — dễ sai sót hơn nếu cài đặt thủ công, cần cẩn thận về thứ tự các phép gán.

### Thêm node vào đầu danh sách liên kết đôi

```
newNode.Next = head
newNode.Prev = NULL
IF head != NULL THEN
    head.Prev = newNode
END IF
head = newNode
```

### Xóa một node khi đã có con trỏ tới nó (ưu điểm nổi bật)

```
FUNCTION DeleteNode(node)
    IF node.Prev != NULL THEN
        node.Prev.Next = node.Next
    ELSE
        head = node.Next        // node là head
    END IF
    IF node.Next != NULL THEN
        node.Next.Prev = node.Prev
    END IF
END FUNCTION
```
So với danh sách đơn (phải duyệt tìm `prev` trước khi xóa, xem [Xóa node](../28-delete-node/)), ở đây không cần duyệt gì cả — chi phí xóa chỉ còn **O(1)** nếu đã có sẵn con trỏ tới node cần xóa.

## Độ phức tạp

| Thao tác | Danh sách đơn | Danh sách đôi |
|---|---|---|
| Duyệt xuôi | O(n) | O(n) |
| Duyệt ngược | Không hỗ trợ trực tiếp | O(n) |
| Xóa node (đã có con trỏ tới node) | O(n) (phải tìm `prev`) | O(1) |
| Bộ nhớ phụ mỗi node | 1 con trỏ | 2 con trỏ |

## Demo

Xem file [demo.html](./demo.html) — khởi tạo danh sách liên kết đôi, dùng con trỏ `p` duyệt xuôi (theo `Next`) hoặc duyệt ngược (theo `Prev`) để thấy rõ khả năng đi hai chiều.
