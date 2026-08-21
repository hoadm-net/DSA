# Đánh giá độ phức tạp giải thuật

## Khái niệm

Độ phức tạp giải thuật (algorithm complexity) là thước đo lượng **tài nguyên** (thời gian xử lý, bộ nhớ sử dụng) mà giải thuật cần để chạy, biểu diễn dưới dạng hàm số của **kích thước dữ liệu đầu vào n**. Ký hiệu **Big-O** (O lớn) mô tả giới hạn trên (worst case/cận trên) của tốc độ tăng đó khi n tiến đến vô cùng.

## Giải thích chi tiết

### Vì sao không đo bằng giây thực tế?

Thời gian chạy thực tế phụ thuộc vào CPU, ngôn ngữ lập trình, trình biên dịch... nên không thể dùng để so sánh giải thuật một cách khách quan. Thay vào đó, ta đếm **số phép toán cơ bản** (so sánh, gán, cộng...) mà giải thuật thực hiện, biểu diễn theo n, rồi chỉ giữ lại **thành phần tăng nhanh nhất** khi n lớn, bỏ qua hằng số và các thành phần bậc thấp hơn.

Ví dụ: giải thuật thực hiện `3n² + 5n + 2` phép toán → độ phức tạp là **O(n²)** (bỏ hằng số 3, bỏ các số hạng bậc thấp hơn `5n + 2` vì khi n rất lớn chúng không đáng kể so với `n²`).

### Các mức Big-O phổ biến (từ nhanh đến chậm)

| Big-O | Tên gọi | Ví dụ giải thuật |
|---|---|---|
| O(1) | Hằng số | Truy xuất phần tử mảng theo chỉ số |
| O(log n) | Logarit | [Tìm kiếm nhị phân](../14-binary-search/) |
| O(n) | Tuyến tính | [Tìm kiếm tuần tự](../13-linear-search/) |
| O(n log n) | n-log-n | Merge Sort, Heap Sort, Quick Sort (trung bình) |
| O(n²) | Bình phương | Bubble Sort, Selection Sort, Insertion Sort |
| O(2ⁿ) | Mũ | Đệ quy tính dãy Fibonacci không tối ưu |

### Quy tắc cộng và quy tắc nhân

Khi phân tích một giải thuật gồm nhiều đoạn, dùng 2 quy tắc sau để suy ra độ phức tạp tổng:

**Quy tắc cộng** — áp dụng cho các đoạn thực hiện **tuần tự** (đoạn này xong mới đến đoạn kia):
```
Nếu đoạn 1 tốn O(f(n)), đoạn 2 tốn O(g(n))
=> Cả hai tốn O(f(n) + g(n)) = O(max(f(n), g(n)))
```

**Quy tắc nhân** — áp dụng cho các đoạn **lồng nhau** (vòng lặp trong vòng lặp):
```
Nếu vòng lặp ngoài chạy O(f(n)) lần, mỗi lần chạy vòng lặp trong tốn O(g(n))
=> Tổng cộng tốn O(f(n) × g(n))
```

### Best case, Average case, Worst case

Với nhiều giải thuật, độ phức tạp còn phụ thuộc vào **cách dữ liệu đầu vào được sắp xếp sẵn** — ví dụ Insertion Sort chạy O(n) nếu mảng đã gần như có thứ tự (best case) nhưng O(n²) nếu mảng bị đảo ngược hoàn toàn (worst case). Khi nói "độ phức tạp của giải thuật X", nếu không chú thích thêm, thường ngầm hiểu là **worst case** — để đảm bảo giải thuật hoạt động tốt trong mọi tình huống.

## Ví dụ

```
Đoạn code 1 (quy tắc cộng):
    for i = 1 to n: ...          // O(n)
    for j = 1 to n: ...          // O(n)
    => Tổng: O(n) + O(n) = O(n)

Đoạn code 2 (quy tắc nhân — vòng lặp lồng nhau):
    for i = 1 to n:               // chạy n lần
        for j = 1 to n: ...       // mỗi lần chạy n lần
    => Tổng: O(n) × O(n) = O(n²)  // đây là cấu trúc của Bubble/Selection Sort
```

## Demo

Xem file [demo.html](./demo.html) — biểu đồ trực quan so sánh tốc độ tăng của các mức Big-O khi n tăng dần, giúp thấy rõ khoảng cách giữa O(log n), O(n), O(n log n), O(n²), O(2ⁿ).
