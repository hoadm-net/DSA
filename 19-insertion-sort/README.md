# Chèn trực tiếp (Insertion Sort)

## Khái niệm

Chèn trực tiếp là giải thuật sắp xếp mô phỏng cách con người sắp xếp một bộ bài trên tay: coi đoạn đầu dãy là **đã sắp xếp**, sau đó lần lượt lấy từng phần tử tiếp theo (gọi là "khóa") và **chèn nó vào đúng vị trí** trong đoạn đã sắp xếp, bằng cách dịch chuyển các phần tử lớn hơn khóa sang phải.

## Giải thích chi tiết

Các bước với mỗi `i` từ 1 đến n-1 (coi `A[0]` là đoạn đã sắp xếp ban đầu, chỉ gồm 1 phần tử):
1. Lưu `key = A[i]`.
2. Đặt `j = i - 1`. Trong khi `j >= 0` và `A[j] > key`: dịch `A[j]` sang phải một vị trí (`A[j+1] = A[j]`), giảm `j`.
3. Khi vòng lặp dừng, chèn `key` vào vị trí `A[j+1]`.
4. Sau bước này, đoạn `A[0..i]` đã được sắp xếp.

**Ưu điểm:**
- **Rất nhanh nếu dữ liệu đã gần như có thứ tự** — trường hợp tốt nhất chỉ O(n) vì hầu như không cần dịch chuyển.
- **Ổn định** (stable): phần tử bằng nhau không bị đổi thứ tự tương đối (chỉ dịch chuyển khi `A[j] > key`, không dịch khi bằng).
- Sắp xếp tại chỗ (in-place), phù hợp với dãy dữ liệu nhỏ hoặc "gần như đã sắp xếp" (ví dụ chèn thêm phần tử mới vào danh sách đã sắp xếp sẵn).

**Nhược điểm:**
- Chậm với dữ liệu lớn và bị sắp xếp ngược — worst case O(n²).

## Độ phức tạp

| Trường hợp | Mô tả | Big-O |
|---|---|---|
| Tốt nhất (best case) | Mảng đã sắp xếp sẵn, không cần dịch chuyển | O(n) |
| Trung bình / Xấu nhất (worst case) | Mảng ngẫu nhiên / sắp xếp ngược | O(n²) |

## Ví dụ

```
FUNCTION InsertionSort(A, n)
    FOR i = 1 TO n - 1
        key = A[i]
        j = i - 1
        WHILE j >= 0 AND A[j] > key
            A[j + 1] = A[j]
            j = j - 1
        END WHILE
        A[j + 1] = key
    END FOR
END FUNCTION
```

```csharp
void InsertionSort(int[] a)
{
    for (int i = 1; i < a.Length; i++)
    {
        int key = a[i];
        int j = i - 1;
        while (j >= 0 && a[j] > key)
        {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = key;
    }
}
```

## Demo

Xem file [demo.html](./demo.html) — nhập mảng hoặc tạo mảng ngẫu nhiên, chạy từng bước để xem "khóa" được lấy ra và chèn vào đúng vị trí trong đoạn đã sắp xếp.
