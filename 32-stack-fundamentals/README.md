# Khái niệm Stack (LIFO) & các thao tác

## Khái niệm

Stack (ngăn xếp) là một [kiểu dữ liệu trừu tượng (ADT)](../06-abstract-data-types/) tuyến tính, trong đó việc thêm và loại bỏ phần tử chỉ được thực hiện ở **một đầu duy nhất**, gọi là **đỉnh (top)**. Nguyên tắc hoạt động của Stack là **LIFO — Last In, First Out** (vào sau ra trước): phần tử được thêm vào sau cùng sẽ là phần tử được lấy ra đầu tiên.

## Giải thích chi tiết

### Hình ảnh trực quan

Stack hoạt động giống một chồng đĩa: đĩa nào được đặt lên sau cùng sẽ là đĩa đầu tiên được lấy ra; muốn lấy đĩa ở dưới cùng, phải lấy hết các đĩa phía trên trước.

### Các thao tác cơ bản

| Thao tác | Ý nghĩa |
|---|---|
| `Push(x)` | Thêm phần tử `x` vào đỉnh stack |
| `Pop()` | Lấy và loại bỏ phần tử ở đỉnh stack |
| `Top()` / `Peek()` | Xem giá trị phần tử ở đỉnh mà **không** loại bỏ nó |
| `IsEmpty()` | Kiểm tra stack có rỗng hay không |
| `IsFull()` | (nếu cài đặt bằng mảng có giới hạn) kiểm tra stack đã đầy chưa |

Đây là đặc tả ADT của Stack — hoàn toàn không quan tâm việc cài đặt bên trong dùng mảng hay danh sách liên kết (xem [Cài đặt Stack bằng mảng](../33-stack-array-implementation/) và [Cài đặt Stack bằng danh sách liên kết](../34-stack-linked-list-implementation/)).

### Các trường hợp đặc biệt

- **Stack rỗng (Underflow)**: gọi `Pop()` hoặc `Top()` khi stack không có phần tử nào → lỗi, cần kiểm tra `IsEmpty()` trước khi thao tác.
- **Stack đầy (Overflow)**: chỉ xảy ra với cài đặt bằng mảng có giới hạn kích thước cố định — gọi `Push()` khi đã đầy → lỗi, cần kiểm tra `IsFull()` trước khi thêm.

### Ứng dụng thực tế

Stack là một trong những cấu trúc dữ liệu được dùng nhiều nhất trong khoa học máy tính:

- **Ngăn xếp lời gọi hàm (call stack)**: mỗi lần gọi hàm, thông tin về hàm (biến cục bộ, địa chỉ trả về) được đẩy vào stack; khi hàm kết thúc, thông tin đó được lấy ra — đây cũng chính là cơ chế cho phép **đệ quy** hoạt động (xem [Ứng dụng: khử đệ quy](../36-stack-application-recursion-removal/)).
- **Tính giá trị biểu thức**: chuyển đổi và tính biểu thức toán học (xem [Ứng dụng: Infix ↔ Postfix](../35-stack-application-expression-evaluation/)).
- **Chức năng Undo/Redo** trong các phần mềm soạn thảo.
- **Kiểm tra dấu ngoặc cân bằng** trong biểu thức hoặc mã nguồn.
- **Duyệt đồ thị/cây theo chiều sâu (DFS)**.

## Ví dụ

```
Thực hiện lần lượt: Push(5), Push(8), Push(3), Pop(), Push(9), Pop(), Pop()

Bước           Trạng thái Stack (đỉnh ở bên phải)     Kết quả
Push(5)        [5]
Push(8)        [5, 8]
Push(3)        [5, 8, 3]
Pop()          [5, 8]                                  trả về 3
Push(9)        [5, 8, 9]
Pop()          [5, 8]                                  trả về 9
Pop()          [5]                                     trả về 8
```
