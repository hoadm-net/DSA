# Thêm/xóa node trong cây AVL

## Khái niệm

Thêm và xóa node trong cây AVL gồm hai giai đoạn: (1) thực hiện thao tác **giống hệt BST thường** ([Insert](../43-binary-search-tree/)/[Delete](../44-bst-delete-node/)), sau đó (2) **đi ngược từ node vừa thay đổi lên đến root**, tại mỗi node kiểm tra chỉ số cân bằng và thực hiện [phép quay](../46-avl-rotations/) nếu cần, để đảm bảo toàn bộ cây luôn giữ tính chất AVL.

## Giải thích chi tiết

### Thêm node (Insert)

1. Thực hiện chèn như BST thường: đi xuống từ root, so sánh và rẽ trái/phải cho đến khi gặp vị trí trống, chèn node mới vào đó.
2. **Trên đường lùi lại (unwind) từ node vừa chèn về root** (tự nhiên xảy ra khi cài đặt đệ quy — xem [khử đệ quy](../36-stack-application-recursion-removal/) để hiểu cơ chế ngăn xếp lời gọi hàm đứng sau việc "lùi lại" này): tại mỗi node tổ tiên, cập nhật lại chiều cao, tính `BalanceFactor`.
3. Nếu phát hiện mất cân bằng tại một node `z` (BF ∉ {-1,0,1}): xác định trường hợp LL/RR/LR/RL dựa vào **giá trị vừa chèn** so với `z` và con của `z`, rồi thực hiện phép quay tương ứng.
4. **Chỉ cần cân bằng lại tại node mất cân bằng gần nhất** (thấp nhất) tính từ node vừa chèn lên — sau khi quay tại đó, toàn bộ cây phía trên tự động trở lại cân bằng (có thể chứng minh: chiều cao cây con sau khi quay bằng đúng chiều cao trước khi chèn).

### Xóa node (Delete)

1. Thực hiện xóa như BST thường: tìm node cần xóa, xử lý theo [3 trường hợp lá/1 con/2 con](../44-bst-delete-node/) (trường hợp 2 con dùng successor).
2. Trên đường lùi lại từ vị trí vừa thay đổi về root: cập nhật chiều cao, tính `BalanceFactor` tại mỗi node tổ tiên, giống hệt Insert.
3. Nếu mất cân bằng: xác định trường hợp dựa vào **BalanceFactor của node con** (khác với Insert — Delete không dựa vào giá trị vừa xóa, vì giá trị đó đã không còn trong cây):
   - `BF(z) ≥ 2` và `BF(z.Left) ≥ 0` → LL
   - `BF(z) ≥ 2` và `BF(z.Left) < 0` → LR
   - `BF(z) ≤ -2` và `BF(z.Right) ≤ 0` → RR
   - `BF(z) ≤ -2` và `BF(z.Right) > 0` → RL
4. **Khác biệt quan trọng so với Insert**: xóa node có thể gây mất cân bằng **ở nhiều node tổ tiên khác nhau cùng lúc** (không dừng lại sau phép quay đầu tiên) — vì vậy quá trình kiểm tra/cân bằng lại phải tiếp tục **cho đến tận root**, không dừng sớm như Insert.

### So sánh Insert và Delete trong AVL

| | Insert | Delete |
|---|---|---|
| Số vị trí có thể mất cân bằng | Tối đa 1 (dừng ngay sau lần quay đầu tiên) | Có thể nhiều, phải kiểm tra tới tận root |
| Xác định trường hợp quay dựa vào | Giá trị vừa chèn so với node | BalanceFactor của node con |
| Số phép quay tối đa | 1 lần quay đơn hoặc 1 lần quay kép | O(log n) lần (mỗi tổ tiên có thể cần quay) |

## Độ phức tạp

| Thao tác | Big-O |
|---|---|
| Insert (bao gồm tìm vị trí + cân bằng lại) | O(log n) |
| Delete (bao gồm tìm node + cân bằng lại) | O(log n) |

Vì chiều cao cây AVL luôn là O(log n) (đảm bảo bởi chính cơ chế tự cân bằng này), mọi thao tác — bao gồm cả chi phí kiểm tra/quay bổ sung — vẫn nằm trong O(log n), **không có worst case O(n)** như BST thường bị suy biến.

## Ví dụ

```
FUNCTION Insert(node, x)
    IF node == NULL THEN RETURN NewNode(x)
    IF x < node.Data THEN node.Left = Insert(node.Left, x)
    ELSE IF x > node.Data THEN node.Right = Insert(node.Right, x)
    ELSE RETURN node                              // không chèn trùng

    UpdateHeight(node)
    balance = GetBalance(node)

    IF balance > 1 AND x < node.Left.Data THEN RETURN RotateRight(node)              // LL
    IF balance < -1 AND x > node.Right.Data THEN RETURN RotateLeft(node)             // RR
    IF balance > 1 AND x > node.Left.Data THEN
        node.Left = RotateLeft(node.Left)
        RETURN RotateRight(node)                                                     // LR
    IF balance < -1 AND x < node.Right.Data THEN
        node.Right = RotateRight(node.Right)
        RETURN RotateLeft(node)                                                      // RL

    RETURN node
END FUNCTION
```

## Demo

Xem file [demo.html](./demo.html) — dựng một cây AVL, rồi Insert/Delete từng giá trị và chạy từng bước để xem: đường đi so sánh, chỉ số BF được cập nhật tại từng node tổ tiên trên đường lùi lại, và phép quay (nếu có) được áp dụng đúng chỗ.
