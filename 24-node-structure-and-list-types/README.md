# Cấu tạo Node & các loại hình danh sách liên kết

## Khái niệm

Node là đơn vị cơ bản cấu thành danh sách liên kết, gồm hai thành phần: **dữ liệu (data)** và **con trỏ liên kết (link)** trỏ tới node khác. Tùy vào số lượng và chiều của con trỏ liên kết, danh sách liên kết được chia thành nhiều loại hình khác nhau.

## Giải thích chi tiết

### Cấu tạo một Node (danh sách liên kết đơn)

```csharp
class Node
{
    public int Data;      // dữ liệu lưu trữ tại node
    public Node Next;     // con trỏ trỏ tới node kế tiếp (null nếu là node cuối)
}
```

Một node có thể lưu dữ liệu đơn giản (số nguyên, chuỗi...) hoặc dữ liệu có cấu trúc (struct/object nhiều trường, xem [Kiểu dữ liệu có cấu trúc](../05-structured-data-types/)).

### Các loại hình danh sách liên kết

**1. Danh sách liên kết đơn (Singly Linked List)**

Mỗi node chỉ có **một** con trỏ `Next` trỏ tới node kế tiếp. Chỉ duyệt được theo **một chiều** (từ đầu đến cuối). Đây là loại cơ bản nhất, được trình bày chi tiết ở các bài [Khởi tạo & duyệt](../25-singly-linked-list-init-and-traverse/), [Thêm node](../26-insert-node-at-head-tail/), [Chèn node](../27-insert-node-by-position/), [Xóa node](../28-delete-node/).

```
[data|next]->[data|next]->[data|next]->NULL
```

**2. Danh sách liên kết đôi (Doubly Linked List)**

Mỗi node có **hai** con trỏ: `Next` (trỏ tới node kế tiếp) và `Prev` (trỏ tới node trước đó). Cho phép duyệt **cả hai chiều**, và việc xóa một node khi đã có con trỏ tới nó trở nên đơn giản hơn (không cần tìm node trước đó bằng cách duyệt lại từ đầu). Đổi lại tốn thêm bộ nhớ cho con trỏ `Prev` ở mỗi node. Xem thêm ở [Danh sách liên kết đôi](../30-doubly-linked-list/).

```
NULL<-[prev|data|next]<->[prev|data|next]<->[prev|data|next]->NULL
```

**3. Danh sách liên kết vòng (Circular Linked List)**

Node cuối cùng, thay vì trỏ tới `NULL`, lại trỏ **quay về node đầu tiên** — tạo thành một vòng khép kín. Có thể áp dụng cho cả danh sách đơn lẫn danh sách đôi. Phù hợp với các bài toán có tính chất tuần hoàn (ví dụ lịch chạy vòng round-robin). Xem thêm ở [Danh sách liên kết vòng](../31-circular-linked-list/).

```
[data|next]->[data|next]->[data|next]-+
     ^_______________________________|
```

### Bảng so sánh nhanh

| Loại | Số con trỏ/node | Duyệt | Ghi chú |
|---|---|---|---|
| Đơn | 1 (Next) | Một chiều | Đơn giản, tiết kiệm bộ nhớ nhất |
| Đôi | 2 (Next, Prev) | Hai chiều | Xóa node dễ hơn, tốn thêm bộ nhớ |
| Vòng | 1 hoặc 2 | Một/hai chiều, quay vòng | Không có node cuối trỏ NULL |

## Ví dụ

```
Danh sách liên kết đơn biểu diễn [5, 8, 3]:

  head
   |
   v
 [5|•]--->[8|•]--->[3|NULL]

Trong đó mỗi ô "[data|•]" là một Node, "•" là con trỏ Next
trỏ sang node kế tiếp, "NULL" đánh dấu hết danh sách.
```
