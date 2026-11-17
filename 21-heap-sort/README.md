# Heap & Heap Sort

Bài này gồm 2 phần độc lập: hiểu **CTDL Heap** trước, sau đó xem cách **tận dụng Heap để sắp xếp (Heap Sort)**.

---

# Phần 1: Cấu trúc dữ liệu Heap

## Khái niệm

**Heap (đống)** là một cấu trúc dữ liệu dạng cây nhị phân gần như đầy (complete binary tree), thỏa mãn **tính chất thứ tự heap**:

- **Max-heap**: giá trị mỗi nút cha ≥ giá trị các nút con → gốc luôn là phần tử **lớn nhất**.
- **Min-heap**: giá trị mỗi nút cha ≤ giá trị các nút con → gốc luôn là phần tử **nhỏ nhất**.

Heap **không phải** là cây tìm kiếm nhị phân (BST) — nó chỉ đảm bảo quan hệ cha/con theo chiều dọc, không có thứ tự trái/phải. Đổi lại, heap "gần như đầy" nên luôn cân bằng, cho phép cài đặt gọn bằng **mảng** và các thao tác chính đều chạy O(log n).

## Giải thích chi tiết

### Biểu diễn heap bằng mảng

Vì heap là cây gần như đầy, có thể biểu diễn trực tiếp bằng mảng (không cần con trỏ):

- Nút tại chỉ số `i` → con trái ở `2i + 1`, con phải ở `2i + 2`.
- Nút tại chỉ số `i` (i > 0) → cha ở `(i - 1) / 2` (chia lấy nguyên).
- Phần tử cuối mảng (`A[n-1]`) luôn là nút "cuối cùng" của cây, dùng để giữ tính chất *gần như đầy* khi thêm/xóa.

### Heapify (vun đống) — thao tác lõi

`Heapify(A, n, i)` giả định hai cây con của `i` đã là max-heap, chỉ có nút `i` có thể vi phạm — nó "đẩy" giá trị tại `i` xuống đúng vị trí:

1. So sánh `A[i]` với con trái và con phải, tìm chỉ số `largest` có giá trị lớn nhất trong 3.
2. Nếu `largest != i`: đổi chỗ `A[i]` và `A[largest]`, rồi gọi đệ quy `Heapify(A, n, largest)`.
3. Nếu `largest == i`: dừng — tính chất heap đã đúng.

Độ phức tạp: O(log n) — vì mỗi lần đệ quy đi xuống 1 tầng, cây cao log n.

### Sift-up (vun lên) — thao tác lõi còn lại

Ngược với heapify (đẩy xuống), **sift-up** đẩy một giá trị **lên** khi nó lớn hơn cha:

1. So sánh `A[i]` với cha `A[(i-1)/2]`.
2. Nếu `A[i] > A[cha]`: đổi chỗ, cập nhật `i = (i-1)/2`, lặp lại.
3. Dừng khi `i = 0` hoặc `A[i] <= A[cha]`.

### Các thao tác trên CTDL Heap

| Thao tác | Ý tưởng | Độ phức tạp |
|---|---|---|
| **Build Heap** (xây dựng từ mảng bất kỳ) | Duyệt từ nút cha không-lá cuối cùng (`i = n/2 - 1`) ngược về gốc (`i = 0`), gọi Heapify tại mỗi nút | O(n) |
| **Insert / Push** (thêm phần tử) | Thêm phần tử mới vào **cuối mảng** (giữ tính chất gần-như-đầy), rồi **sift-up** từ vị trí đó lên gốc để khôi phục tính chất heap | O(log n) |
| **Extract-Max / Pop** (lấy & xóa phần tử lớn nhất) | Gốc (`A[0]`) là kết quả cần lấy. Đưa phần tử **cuối mảng** lên gốc, giảm kích thước heap đi 1, rồi **Heapify** tại gốc để khôi phục tính chất heap | O(log n) |
| **Peek** (xem phần tử lớn nhất) | Trả về `A[0]` mà không thay đổi heap | O(1) |
| **Update / Increase-Key** (tăng giá trị 1 nút) | Sửa `A[i]`, giá trị mới **lớn hơn** giá trị cũ → chỉ có thể vi phạm với cha → **sift-up** từ `i` | O(log n) |
| **Update / Decrease-Key** (giảm giá trị 1 nút) | Sửa `A[i]`, giá trị mới **nhỏ hơn** giá trị cũ → chỉ có thể vi phạm với con → **Heapify** tại `i` | O(log n) |
| **Delete(i)** (xóa nút tùy ý ở vị trí i) | Thay `A[i]` bằng phần tử cuối mảng, giảm kích thước heap đi 1, rồi tùy giá trị mới lớn hơn hay nhỏ hơn giá trị cũ mà **sift-up** hoặc **Heapify** tại `i` | O(log n) |

> **Vì sao Insert đẩy lên còn Extract-Max đẩy xuống?** Khi thêm, phần tử mới nằm ở lá (đáy cây) — nó chỉ có thể "quá lớn" so với tổ tiên nên cần đi lên. Khi lấy gốc ra và thay bằng phần tử cuối, giá trị đưa lên gốc thường "quá nhỏ" so với các con nên cần đi xuống.

### Ứng dụng của Heap

- **Priority Queue** (hàng đợi ưu tiên) — cài đặt chuẩn nhất cho ADT này.
- Thuật toán **Dijkstra**, **Prim** (tìm đường đi ngắn nhất / cây khung nhỏ nhất) dùng min-heap để chọn đỉnh tiếp theo.
- Tìm **k phần tử lớn/nhỏ nhất** trong luồng dữ liệu (giữ heap kích thước k).
- **Heap Sort** — xem [Phần 2](#phần-2-heap-sort) bên dưới.

## Độ phức tạp

| Thao tác | Big-O |
|---|---|
| Insert (Push) | O(log n) |
| Extract-Max (Pop) | O(log n) |
| Peek | O(1) |
| Update key (sửa giá trị 1 nút) | O(log n) |
| Build Heap (xây dựng từ mảng) | O(n) |

## Ví dụ

### Pseudo-code

```
FUNCTION Heapify(A, n, i)          // vun đống — đẩy A[i] xuống
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

FUNCTION SiftUp(A, i)               // vun lên — đẩy A[i] lên
    WHILE i > 0 AND A[(i-1)/2] < A[i]
        Đổi chỗ A[i] và A[(i-1)/2]
        i = (i-1)/2
    END WHILE
END FUNCTION

FUNCTION BuildHeap(A, n)
    FOR i = n/2 - 1 DOWNTO 0
        Heapify(A, n, i)
    END FOR
END FUNCTION

FUNCTION Insert(A, n, value)        // thêm phần tử — O(log n)
    A[n] = value                    // thêm vào cuối mảng
    n = n + 1
    SiftUp(A, n - 1)
END FUNCTION

FUNCTION ExtractMax(A, n)           // lấy & xóa phần tử lớn nhất — O(log n)
    max = A[0]
    A[0] = A[n - 1]                 // đưa phần tử cuối lên gốc
    n = n - 1
    Heapify(A, n, 0)
    RETURN max
END FUNCTION

FUNCTION UpdateKey(A, n, i, newValue)   // sửa giá trị tại vị trí i — O(log n)
    old = A[i]
    A[i] = newValue
    IF newValue > old THEN
        SiftUp(A, i)                // giá trị tăng → có thể vi phạm với cha
    ELSE
        Heapify(A, n, i)            // giá trị giảm → có thể vi phạm với con
    END IF
END FUNCTION
```

### Cài đặt CTDL MaxHeap (C#)

```csharp
class MaxHeap
{
    private List<int> a = new List<int>();

    public int Count => a.Count;
    public int Peek() => a[0];

    // Thêm phần tử — O(log n)
    public void Insert(int value)
    {
        a.Add(value);
        SiftUp(a.Count - 1);
    }

    // Lấy & xóa phần tử lớn nhất — O(log n)
    public int ExtractMax()
    {
        int max = a[0];
        a[0] = a[^1];
        a.RemoveAt(a.Count - 1);
        if (a.Count > 0) Heapify(0);
        return max;
    }

    // Sửa giá trị tại vị trí i — O(log n)
    public void UpdateKey(int i, int newValue)
    {
        int old = a[i];
        a[i] = newValue;
        if (newValue > old) SiftUp(i);
        else Heapify(i);
    }

    private void SiftUp(int i)
    {
        while (i > 0)
        {
            int parent = (i - 1) / 2;
            if (a[parent] >= a[i]) break;
            (a[parent], a[i]) = (a[i], a[parent]);
            i = parent;
        }
    }

    private void Heapify(int i)
    {
        int largest = i, l = 2 * i + 1, r = 2 * i + 2;
        if (l < a.Count && a[l] > a[largest]) largest = l;
        if (r < a.Count && a[r] > a[largest]) largest = r;
        if (largest != i)
        {
            (a[i], a[largest]) = (a[largest], a[i]);
            Heapify(largest);
        }
    }
}
```

## Demo

Xem file [heap.html](./heap.html) — khởi tạo heap từ mảng (Build Heap), rồi thao tác Insert, Extract-Max, Update-Key trực quan trên cây nhị phân, xem heap tự động vun lên (sift-up) / vun xuống (heapify).

---

# Phần 2: Heap Sort

## Khái niệm

**Heap Sort** là giải thuật sắp xếp **tận dụng CTDL max-heap** ở Phần 1: xây dựng max-heap từ mảng ban đầu, sau đó liên tục dùng thao tác **Extract-Max** để lấy phần tử lớn nhất (luôn ở gốc heap) đưa về cuối mảng.

## Giải thích chi tiết

### Giai đoạn 1 — Xây dựng max-heap (Build Heap)

Áp dụng đúng thao tác **Build Heap** đã học ở Phần 1: duyệt từ nút cha không-lá cuối cùng (`i = n/2 - 1`) ngược về gốc (`i = 0`), gọi **Heapify** tại mỗi nút — đảm bảo tính chất max-heap được lan truyền xuống. Độ phức tạp O(n).

### Giai đoạn 2 — Trích xuất phần tử lớn nhất lặp lại

Về bản chất là gọi **Extract-Max** liên tiếp `n - 1` lần, nhưng thay vì cấp phát mảng phụ, ta tận dụng chính mảng gốc: mỗi lần lấy phần tử lớn nhất ra thì đặt luôn vào vị trí cuối của phần chưa sắp xếp — nhờ vậy sắp xếp tại chỗ (in-place).

Lặp lại từ `i = n-1` giảm về 1:
1. Đổi chỗ gốc heap (`A[0]`, luôn là phần tử lớn nhất hiện tại) với `A[i]` — đưa phần tử lớn nhất về đúng vị trí cuối cùng.
2. Thu nhỏ phạm vi heap còn `i` phần tử (bỏ phần tử vừa chốt ra khỏi heap).
3. Gọi Heapify tại gốc (`i = 0`) trên phạm vi heap mới để khôi phục tính chất max-heap.

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
FUNCTION HeapSort(A, n)
    // Giai đoạn 1: xây dựng max-heap
    BuildHeap(A, n)
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

Xem file [heap-sort.html](./heap-sort.html) — nhập mảng hoặc tạo mảng ngẫu nhiên, chạy từng bước để xem giai đoạn xây dựng heap và giai đoạn trích xuất phần tử lớn nhất về cuối mảng.
