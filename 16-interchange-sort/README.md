# Đổi chỗ trực tiếp (Interchange Sort)

## Khái niệm

Đổi chỗ trực tiếp là giải thuật sắp xếp cơ bản: với mỗi vị trí `i` từ đầu dãy, so sánh trực tiếp `A[i]` lần lượt với **từng phần tử phía sau** `A[j]` (j từ i+1 đến cuối); hễ phát hiện `A[i] > A[j]` thì **đổi chỗ ngay lập tức**. Sau khi hoàn tất vòng lặp trong với một giá trị `i`, phần tử tại vị trí `i` chắc chắn là nhỏ nhất trong đoạn `A[i..n-1]`.

## Giải thích chi tiết

Đây là giải thuật đơn giản nhất trong nhóm sắp xếp cơ bản: khác với Selection Sort (chỉ so sánh để *tìm ra* vị trí nhỏ nhất rồi mới đổi chỗ một lần), Interchange Sort **đổi chỗ ngay** mỗi khi tìm thấy cặp sai thứ tự, có thể đổi chỗ nhiều lần trong cùng một vòng lặp `i`.

Các bước với mỗi `i` từ 0 đến n-2:
1. Với mỗi `j` từ `i+1` đến `n-1`: nếu `A[i] > A[j]` thì đổi chỗ `A[i]` và `A[j]`.
2. Sau khi j chạy hết, `A[i]` đã là giá trị nhỏ nhất của đoạn `A[i..n-1]`.

**Ưu điểm**: cài đặt rất đơn giản, dễ hiểu, sắp xếp tại chỗ (in-place).

**Nhược điểm**: số phép hoán vị (swap) có thể nhiều hơn Selection Sort (vì đổi chỗ ngay mỗi lần thay vì gộp lại một lần), hiệu năng kém với dữ liệu lớn.

## Độ phức tạp

| Trường hợp | Số phép so sánh | Big-O |
|---|---|---|
| Mọi trường hợp | n(n-1)/2 phép so sánh (không đổi theo dữ liệu đầu vào) | O(n²) |

Không có bộ nhớ phụ đáng kể — đây là giải thuật sắp xếp tại chỗ, không ổn định (stability không được đảm bảo vì đổi chỗ trực tiếp có thể làm thay đổi thứ tự tương đối của các phần tử bằng nhau).

## Ví dụ

```
FUNCTION InterchangeSort(A, n)
    FOR i = 0 TO n - 2
        FOR j = i + 1 TO n - 1
            IF A[i] > A[j] THEN
                Đổi chỗ A[i] và A[j]
            END IF
        END FOR
    END FOR
END FUNCTION
```

```csharp
void InterchangeSort(int[] a)
{
    for (int i = 0; i < a.Length - 1; i++)
    {
        for (int j = i + 1; j < a.Length; j++)
        {
            if (a[i] > a[j])
            {
                (a[i], a[j]) = (a[j], a[i]);
            }
        }
    }
}
```

## Demo

Xem file [demo.html](./demo.html) — nhập mảng hoặc tạo mảng ngẫu nhiên, chạy từng bước để xem từng phép so sánh và đổi chỗ.
