# Cây nhị phân tìm kiếm cân bằng — AVL: khái niệm & chỉ số cân bằng

## Khái niệm

Cây AVL (đặt theo tên hai nhà phát minh Adelson-Velsky và Landis) là [cây nhị phân tìm kiếm (BST)](../43-binary-search-tree/) có thêm một ràng buộc: **với mọi node, chiều cao của hai cây con trái và phải chỉ được chênh lệch nhau tối đa 1**. Ràng buộc này đảm bảo cây luôn "gần như cân bằng", giữ cho các thao tác luôn đạt O(log n).

## Giải thích chi tiết

### Vấn đề mà AVL giải quyết

Như đã nêu ở [BST: định nghĩa & thao tác thêm/tìm](../43-binary-search-tree/), một BST thông thường có thể **suy biến thành đường thẳng** nếu dữ liệu được chèn theo thứ tự đã sắp xếp — khi đó chiều cao cây `h = n`, khiến Search/Insert/Delete đều tụt xuống O(n), mất hoàn toàn lợi thế của cấu trúc cây. AVL khắc phục vấn đề này bằng cách **tự động điều chỉnh lại cấu trúc cây** (thông qua phép quay, xem [Các trường hợp mất cân bằng & phép quay](../46-avl-rotations/)) mỗi khi phát hiện mất cân bằng, đảm bảo `h` luôn ở mức O(log n) **trong mọi trường hợp**, không phụ thuộc thứ tự dữ liệu được chèn vào.

### Chỉ số cân bằng (Balance Factor)

Với mỗi node, định nghĩa:

```
BalanceFactor(node) = Height(node.Left) − Height(node.Right)
```

Quy ước: chiều cao của cây rỗng (node NULL) là **-1** (hoặc một số tài liệu dùng quy ước node lá có chiều cao 0 — quan trọng là nhất quán trong toàn bộ cài đặt).

**Một cây là cây AVL hợp lệ khi và chỉ khi mọi node trong cây đều có** `BalanceFactor ∈ {-1, 0, 1}`.

| Giá trị BalanceFactor | Ý nghĩa |
|---|---|
| `0` | Hai cây con có chiều cao bằng nhau — cân bằng hoàn hảo |
| `1` | Cây con trái cao hơn cây con phải đúng 1 mức — vẫn hợp lệ |
| `-1` | Cây con phải cao hơn cây con trái đúng 1 mức — vẫn hợp lệ |
| `≥ 2` hoặc `≤ -2` | **Mất cân bằng** — cần thực hiện phép quay để khôi phục |

### Tại sao giới hạn chênh lệch chỉ ±1 vẫn đảm bảo O(log n)?

Đây là kết quả toán học quan trọng của cấu trúc AVL: có thể chứng minh rằng với ràng buộc "chênh lệch chiều cao 2 cây con tối đa 1" áp dụng cho mọi node, số node tối thiểu của một cây AVL chiều cao `h` tăng theo cấp số nhân xấp xỉ tỉ lệ vàng (không phải tuyến tính) — dẫn tới `h = O(log n)` được đảm bảo trong **mọi** trường hợp, kể cả trường hợp xấu nhất. Đây chính là điểm khác biệt cốt lõi so với BST thường (chỉ đạt O(log n) ở trường hợp trung bình/tốt, có thể tụt xuống O(n) ở trường hợp xấu).

### Cần lưu thêm thông tin gì trong mỗi node?

Để tính `BalanceFactor` hiệu quả (không phải tính lại chiều cao từ đầu mỗi lần), cài đặt AVL thường lưu thêm trường **`Height`** ngay tại mỗi node, được cập nhật lại sau mỗi lần Insert/Delete/Rotation:

```csharp
class AVLNode
{
    public int Data;
    public AVLNode Left;
    public AVLNode Right;
    public int Height;   // chiều cao của cây con gốc tại node này
}
```

## Độ phức tạp

| Thao tác | BST thường (worst case) | AVL (mọi trường hợp) |
|---|---|---|
| Search | O(n) | **O(log n)** |
| Insert | O(n) | **O(log n)** (bao gồm cả chi phí kiểm tra & cân bằng lại) |
| Delete | O(n) | **O(log n)** |

Cái giá phải trả để đạt được đảm bảo này: sau mỗi lần Insert/Delete, cần **kiểm tra và có thể thực hiện phép quay** để khôi phục cân bằng — chi tiết được trình bày ở [Các trường hợp mất cân bằng & phép quay](../46-avl-rotations/) và [Thêm/xóa node trong cây AVL](../47-avl-insert-delete/).

## Ví dụ

Quy ước: chiều cao node lá = 0, chiều cao node NULL = -1.

```
Cây AVL hợp lệ (mọi BalanceFactor trong {-1, 0, 1}):

          8      height=2, BF = height(3) - height(10) = 1 - 1 = 0
        /   \
       3     10   height=1, BF = height(1)-height(6) = 0-0 = 0   |   height=1, BF = height(NULL)-height(14) = -1-0 = -1
      / \      \
     1   6      14   height=0, BF=0 (đều là lá)

=> Mọi node đều có BF trong {-1, 0, 1} => đây là cây AVL hợp lệ.

Cây KHÔNG hợp lệ (không phải AVL) — chèn liên tiếp 8, 3, 1, 0 mà không cân bằng lại:

   8   height=3, BF = height(3) - height(NULL) = 2 - (-1) = 3
  /
 3    height=2, BF = height(1) - height(NULL) = 1 - (-1) = 2   <- đã mất cân bằng tại đây
/
1    height=1, BF = height(0) - height(NULL) = 0 - (-1) = 1
/
0    height=0, lá

=> Ngay tại node 3 đã có BF = 2 (vượt ngoài {-1,0,1}) => mất cân bằng,
   cần phép quay để khôi phục (xem bài tiếp theo).
```
