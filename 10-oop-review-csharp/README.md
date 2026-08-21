# Ôn tập OOP trên C#

## Khái niệm

Lập trình hướng đối tượng (Object-Oriented Programming — OOP) là cách tổ chức chương trình xoay quanh khái niệm **đối tượng (object)** — thực thể gói gọn cả dữ liệu (thuộc tính) và hành vi (phương thức) liên quan đến dữ liệu đó. C# là ngôn ngữ được dùng để cài đặt các cấu trúc dữ liệu trong môn học này, nên cần nắm vững các khái niệm OOP nền tảng trước khi đi vào cài đặt.

## Giải thích chi tiết

### Class và Object

- **Class (lớp)**: là bản thiết kế/khuôn mẫu mô tả một loại đối tượng — gồm những thuộc tính (dữ liệu) nào và những phương thức (hành vi) nào.
- **Object (đối tượng)**: là một thực thể cụ thể được tạo ra (khởi tạo) từ một class, có giá trị dữ liệu riêng.

Quan hệ giữa class và object giống như quan hệ giữa "bản vẽ thiết kế nhà" (class) và "ngôi nhà cụ thể được xây" (object) — nhiều ngôi nhà (object) có thể được xây từ cùng một bản vẽ (class).

### Constructor (hàm khởi tạo)

Là phương thức đặc biệt, **tự động được gọi khi một object được tạo ra** bằng từ khóa `new`, dùng để thiết lập giá trị ban đầu cho các thuộc tính. Constructor có tên trùng với tên class và không có kiểu trả về.

### Thuộc tính (Property)

Property gói bọc quyền truy xuất tới một trường dữ liệu (field) của class, thông qua hai khối `get` (đọc giá trị) và `set` (gán giá trị) — cho phép kiểm soát cách dữ liệu được đọc/ghi từ bên ngoài (ví dụ: validate giá trị trước khi gán), thay vì để trường dữ liệu bị truy xuất trực tiếp, tự do.

### Access modifier (từ khóa truy xuất)

Quy định phạm vi mà một thành phần (trường, thuộc tính, phương thức) của class có thể được truy xuất từ bên ngoài:

| Từ khóa | Phạm vi truy xuất |
|---|---|
| `public` | Truy xuất được từ mọi nơi |
| `private` | Chỉ truy xuất được từ bên trong chính class đó |
| `protected` | Truy xuất được từ chính class và các class kế thừa (con) |
| `internal` | Truy xuất được trong cùng project/assembly |

Nguyên tắc phổ biến khi thiết kế class: **giấu (private) dữ liệu bên trong, chỉ mở (public) các phương thức/thuộc tính cần thiết** — đây chính là nguyên lý **đóng gói (encapsulation)**, một trong bốn trụ cột của OOP (cùng với **kế thừa** — inheritance, **đa hình** — polymorphism, và **trừu tượng hóa** — abstraction, khái niệm liên quan trực tiếp tới [ADT](../06-abstract-data-types/)).

## Ví dụ

```csharp
public class Stack
{
    // Trường dữ liệu: giấu kín (private), không cho truy xuất trực tiếp từ bên ngoài
    private int[] items;
    private int top;

    // Property: cho phép đọc (get) số lượng phần tử, không cho gán trực tiếp
    public int Count
    {
        get { return top + 1; }
    }

    // Constructor: thiết lập giá trị ban đầu khi tạo object
    public Stack(int capacity)
    {
        items = new int[capacity];
        top = -1;
    }

    // Phương thức public: hành vi được phép gọi từ bên ngoài
    public void Push(int value)
    {
        top++;
        items[top] = value;
    }
}

// Sử dụng: tạo object cụ thể từ class Stack
Stack myStack = new Stack(10); // gọi constructor
myStack.Push(5);
Console.WriteLine(myStack.Count); // đọc qua property, không đụng trực tiếp vào "top"
```
