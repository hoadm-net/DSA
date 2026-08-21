# Tìm kiếm tuần tự (Linear Search)

## Khái niệm

Tìm kiếm tuần tự là giải thuật tìm kiếm đơn giản nhất: duyệt qua **từng phần tử của dãy dữ liệu, theo thứ tự từ đầu đến cuối**, so sánh với khóa cần tìm cho đến khi tìm thấy hoặc duyệt hết dãy.

## Giải thích chi tiết

Ý tưởng: bắt đầu từ phần tử đầu tiên, so sánh lần lượt với khóa `x`:
- Nếu phần tử hiện tại bằng `x` → tìm thấy, trả về vị trí.
- Nếu duyệt hết dãy mà không gặp `x` → không tìm thấy.

**Ưu điểm:**
- Cài đặt đơn giản nhất trong các giải thuật tìm kiếm.
- **Không đòi hỏi dữ liệu phải được sắp xếp trước** — áp dụng được cho mọi dãy dữ liệu.
- Hoạt động được trên cả mảng lẫn danh sách liên kết (chỉ cần duyệt tuần tự được).

**Nhược điểm:**
- Chậm với dữ liệu lớn vì phải so sánh trung bình một nửa số phần tử.

## Độ phức tạp

| Trường hợp | Số phép so sánh | Big-O |
|---|---|---|
| Tốt nhất (best case) | Phần tử đầu tiên chính là khóa cần tìm | O(1) |
| Trung bình (average case) | Khoảng n/2 phép so sánh | O(n) |
| Xấu nhất (worst case) | Khóa ở cuối dãy hoặc không tồn tại | O(n) |

## Ví dụ

```
FUNCTION LinearSearch(A, n, x)
    FOR i = 0 TO n - 1
        IF A[i] == x THEN
            RETURN i          // tìm thấy, trả về vị trí
        END IF
    END FOR
    RETURN -1                 // duyệt hết mà không thấy
END FUNCTION
```

```csharp
int LinearSearch(int[] a, int x)
{
    for (int i = 0; i < a.Length; i++)
    {
        if (a[i] == x) return i;
    }
    return -1;
}
```

## Demo

Xem file [demo.html](./demo.html) — nhập mảng và giá trị cần tìm, chạy từng bước để xem giải thuật duyệt và so sánh từng phần tử ra sao.
