# Nổi bọt (Bubble Sort)

## Khái niệm

Nổi bọt là giải thuật sắp xếp lặp lại việc so sánh **hai phần tử liền kề**; nếu chúng sai thứ tự thì đổi chỗ. Sau mỗi lượt duyệt (pass) từ đầu đến cuối đoạn chưa sắp xếp, phần tử lớn nhất trong đoạn đó sẽ "nổi" dần về đúng vị trí cuối cùng — giống bọt khí nổi lên trên.

## Giải thích chi tiết

Các bước:
1. Duyệt đoạn `A[0..n-1-i]` (với i là số lượt đã hoàn thành), so sánh từng cặp liền kề `A[j]` và `A[j+1]`.
2. Nếu `A[j] > A[j+1]` thì đổi chỗ.
3. Sau khi duyệt hết một lượt, phần tử lớn nhất của đoạn đã "nổi" về cuối đoạn (`vị trí n-1-i`) → không cần xét lại vị trí này ở các lượt sau.
4. Lặp lại cho đến khi không còn cặp nào cần đổi chỗ, hoặc đã thực hiện đủ n-1 lượt.

**Tối ưu thường gặp**: nếu trong một lượt duyệt không có phép đổi chỗ nào xảy ra, nghĩa là mảng đã sắp xếp xong — có thể dừng sớm thay vì chạy đủ n-1 lượt.

**Ưu điểm**: dễ hiểu, dễ cài đặt, sắp xếp tại chỗ, **ổn định** (stable) — hai phần tử bằng nhau không bao giờ bị đổi chỗ cho nhau (chỉ đổi chỗ khi `A[j] > A[j+1]`, không đổi khi bằng).

**Nhược điểm**: hiệu năng kém với dữ liệu lớn do số phép so sánh và đổi chỗ nhiều.

## Độ phức tạp

| Trường hợp | Mô tả | Big-O |
|---|---|---|
| Tốt nhất (best case) | Mảng đã sắp xếp sẵn, dừng sớm sau 1 lượt (nếu có tối ưu) | O(n) |
| Trung bình / Xấu nhất (worst case) | Mảng ngẫu nhiên / sắp xếp ngược | O(n²) |

## Ví dụ

```
FUNCTION BubbleSort(A, n)
    FOR i = 0 TO n - 2
        FOR j = 0 TO n - 2 - i
            IF A[j] > A[j+1] THEN
                Đổi chỗ A[j] và A[j+1]
            END IF
        END FOR
    END FOR
END FUNCTION
```

```csharp
void BubbleSort(int[] a)
{
    for (int i = 0; i < a.Length - 1; i++)
    {
        for (int j = 0; j < a.Length - 1 - i; j++)
        {
            if (a[j] > a[j + 1])
            {
                (a[j], a[j + 1]) = (a[j + 1], a[j]);
            }
        }
    }
}
```

## Demo

Xem file [demo.html](./demo.html) — nhập mảng hoặc tạo mảng ngẫu nhiên, chạy từng bước để xem phần tử lớn nhất "nổi" dần về cuối mảng sau mỗi lượt.
