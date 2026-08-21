# Heap Sort

## Khái niệm

Heap Sort là giải thuật sắp xếp dựa trên cấu trúc dữ liệu **heap** (đống) — cụ thể là **max-heap**, một cây nhị phân gần như đầy, trong đó giá trị của mỗi nút cha luôn lớn hơn hoặc bằng giá trị của các nút con. Giải thuật gồm hai giai đoạn: **xây dựng max-heap** từ mảng ban đầu, sau đó **liên tục lấy phần tử lớn nhất** (luôn ở gốc heap) đưa về cuối mảng.

## Giải thích chi tiết

### Biểu diễn heap bằng mảng

Một max-heap có thể biểu diễn trực tiếp bằng mảng: với nút tại chỉ số `i`, con trái ở chỉ số `2i + 1`, con phải ở chỉ số `2i + 2`. Nhờ vậy heap không cần con trỏ, thao tác hoàn toàn trên mảng.

### Giai đoạn 1 — Xây dựng max-heap (Build Heap)

Duyệt từ nút cha không-lá cuối cùng (`i = n/2 - 1`) ngược về gốc (`i = 0`), gọi thao tác **heapify** (vun đống) tại mỗi nút: so sánh nút với hai con, nếu con lớn hơn thì đổi chỗ và tiếp tục heapify tại vị trí con đó — đảm bảo tính chất max-heap được lan truyền xuống.

### Giai đoạn 2 — Trích xuất phần tử lớn nhất (Extract Max)

Lặp lại từ `i = n-1` giảm về 1:
1. Đổi chỗ gốc heap (`A[0]`, luôn là phần tử lớn nhất hiện tại) với `A[i]` — đưa phần tử lớn nhất về đúng vị trí cuối cùng.
2. Thu nhỏ phạm vi heap còn `i` phần tử (bỏ phần tử vừa chốt ra khỏi heap).
3. Gọi heapify tại gốc (`i = 0`) trên phạm vi heap mới để khôi phục tính chất max-heap.

**Ưu điểm:**
- Đảm bảo O(n log n) ở **mọi trường hợp** (không có worst case tệ như Quick Sort).
- Sắp xếp tại chỗ, chỉ cần O(1) bộ nhớ phụ (khác Merge Sort cần bộ nhớ phụ O(n)).

**Nhược điểm:**
- **Không ổn định** (stable).
- Trong thực tế thường chạy chậm hơn Quick Sort do tính "cache-friendly" kém hơn (truy cập bộ nhớ không liên tục bằng).

## Độ phức tạp

| Giai đoạn | Big-O |
|---|---|
| Xây dựng heap (Build Heap) | O(n) |
| Trích xuất n phần tử, mỗi lần heapify O(log n) | O(n log n) |
| **Tổng cộng (mọi trường hợp)** | **O(n log n)** |

## Ví dụ

```
FUNCTION Heapify(A, n, i)
    largest = i
    l = 2*i + 1
    r = 2*i + 2
    IF l < n AND A[l] > A[largest] THEN largest = l
    IF r < n AND A[r] > A[largest] THEN largest = r
    IF largest != i THEN
        Đổi chỗ A[i] và A[largest]
        Heapify(A, n, largest)
    END IF
END FUNCTION

FUNCTION HeapSort(A, n)
    // Giai đoạn 1: xây dựng max-heap
    FOR i = n/2 - 1 DOWNTO 0
        Heapify(A, n, i)
    END FOR
    // Giai đoạn 2: trích xuất phần tử lớn nhất
    FOR i = n - 1 DOWNTO 1
        Đổi chỗ A[0] và A[i]
        Heapify(A, i, 0)
    END FOR
END FUNCTION
```

```csharp
void HeapSort(int[] a)
{
    int n = a.Length;
    for (int i = n / 2 - 1; i >= 0; i--) Heapify(a, n, i);
    for (int i = n - 1; i > 0; i--)
    {
        (a[0], a[i]) = (a[i], a[0]);
        Heapify(a, i, 0);
    }
}

void Heapify(int[] a, int n, int i)
{
    int largest = i, l = 2 * i + 1, r = 2 * i + 2;
    if (l < n && a[l] > a[largest]) largest = l;
    if (r < n && a[r] > a[largest]) largest = r;
    if (largest != i)
    {
        (a[i], a[largest]) = (a[largest], a[i]);
        Heapify(a, n, largest);
    }
}
```

## Demo

Xem file [demo.html](./demo.html) — nhập mảng hoặc tạo mảng ngẫu nhiên, chạy từng bước để xem giai đoạn xây dựng heap và giai đoạn trích xuất phần tử lớn nhất về cuối mảng.
