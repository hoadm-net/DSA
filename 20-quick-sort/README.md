# Quick Sort

## Khái niệm

Quick Sort là giải thuật sắp xếp hiệu quả dựa trên chiến lược **chia để trị** (divide and conquer): chọn một phần tử làm **chốt (pivot)**, phân hoạch (partition) dãy sao cho các phần tử nhỏ hơn chốt nằm bên trái, các phần tử lớn hơn nằm bên phải, rồi **đệ quy** sắp xếp hai đoạn con đó.

## Giải thích chi tiết

### Bước phân hoạch (partition)

Với đoạn `A[lo..hi]`, chọn phần tử cuối `A[hi]` làm chốt (một trong nhiều cách chọn chốt phổ biến). Dùng chỉ số `i` đánh dấu ranh giới của vùng "nhỏ hơn chốt":

1. Duyệt `j` từ `lo` đến `hi-1`, so sánh `A[j]` với chốt.
2. Nếu `A[j] < chốt`, tăng `i` rồi đổi chỗ `A[i]` và `A[j]` (đưa phần tử nhỏ hơn chốt về vùng bên trái).
3. Sau khi duyệt xong, đổi chỗ chốt (`A[hi]`) với `A[i+1]` — chốt đã về **đúng vị trí cuối cùng** trong dãy đã sắp xếp.

### Bước đệ quy

Sau phân hoạch, chốt chia dãy thành hai đoạn: `A[lo..i]` (toàn bộ nhỏ hơn chốt) và `A[i+2..hi]` (toàn bộ lớn hơn chốt). Áp dụng đệ quy Quick Sort cho từng đoạn con cho đến khi đoạn chỉ còn 0 hoặc 1 phần tử (đã hiển nhiên có thứ tự).

**Ưu điểm:**
- Rất nhanh trong thực tế (trung bình O(n log n)), sắp xếp tại chỗ (chỉ cần thêm O(log n) bộ nhớ cho ngăn xếp đệ quy).

**Nhược điểm:**
- Trường hợp xấu nhất O(n²) khi cách chọn chốt liên tục rơi vào phần tử nhỏ nhất/lớn nhất của đoạn (ví dụ dữ liệu đã gần như sắp xếp sẵn và luôn chọn chốt là phần tử cuối).
- **Không ổn định** (stable) theo cài đặt chuẩn.

## Độ phức tạp

| Trường hợp | Mô tả | Big-O |
|---|---|---|
| Tốt nhất / Trung bình | Chốt chia đôi dãy tương đối đều mỗi lần | O(n log n) |
| Xấu nhất (worst case) | Chốt luôn là phần tử nhỏ nhất/lớn nhất của đoạn | O(n²) |

## Ví dụ

```
FUNCTION Partition(A, lo, hi)
    pivot = A[hi]
    i = lo - 1
    FOR j = lo TO hi - 1
        IF A[j] < pivot THEN
            i = i + 1
            Đổi chỗ A[i] và A[j]
        END IF
    END FOR
    Đổi chỗ A[i+1] và A[hi]
    RETURN i + 1              // vị trí cuối cùng của chốt

FUNCTION QuickSort(A, lo, hi)
    IF lo < hi THEN
        p = Partition(A, lo, hi)
        QuickSort(A, lo, p - 1)
        QuickSort(A, p + 1, hi)
    END IF
END FUNCTION
```

```csharp
void QuickSort(int[] a, int lo, int hi)
{
    if (lo < hi)
    {
        int p = Partition(a, lo, hi);
        QuickSort(a, lo, p - 1);
        QuickSort(a, p + 1, hi);
    }
}

int Partition(int[] a, int lo, int hi)
{
    int pivot = a[hi];
    int i = lo - 1;
    for (int j = lo; j < hi; j++)
    {
        if (a[j] < pivot)
        {
            i++;
            (a[i], a[j]) = (a[j], a[i]);
        }
    }
    (a[i + 1], a[hi]) = (a[hi], a[i + 1]);
    return i + 1;
}
```

## Demo

Xem file [demo.html](./demo.html) — nhập mảng hoặc tạo mảng ngẫu nhiên, chạy từng bước để xem chốt được chọn, quá trình phân hoạch, và các lần gọi đệ quy trên đoạn con.
