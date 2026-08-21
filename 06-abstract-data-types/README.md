# Trừu tượng hóa dữ liệu (ADT)

## Khái niệm

Kiểu dữ liệu trừu tượng (Abstract Data Type — ADT) là một mô hình toán học mô tả **dữ liệu cùng tập các thao tác trên dữ liệu đó**, hoàn toàn tách biệt với cách nó được cài đặt cụ thể bên trong (bằng mảng, danh sách liên kết, hay bất kỳ CTDL nào khác).

## Giải thích chi tiết

ADT gồm hai phần:

1. **Đặc tả (specification)** — "cái gì": định nghĩa dữ liệu gồm những gì và có những thao tác nào được phép thực hiện trên dữ liệu đó, cùng ý nghĩa/hành vi của mỗi thao tác. Đây là phần **giao diện (interface)** mà người dùng ADT nhìn thấy.
2. **Cài đặt (implementation)** — "như thế nào": cách hiện thực hóa dữ liệu và các thao tác đó bằng một CTDL cụ thể (mảng, danh sách liên kết...). Đây là phần **bị che giấu** (ẩn tàng — encapsulation) khỏi người dùng.

Nguyên tắc cốt lõi của ADT: **người dùng chỉ cần biết ADT làm được gì (thông qua các thao tác), không cần biết nó làm điều đó bằng cách nào**. Nhờ vậy:

- Có thể **thay đổi cách cài đặt bên trong** (ví dụ đổi từ mảng sang danh sách liên kết) mà không ảnh hưởng đến code đang sử dụng ADT đó, miễn là tập thao tác và hành vi giữ nguyên.
- Giảm độ phức tạp khi thiết kế hệ thống lớn: mỗi ADT là một "hộp đen" độc lập.

Ví dụ kinh điển về ADT: **Stack** (xem [Khái niệm Stack](../32-stack-fundamentals/)) được đặc tả bởi các thao tác `Push`, `Pop`, `Top`, `IsEmpty` cùng nguyên tắc "vào sau ra trước" (LIFO) — hoàn toàn không quan tâm Stack được cài đặt bằng mảng hay danh sách liên kết.

| | Kiểu dữ liệu có cấu trúc | Kiểu dữ liệu trừu tượng (ADT) |
|---|---|---|
| Trọng tâm | Cách tổ chức dữ liệu | Hành vi (thao tác) trên dữ liệu |
| Cài đặt | Là một phần định nghĩa | Bị che giấu, có thể thay đổi tự do |
| Ví dụ | mảng, struct | Stack, Queue, List, Set, Map |

## Ví dụ

```
Đặc tả ADT "Danh sách" (List) — không quan tâm cài đặt bên trong:
  - Init()          : khởi tạo danh sách rỗng
  - IsEmpty()        : kiểm tra danh sách có rỗng không
  - Insert(x, pos)   : chèn phần tử x vào vị trí pos
  - Delete(pos)      : xóa phần tử tại vị trí pos
  - Get(pos)         : lấy giá trị phần tử tại vị trí pos

Cùng một đặc tả ADT "Danh sách" này có thể cài đặt bằng:
  - Mảng động        -> Get(pos) nhanh O(1), Insert ở giữa chậm O(n)
  - Danh sách liên kết -> Get(pos) chậm O(n), Insert khi đã có vị trí nhanh O(1)

Người dùng ADT chỉ gọi Insert/Delete/Get, không cần sửa code
khi đội phát triển đổi cài đặt bên trong từ mảng sang danh sách liên kết.
```
