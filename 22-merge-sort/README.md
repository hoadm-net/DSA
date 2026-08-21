# Merge Sort

## Khái niệm

Merge Sort là giải thuật sắp xếp dựa trên chiến lược **chia để trị** (divide and conquer): chia đôi dãy liên tục thành các đoạn con nhỏ hơn cho đến khi mỗi đoạn chỉ còn 1 phần tử (hiển nhiên đã sắp xếp), sau đó **trộn (merge)** dần các đoạn con đã sắp xếp lại thành đoạn lớn hơn có thứ tự.

## Giải thích chi tiết

### Bước chia (Divide)

Chia đoạn `A[lo..hi]` thành hai nửa tại `mid = (lo + hi) / 2`: `A[lo..mid]` và `A[mid+1..hi]`. Đệ quy tiếp tục chia cho đến khi đoạn chỉ còn 0 hoặc 1 phần tử.

### Bước trộn (Merge)

Trộn hai đoạn con **đã được sắp xếp** thành một đoạn lớn có thứ tự:
1. Dùng hai con trỏ `i`, `j` lần lượt trỏ vào đầu đoạn trái và đoạn phải.
2. So sánh phần tử tại hai con trỏ, phần tử nào nhỏ hơn được ghi vào mảng kết quả trước, con trỏ tương ứng tăng lên.
3. Lặp lại cho đến khi một trong hai đoạn hết phần tử, sau đó chép nốt phần còn lại của đoạn kia vào cuối.

Vì bước trộn cần so sánh và ghi kết quả vào một vị trí mới, Merge Sort thường cần một **mảng phụ (buffer)** để chứa kết quả trộn tạm thời, sau đó chép ngược lại mảng gốc.

**Ưu điểm:**
- Đảm bảo O(n log n) ở **mọi trường hợp** — không có worst case tệ như Quick Sort.
- **Ổn định** (stable): khi hai phần tử bằng nhau, phần tử ở đoạn trái luôn được ghi trước (quy ước `left[i] <= right[j]` thì lấy từ đoạn trái).
- Rất phù hợp để sắp xếp danh sách liên kết (không cần truy xuất ngẫu nhiên) và sắp xếp dữ liệu ngoài (external sorting) với dữ liệu lớn hơn bộ nhớ.

**Nhược điểm:**
- Cần thêm bộ nhớ phụ O(n) cho mảng buffer trong bước trộn — không phải giải thuật tại chỗ (in-place) theo cài đặt chuẩn.

## Độ phức tạp

| Thành phần | Chi phí |
|---|---|
| Số lần chia đôi (độ sâu đệ quy) | O(log n) |
| Chi phí trộn ở mỗi tầng (tổng cộng duyệt qua n phần tử) | O(n) |
| **Tổng cộng (mọi trường hợp)** | **O(n log n)** |
| Bộ nhớ phụ | O(n) |

## Ví dụ

```
FUNCTION MergeSort(A, lo, hi)
    IF lo >= hi THEN RETURN
    mid = (lo + hi) / 2
    MergeSort(A, lo, mid)
    MergeSort(A, mid + 1, hi)
    Merge(A, lo, mid, hi)
END FUNCTION

FUNCTION Merge(A, lo, mid, hi)
    left = A[lo..mid]
    right = A[mid+1..hi]
    i = 0, j = 0, k = lo
    WHILE i < length(left) AND j < length(right)
        IF left[i] <= right[j] THEN
            A[k] = left[i]; i = i + 1
        ELSE
            A[k] = right[j]; j = j + 1
        END IF
        k = k + 1
    END WHILE
    Chép nốt phần tử còn lại của left hoặc right vào A
END FUNCTION
```

```csharp
void MergeSort(int[] a, int lo, int hi)
{
    if (lo >= hi) return;
    int mid = (lo + hi) / 2;
    MergeSort(a, lo, mid);
    MergeSort(a, mid + 1, hi);
    Merge(a, lo, mid, hi);
}

void Merge(int[] a, int lo, int mid, int hi)
{
    int[] left = a[lo..(mid + 1)];
    int[] right = a[(mid + 1)..(hi + 1)];
    int i = 0, j = 0, k = lo;
    while (i < left.Length && j < right.Length)
    {
        a[k++] = (left[i] <= right[j]) ? left[i++] : right[j++];
    }
    while (i < left.Length) a[k++] = left[i++];
    while (j < right.Length) a[k++] = right[j++];
}
```

## Demo

Xem file [demo.html](./demo.html) — nhập mảng hoặc tạo mảng ngẫu nhiên, chạy từng bước để xem quá trình chia đôi đệ quy và trộn các đoạn con lại theo thứ tự.
