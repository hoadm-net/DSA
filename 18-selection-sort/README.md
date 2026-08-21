# Chọn trực tiếp (Selection Sort)

## Khái niệm

Chọn trực tiếp là giải thuật sắp xếp: với mỗi vị trí `i` từ đầu dãy, **tìm ra phần tử nhỏ nhất** trong đoạn `A[i..n-1]`, sau đó đổi chỗ nó với `A[i]`. Khác với [Đổi chỗ trực tiếp](../16-interchange-sort/), Selection Sort chỉ thực hiện **đúng một phép đổi chỗ** cho mỗi vị trí `i` (sau khi đã xác định được vị trí nhỏ nhất), thay vì đổi chỗ ngay mỗi lần so sánh.

## Giải thích chi tiết

Các bước với mỗi `i` từ 0 đến n-2:
1. Giả sử `A[i]` là phần tử nhỏ nhất tạm thời, đặt `minIdx = i`.
2. Duyệt `j` từ `i+1` đến `n-1`: nếu `A[j] < A[minIdx]` thì cập nhật `minIdx = j`.
3. Sau khi duyệt hết, nếu `minIdx != i` thì đổi chỗ `A[i]` và `A[minIdx]`.

**Ưu điểm**: số phép đổi chỗ tối đa chỉ là n-1 lần (ít hơn hẳn Bubble Sort hay Interchange Sort) — phù hợp khi chi phí đổi chỗ (ghi dữ liệu) tốn kém hơn nhiều so với chi phí so sánh.

**Nhược điểm**: số phép so sánh vẫn là O(n²) bất kể dữ liệu đầu vào đã sắp xếp hay chưa (không có cách nào "kết thúc sớm"); **không ổn định** (stable) theo cài đặt chuẩn — việc đổi chỗ trực tiếp phần tử nhỏ nhất về đầu có thể làm thay đổi thứ tự tương đối của các phần tử bằng nhau.

## Độ phức tạp

| Trường hợp | Số phép so sánh | Số phép đổi chỗ | Big-O |
|---|---|---|---|
| Mọi trường hợp | n(n-1)/2 (không đổi theo dữ liệu đầu vào) | Tối đa n-1 | O(n²) |

## Ví dụ

```
FUNCTION SelectionSort(A, n)
    FOR i = 0 TO n - 2
        minIdx = i
        FOR j = i + 1 TO n - 1
            IF A[j] < A[minIdx] THEN
                minIdx = j
            END IF
        END FOR
        IF minIdx != i THEN
            Đổi chỗ A[i] và A[minIdx]
        END IF
    END FOR
END FUNCTION
```

```csharp
void SelectionSort(int[] a)
{
    for (int i = 0; i < a.Length - 1; i++)
    {
        int minIdx = i;
        for (int j = i + 1; j < a.Length; j++)
        {
            if (a[j] < a[minIdx]) minIdx = j;
        }
        if (minIdx != i)
        {
            (a[i], a[minIdx]) = (a[minIdx], a[i]);
        }
    }
}
```

## Demo

Xem file [demo.html](./demo.html) — nhập mảng hoặc tạo mảng ngẫu nhiên, chạy từng bước để xem quá trình tìm phần tử nhỏ nhất (highlight riêng) và đổi chỗ về đầu đoạn.
