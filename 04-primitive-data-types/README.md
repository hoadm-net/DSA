# Kiểu dữ liệu cơ bản

## Khái niệm

Kiểu dữ liệu cơ bản (primitive data type) là các kiểu dữ liệu đơn giản nhất, được ngôn ngữ lập trình hỗ trợ sẵn, lưu trữ một giá trị đơn lẻ và không thể chia nhỏ thành các thành phần có ý nghĩa hơn.

## Giải thích chi tiết

Các kiểu dữ liệu cơ bản phổ biến:

| Kiểu | Ý nghĩa | Ví dụ (C#) | Kích thước điển hình |
|---|---|---|---|
| Số nguyên (integer) | Số không có phần thập phân | `int`, `long`, `short`, `byte` | 1–8 byte |
| Số thực (floating-point) | Số có phần thập phân | `float`, `double`, `decimal` | 4–16 byte |
| Ký tự (character) | Một ký tự đơn | `char` | 2 byte (Unicode) |
| Luận lý (boolean) | Giá trị đúng/sai | `bool` | 1 byte |

Đặc điểm chung của kiểu dữ liệu cơ bản:

- **Kích thước cố định**: mỗi kiểu chiếm một số byte bộ nhớ xác định, biết trước tại thời điểm biên dịch.
- **Lưu trực tiếp giá trị**: biến kiểu cơ bản lưu trực tiếp giá trị trong vùng nhớ của nó (không giống kiểu tham chiếu lưu địa chỉ).
- **Có sẵn các phép toán nguyên thủy**: cộng, trừ, nhân, chia, so sánh... được ngôn ngữ hỗ trợ trực tiếp, không cần định nghĩa thêm.
- **Là "viên gạch" xây dựng nên kiểu dữ liệu có cấu trúc**: mảng, struct, class đều được xây dựng từ tổ hợp các kiểu dữ liệu cơ bản (xem [Kiểu dữ liệu có cấu trúc](../05-structured-data-types/)).

Mỗi kiểu có một **miền giá trị** (range) giới hạn — ví dụ `int` trong C# lưu được từ -2,147,483,648 đến 2,147,483,647. Khi giá trị vượt miền này sẽ xảy ra hiện tượng tràn số (overflow), đây là điều lập trình viên cần lưu ý khi chọn kiểu dữ liệu phù hợp với miền giá trị thực tế của bài toán.

## Ví dụ

```csharp
int soLuong = 25;          // số nguyên
double diemTrungBinh = 8.5; // số thực
char loaiHang = 'A';        // ký tự
bool conHang = true;        // luận lý

// Chọn kiểu phù hợp với miền giá trị thực tế:
byte tuoi = 20;      // đủ dùng, tiết kiệm bộ nhớ hơn int (1 byte vs 4 byte)
long danSo = 8_000_000_000; // vượt miền int, cần long
```
