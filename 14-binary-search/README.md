# Tìm kiếm nhị phân (Binary Search)

## Khái niệm

Tìm kiếm nhị phân là giải thuật tìm kiếm hiệu quả áp dụng trên **dãy dữ liệu đã được sắp xếp**, dựa trên nguyên lý "chia để trị" (divide and conquer): so sánh khóa cần tìm với phần tử ở giữa dãy, từ đó **loại bỏ ngay một nửa** phạm vi tìm kiếm sau mỗi lần so sánh.

## Giải thích chi tiết

Ý tưởng: xét đoạn tìm kiếm hiện tại từ vị trí `low` đến `high` (ban đầu là toàn bộ dãy). Lặp lại:

1. Tính vị trí giữa `mid = (low + high) / 2`.
2. So sánh `A[mid]` với khóa `x`:
   - Nếu `A[mid] == x` → tìm thấy, trả về `mid`.
   - Nếu `A[mid] < x` → khóa (nếu có) chỉ có thể nằm ở nửa phải → thu hẹp `low = mid + 1`.
   - Nếu `A[mid] > x` → khóa (nếu có) chỉ có thể nằm ở nửa trái → thu hẹp `high = mid - 1`.
3. Lặp lại cho đến khi tìm thấy hoặc `low > high` (đoạn tìm kiếm rỗng → không tìm thấy).

**Điều kiện bắt buộc**: dãy dữ liệu phải **đã được sắp xếp** theo khóa tìm kiếm — nếu chưa sắp xếp, phải sắp xếp trước (tốn thêm O(n log n)) hoặc dùng [tìm kiếm tuần tự](../13-linear-search/) thay thế.

**Ưu điểm:**
- Rất nhanh với dữ liệu lớn: chỉ cần khoảng log₂(n) lần so sánh.

**Nhược điểm:**
- Đòi hỏi dữ liệu đã sắp xếp và **truy xuất ngẫu nhiên được theo chỉ số** (O(1)) — phù hợp với mảng, không phù hợp với danh sách liên kết (vì phải duyệt tuần tự để tới vị trí giữa).

## Độ phức tạp

| Trường hợp | Số phép so sánh | Big-O |
|---|---|---|
| Tốt nhất (best case) | Phần tử giữa chính là khóa cần tìm | O(1) |
| Trung bình / Xấu nhất (worst case) | Chia đôi dãy liên tục cho tới khi còn 1 phần tử | O(log n) |

So sánh trực quan: với dãy 1,000,000 phần tử, tìm kiếm tuần tự cần tối đa 1,000,000 phép so sánh, trong khi tìm kiếm nhị phân chỉ cần tối đa 20 phép so sánh (log₂ 1,000,000 ≈ 20).

## Ví dụ

```
FUNCTION BinarySearch(A, n, x)
    low = 0
    high = n - 1
    WHILE low <= high
        mid = (low + high) / 2
        IF A[mid] == x THEN
            RETURN mid           // tìm thấy
        ELSE IF A[mid] < x THEN
            low = mid + 1        // tìm ở nửa phải
        ELSE
            high = mid - 1       // tìm ở nửa trái
        END IF
    END WHILE
    RETURN -1                    // không tìm thấy
END FUNCTION
```

```csharp
int BinarySearch(int[] a, int x)
{
    int low = 0, high = a.Length - 1;
    while (low <= high)
    {
        int mid = (low + high) / 2;
        if (a[mid] == x) return mid;
        else if (a[mid] < x) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}
```

## Demo

Xem file [demo.html](./demo.html) — nhập mảng đã sắp xếp và giá trị cần tìm, chạy từng bước để xem đoạn tìm kiếm [low, high] thu hẹp dần và vị trí giữa được xét ra sao.
