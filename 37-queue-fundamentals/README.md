# Khái niệm Queue (FIFO) & các thao tác

## Khái niệm

Queue (hàng đợi) là một [kiểu dữ liệu trừu tượng (ADT)](../06-abstract-data-types/) tuyến tính, trong đó phần tử được **thêm vào ở một đầu (rear/tail — cuối hàng đợi)** và **lấy ra ở đầu kia (front/head — đầu hàng đợi)**. Nguyên tắc hoạt động của Queue là **FIFO — First In, First Out** (vào trước ra trước).

## Giải thích chi tiết

### Hình ảnh trực quan

Queue hoạt động giống hàng người xếp hàng chờ mua vé: ai đến trước (xếp vào cuối hàng trước) sẽ được phục vụ trước (ra khỏi đầu hàng trước) — trái ngược hoàn toàn với nguyên tắc LIFO của [Stack](../32-stack-fundamentals/).

### Các thao tác cơ bản

| Thao tác | Ý nghĩa |
|---|---|
| `Enqueue(x)` | Thêm phần tử `x` vào **cuối** hàng đợi (rear) |
| `Dequeue()` | Lấy và loại bỏ phần tử ở **đầu** hàng đợi (front) |
| `Front()` | Xem giá trị phần tử ở đầu hàng đợi mà **không** loại bỏ nó |
| `IsEmpty()` | Kiểm tra hàng đợi có rỗng hay không |
| `IsFull()` | (nếu cài đặt bằng mảng có giới hạn) kiểm tra hàng đợi đã đầy chưa |

### So sánh Stack và Queue

| | Stack (LIFO) | Queue (FIFO) |
|---|---|---|
| Thêm vào | Một đầu (top) | Một đầu (rear) |
| Lấy ra | Cùng đầu đó (top) | Đầu còn lại (front) |
| Phần tử ra trước | Phần tử **mới nhất** | Phần tử **cũ nhất** |
| Ví dụ đời thực | Chồng đĩa | Hàng người xếp hàng |

### Các trường hợp đặc biệt

Giống Stack, Queue cũng có hai trường hợp lỗi cần kiểm tra trước khi thao tác:
- **Underflow**: gọi `Dequeue()` hoặc `Front()` khi hàng đợi rỗng.
- **Overflow**: gọi `Enqueue()` khi hàng đợi đã đầy (chỉ xảy ra với cài đặt bằng mảng có giới hạn kích thước, xem [Cài đặt Queue bằng mảng](../38-queue-array-implementation/)).

### Ứng dụng thực tế

- **Bộ đệm (buffer)**: dữ liệu đến từ bàn phím, mạng, máy in... được xếp vào hàng đợi và xử lý lần lượt đúng thứ tự đến.
- **Quản lý tiến trình (process scheduling)**: hệ điều hành xếp các tiến trình chờ CPU vào hàng đợi, xử lý lần lượt (ví dụ giải thuật Round-Robin, xem [Ứng dụng Queue](../40-queue-applications/)).
- **Duyệt theo chiều rộng (BFS)** trên cây/đồ thị.
- **Hàng đợi tin nhắn (message queue)** trong hệ thống phân tán.

## Ví dụ

```
Thực hiện lần lượt: Enqueue(5), Enqueue(8), Enqueue(3), Dequeue(), Enqueue(9), Dequeue()

Bước             Trạng thái Queue (front bên trái, rear bên phải)   Kết quả
Enqueue(5)       [5]
Enqueue(8)       [5, 8]
Enqueue(3)       [5, 8, 3]
Dequeue()        [8, 3]                                              trả về 5
Enqueue(9)       [8, 3, 9]
Dequeue()        [3, 9]                                              trả về 8
```
