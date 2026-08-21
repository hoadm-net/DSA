# Kiểu dữ liệu có cấu trúc

## Khái niệm

Kiểu dữ liệu có cấu trúc (structured data type) là kiểu dữ liệu được xây dựng bằng cách tổ hợp nhiều [kiểu dữ liệu cơ bản](../04-primitive-data-types/) (hoặc kiểu có cấu trúc khác) lại với nhau theo một quy tắc tổ chức nhất định, tạo thành một đơn vị dữ liệu lớn hơn, phức tạp hơn.

## Giải thích chi tiết

Hai dạng kiểu dữ liệu có cấu trúc nền tảng nhất:

### Mảng (Array)

Tập hợp **hữu hạn các phần tử cùng kiểu**, được lưu liên tục trong bộ nhớ và truy xuất thông qua chỉ số (index).

- Truy xuất trực tiếp theo chỉ số: O(1), vì địa chỉ phần tử thứ `i` tính được bằng `địa_chỉ_đầu + i * kích_thước_phần_tử`.
- Kích thước thường cố định khi khai báo (mảng tĩnh); một số ngôn ngữ hỗ trợ mảng động (tự mở rộng khi cần, ví dụ `List<T>` trong C#).
- Thêm/xóa phần tử ở giữa mảng tốn chi phí O(n) vì phải dịch chuyển các phần tử phía sau.

### Bản ghi/Struct (Record)

Tập hợp **các phần tử có thể khác kiểu nhau**, mỗi phần tử được gọi là một trường (field), gộp chung lại để mô tả một thực thể trong thực tế.

- Mỗi trường được truy xuất qua tên, không qua chỉ số.
- Dùng để mô hình hóa các đối tượng có nhiều thuộc tính khác kiểu (ví dụ: một sinh viên có mã số (chuỗi), tên (chuỗi), điểm (số thực), đã tốt nghiệp (luận lý)).
- Là tiền thân của khái niệm `class`/`object` trong lập trình hướng đối tượng (xem [Ôn tập OOP trên C#](../10-oop-review-csharp/)).

### So sánh Mảng và Struct

| Tiêu chí | Mảng | Struct |
|---|---|---|
| Kiểu phần tử | Cùng kiểu | Có thể khác kiểu |
| Truy xuất | Theo chỉ số | Theo tên trường |
| Mục đích | Tập hợp nhiều giá trị đồng nhất | Mô tả một thực thể nhiều thuộc tính |

Trong thực tế, hai kiểu này thường **kết hợp với nhau**: mảng các struct (ví dụ mảng sinh viên) hoặc struct chứa mảng bên trong (ví dụ struct lớp học chứa mảng điểm).

## Ví dụ

```csharp
// Mảng: tập hợp các phần tử cùng kiểu
int[] diemThi = new int[5] { 8, 7, 9, 6, 10 };

// Struct: tổ hợp nhiều trường khác kiểu, mô tả một thực thể
struct SinhVien
{
    public string MaSo;
    public string HoTen;
    public double DiemTrungBinh;
}

// Kết hợp: mảng các struct
SinhVien[] danhSachSV = new SinhVien[100];
danhSachSV[0].MaSo = "SV001";
danhSachSV[0].HoTen = "Nguyen Van A";
danhSachSV[0].DiemTrungBinh = 8.5;
```
