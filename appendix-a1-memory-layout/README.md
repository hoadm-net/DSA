# Phụ lục A1: Bố cục bộ nhớ của một chương trình

## Khái niệm

Khi một chương trình được nạp và chạy, hệ điều hành cấp cho nó một vùng không gian địa chỉ ảo (virtual address space), được chia thành các **segment (phân đoạn)** với vai trò khác nhau: **Text**, **Data**, **BSS**, **Heap** và **Stack**. Hiểu bố cục này giải thích *vì sao* biến cục bộ mất đi khi hàm kết thúc, *vì sao* con trỏ/tham chiếu vẫn truy cập được dữ liệu sau khi hàm gọi nó đã return, và *vì sao* đệ quy sâu gây "Stack Overflow" còn cấp phát runaway gây "hết bộ nhớ Heap".

## Giải thích chi tiết

### Các segment, theo thứ tự địa chỉ tăng dần

```
Địa chỉ thấp                                                    Địa chỉ cao
┌───────────┬───────────┬───────────┬───────────────┬───────────┐
│   Text    │   Data    │    BSS    │     Heap      │   Stack   │
│ (code)    │(khởi tạo) │(chưa k.t) │      ↓→        │    ←↑     │
└───────────┴───────────┴───────────┴───────────────┴───────────┘
                                      Heap lớn dần lên     Stack lớn dần xuống
                                      (địa chỉ tăng)        (địa chỉ giảm)
```

- **Text (Code segment)**: chứa mã lệnh (instructions) đã biên dịch của chương trình. Chỉ đọc (read-only) để tránh chương trình tự ý sửa mã đang chạy.
- **Data segment**: chứa **biến toàn cục (global)** và **biến static** đã được **khởi tạo giá trị cụ thể** (ví dụ `static int x = 5;`). Kích thước cố định, xác định lúc biên dịch.
- **BSS (Block Started by Symbol)**: chứa biến toàn cục/static **chưa khởi tạo** hoặc khởi tạo bằng 0 (ví dụ `static int y;`). Hệ điều hành chỉ cần nhớ kích thước, không cần lưu giá trị trong file thực thi → tiết kiệm dung lượng file.
- **Heap**: vùng nhớ **cấp phát động** lúc chạy (`new`, `malloc`, `List<T>`, object trong C#/Java...). Lập trình viên hoặc garbage collector chủ động cấp phát và giải phóng. Heap phát triển từ địa chỉ thấp lên địa chỉ cao.
- **Stack**: vùng nhớ cho **lời gọi hàm** — mỗi lần gọi hàm tạo một **stack frame** chứa tham số, biến cục bộ, địa chỉ trả về. Stack phát triển từ địa chỉ cao xuống địa chỉ thấp, hoạt động theo cơ chế **LIFO** (giống CTDL Stack đã học ở [32-stack-fundamentals](../32-stack-fundamentals/)).

### Stack hoạt động ra sao khi gọi hàm

Mỗi lần một hàm được gọi, một **stack frame** mới được đẩy (push) lên đỉnh stack, chứa:
1. Tham số truyền vào hàm.
2. Địa chỉ trả về (return address) — nơi tiếp tục thực thi sau khi hàm kết thúc.
3. Biến cục bộ khai báo bên trong hàm.

Khi hàm `return`, toàn bộ stack frame đó bị hủy (pop) — đây chính là lý do **biến cục bộ chỉ tồn tại trong phạm vi hàm**: vùng nhớ của nó bị thu hồi ngay khi hàm kết thúc.

Gọi hàm đệ quy (xem [07-algorithm-concepts-and-representation](../07-algorithm-concepts-and-representation/)) sẽ đẩy một stack frame mới cho mỗi lần gọi. Đệ quy không có điều kiện dừng (hoặc quá sâu) sẽ đẩy stack frame liên tục cho đến khi vượt quá kích thước Stack đã cấp → lỗi **Stack Overflow**.

### Heap hoạt động ra sao

Khi lập trình viên yêu cầu cấp phát động (`new Node()`, `malloc(...)`), vùng nhớ được lấy từ Heap và **tồn tại cho đến khi được giải phóng tường minh** (C/C++: `free`/`delete`) hoặc **không còn tham chiếu nào trỏ tới** (C#/Java/JS: garbage collector tự thu hồi). Vì vậy:
- Một **Node** của danh sách liên kết ([24-node-structure-and-list-types](../24-node-structure-and-list-types/)) được cấp phát trên Heap — nó vẫn tồn tại sau khi hàm tạo ra nó đã return, miễn còn biến nào (kể cả ở stack frame khác) giữ tham chiếu tới nó.
- Cấp phát Heap liên tục mà không giải phóng (hoặc không còn tham chiếu nào bị hủy do vòng tham chiếu chéo) gây **rò rỉ bộ nhớ (memory leak)**.

### So sánh Stack vs Heap

| Tiêu chí | Stack | Heap |
|---|---|---|
| Cấp phát | Tự động (compiler), khi hàm được gọi | Thủ công hoặc qua GC, khi lập trình viên yêu cầu |
| Giải phóng | Tự động, khi hàm return | Thủ công (`free`/`delete`) hoặc GC thu hồi |
| Tốc độ | Rất nhanh (chỉ dịch chuyển con trỏ đỉnh) | Chậm hơn (phải tìm khối trống phù hợp) |
| Kích thước | Giới hạn, cố định khi chương trình khởi động (vài MB) | Lớn, giới hạn bởi bộ nhớ hệ thống |
| Vòng đời dữ liệu | Theo phạm vi hàm (block scope) | Tùy ý, đến khi giải phóng/không còn tham chiếu |
| Lỗi thường gặp | Stack Overflow (đệ quy quá sâu) | Memory leak, Out of Memory |

### Vì sao chủ đề này quan trọng với CTDL

- **Mảng (Array)** khai báo cục bộ kích thước cố định thường nằm trên Stack; mảng động (`List<T>`, `int[]` cấp phát bằng `new`) nằm trên Heap.
- **Danh sách liên kết, cây, đồ thị** luôn dùng con trỏ/tham chiếu tới Node trên Heap — đây là lý do chúng linh hoạt về kích thước, khác với mảng.
- **Đệ quy** (dùng trong Quick Sort, Merge Sort, duyệt cây, Heapify...) tiêu tốn Stack theo độ sâu đệ quy — hiểu điều này giải thích tại sao một số giải thuật đệ quy cần chuyển sang dạng lặp khi dữ liệu lớn.

## Ví dụ

```csharp
using System;

class Program
{
    static int counter = 0;          // Data segment — biến static đã khởi tạo
    static int total;                // BSS segment — biến static chưa khởi tạo (mặc định 0)

    static int Square(int x)         // Text segment — mã lệnh của hàm Square
    {
        int result = x * x;          // biến cục bộ "result" nằm trên Stack (trong stack frame của Square)
        return result;
    }                                  // stack frame của Square bị hủy ngay khi return

    static void Main()
    {
        int a = 5;                    // biến cục bộ "a" trên Stack (trong stack frame của Main)
        int b = Square(a);            // gọi Square → đẩy thêm 1 stack frame, rồi pop khi xong

        int[] heapArray = new int[100];   // mảng cấp phát trên Heap, "heapArray" (con trỏ) nằm trên Stack

        Console.WriteLine(b);
    }
}
```

Minh họa trạng thái Stack tại thời điểm `Square(a)` đang thực thi (trước khi return):

```
Stack (địa chỉ cao → thấp)
┌─────────────────────────────┐
│ Stack frame: Square          │  ← đỉnh stack hiện tại
│   x = 5                      │
│   result = 25                │
│   địa chỉ trả về → Main      │
├─────────────────────────────┤
│ Stack frame: Main             │
│   a = 5                      │
│   b = (chưa gán, đang chờ)   │
│   heapArray = 0x7F3A... (con trỏ trỏ tới Heap)│
└─────────────────────────────┘

Heap
┌─────────────────────────────┐
│ int[100] tại địa chỉ 0x7F3A...│
└─────────────────────────────┘
```

## Demo

Xem file [demo.html](./demo.html) — nhập đoạn khai báo biến/lời gọi hàm đơn giản, xem trực quan biến được đặt vào segment nào (Text/Data/BSS/Heap/Stack), và mô phỏng từng bước Stack frame được push/pop khi gọi hàm lồng nhau hoặc đệ quy.
