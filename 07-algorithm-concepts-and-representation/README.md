# Khái niệm giải thuật & các cách mô tả

## Khái niệm

Giải thuật (algorithm) là một dãy hữu hạn các bước (thao tác) được sắp xếp theo một trình tự xác định, nhằm giải quyết một bài toán cụ thể, biến đổi dữ liệu đầu vào (input) thành kết quả đầu ra (output) mong muốn.

## Giải thích chi tiết

Giải thuật là "công thức xử lý" độc lập với ngôn ngữ lập trình — cùng một giải thuật có thể cài đặt bằng C#, Python, Java... Có ba cách mô tả giải thuật phổ biến, mỗi cách phù hợp với mục đích khác nhau:

### 1. Ngôn ngữ tự nhiên (mã tự nhiên)

Diễn đạt các bước giải thuật bằng câu văn thông thường (tiếng Việt, tiếng Anh...).

- **Ưu điểm**: dễ hiểu với người không chuyên, không cần biết cú pháp lập trình.
- **Nhược điểm**: dài dòng, dễ mơ hồ, khó chuyển trực tiếp thành code.

### 2. Mã giả (pseudo-code)

Diễn đạt các bước bằng cú pháp "giống ngôn ngữ lập trình" nhưng không tuân theo quy tắc cú pháp chặt chẽ của một ngôn ngữ cụ thể nào — dùng các từ khóa như `if`, `while`, `for`, `return` kết hợp ngôn ngữ tự nhiên.

- **Ưu điểm**: ngắn gọn, rõ ràng về trình tự và logic, dễ chuyển thành code thật ở bất kỳ ngôn ngữ nào.
- **Nhược điểm**: cần người đọc có nền tảng lập trình cơ bản.
- Đây là cách mô tả **phổ biến nhất** trong giảng dạy và tài liệu kỹ thuật.

### 3. Lưu đồ (flowchart)

Diễn đạt bằng sơ đồ khối, dùng các hình khối chuẩn để biểu diễn từng loại thao tác:

| Hình khối | Ý nghĩa |
|---|---|
| Hình oval (bo tròn) | Điểm bắt đầu / kết thúc |
| Hình chữ nhật | Một thao tác xử lý |
| Hình thoi | Điểm rẽ nhánh (kiểm tra điều kiện) |
| Hình bình hành | Nhập/xuất dữ liệu |
| Mũi tên | Hướng thực hiện tiếp theo |

- **Ưu điểm**: trực quan, dễ nhìn thấy toàn bộ luồng xử lý và các nhánh rẽ cùng lúc.
- **Nhược điểm**: cồng kềnh với giải thuật phức tạp, khó thể hiện chi tiết tính toán.

## Ví dụ

Bài toán: Tìm số lớn nhất trong 2 số a, b.

**Ngôn ngữ tự nhiên:**
> So sánh a và b. Nếu a lớn hơn b thì kết quả là a, ngược lại kết quả là b.

**Mã giả:**
```
FUNCTION Max(a, b)
    IF a > b THEN
        RETURN a
    ELSE
        RETURN b
    END IF
END FUNCTION
```

**Lưu đồ (mô tả bằng văn bản):**
```
[Bắt đầu] -> [Nhập a, b] -> <a > b?> --Đúng--> [Kết quả = a] -> [Kết thúc]
                                  |
                                Sai
                                  v
                          [Kết quả = b] -> [Kết thúc]
```
