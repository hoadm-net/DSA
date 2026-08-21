# Xóa node khỏi danh sách

## Khái niệm

Xóa node là thao tác loại bỏ một node khỏi danh sách liên kết bằng cách **cập nhật lại liên kết** của node đứng trước nó, bỏ qua node cần xóa — không cần dịch chuyển bất kỳ phần tử nào khác như khi xóa trong mảng.

## Giải thích chi tiết

Xóa node trong danh sách liên kết đơn cần xét **ba trường hợp** theo vị trí node cần xóa:

### Trường hợp 1 — Xóa node đầu (head)

```
head = head.Next
```
Chỉ cần cập nhật `head` trỏ sang node kế tiếp. Node cũ không còn được tham chiếu bởi ai, sẽ được thu hồi bộ nhớ (garbage collected, với các ngôn ngữ có GC như C#).

### Trường hợp 2 — Xóa node ở giữa

Cần **duyệt để tìm node đứng trước** (`prev`) node cần xóa (`curr`), sau đó:
```
prev.Next = curr.Next
```
`prev` "nhảy qua" `curr`, trỏ thẳng tới node kế tiếp của `curr` — loại `curr` ra khỏi chuỗi liên kết.

### Trường hợp 3 — Xóa node cuối

Về bản chất là một dạng đặc biệt của trường hợp 2: tìm `prev` là node đứng trước node cuối, rồi gán `prev.Next = NULL`.

### Thuật toán tổng quát (xóa theo giá trị)

1. Nếu danh sách rỗng: không có gì để xóa.
2. Nếu `head.Data == value`: xóa node đầu (trường hợp 1), kết thúc.
3. Ngược lại: dùng hai con trỏ `prev` và `curr`, cùng duyệt (`prev` đi sau `curr` một node) cho đến khi `curr.Data == value` hoặc `curr == NULL`.
4. Nếu tìm thấy (`curr != NULL`): gán `prev.Next = curr.Next` (áp dụng cho cả trường hợp 2 và 3).
5. Nếu không tìm thấy (`curr == NULL`): giá trị không tồn tại trong danh sách.

**So sánh với xóa trong mảng**: xóa một phần tử ở giữa mảng cần **dịch chuyển tất cả phần tử phía sau lên một vị trí** (O(n) phép dịch chuyển); xóa node trong danh sách liên kết chỉ cần **một phép gán con trỏ** (O(1)) sau khi đã tìm được vị trí — chi phí O(n) chỉ nằm ở bước *tìm kiếm*, không phải ở bước *xóa*.

## Độ phức tạp

| Thao tác | Big-O |
|---|---|
| Xóa node đầu (đã biết head) | O(1) |
| Tìm kiếm node cần xóa (theo giá trị) | O(n) |
| Xóa khi đã có con trỏ `prev` | O(1) |
| **Tổng cộng xóa theo giá trị** | **O(n)** |

## Ví dụ

```
FUNCTION DeleteByValue(head, value)
    IF head == NULL THEN
        RETURN head              // danh sách rỗng
    END IF
    IF head.Data == value THEN
        RETURN head.Next          // xóa node đầu
    END IF
    prev = head
    curr = head.Next
    WHILE curr != NULL AND curr.Data != value
        prev = curr
        curr = curr.Next
    END WHILE
    IF curr != NULL THEN
        prev.Next = curr.Next     // xóa node giữa/cuối
    END IF
    RETURN head
END FUNCTION
```

```csharp
Node DeleteByValue(Node head, int value)
{
    if (head == null) return head;
    if (head.Data == value) return head.Next;

    Node prev = head, curr = head.Next;
    while (curr != null && curr.Data != value)
    {
        prev = curr;
        curr = curr.Next;
    }
    if (curr != null)
    {
        prev.Next = curr.Next;
    }
    return head;
}
```

## Demo

Xem file [demo.html](./demo.html) — khởi tạo danh sách, nhập giá trị cần xóa, chạy từng bước để xem hai con trỏ `prev`/`curr` cùng duyệt tìm node cần xóa rồi "nhảy qua" nó.
