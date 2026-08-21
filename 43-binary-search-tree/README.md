# Cây nhị phân tìm kiếm (BST): định nghĩa & thao tác thêm/tìm

## Khái niệm

Cây nhị phân tìm kiếm (Binary Search Tree — BST) là [cây nhị phân](../42-binary-tree-traversal/) thỏa mãn **tính chất thứ tự**: với **mọi node**, tất cả giá trị trong cây con trái **nhỏ hơn** giá trị của node đó, và tất cả giá trị trong cây con phải **lớn hơn** giá trị của node đó.

## Giải thích chi tiết

### Tính chất thứ tự

Tính chất này áp dụng **đệ quy cho mọi node**, không chỉ ở node gốc — nghĩa là mỗi cây con của một BST cũng phải là một BST hợp lệ. Nhờ tính chất này, duyệt [LNR (in-order)](../42-binary-tree-traversal/) trên BST luôn cho ra dãy giá trị **đã sắp xếp tăng dần**.

### Thao tác Tìm kiếm (Search)

Nhờ tính chất thứ tự, tìm kiếm trong BST hoạt động tương tự [tìm kiếm nhị phân trên mảng](../14-binary-search/) — mỗi bước so sánh loại bỏ được một nhánh con:

1. Bắt đầu từ `root`.
2. So sánh giá trị cần tìm `x` với giá trị node hiện tại:
   - Nếu bằng nhau → tìm thấy.
   - Nếu `x` nhỏ hơn → chỉ có thể nằm ở cây con **trái** → đi sang trái.
   - Nếu `x` lớn hơn → chỉ có thể nằm ở cây con **phải** → đi sang phải.
3. Lặp lại cho đến khi tìm thấy, hoặc đi tới `NULL` (không tìm thấy).

### Thao tác Thêm (Insert)

Về bản chất là một lần **tìm kiếm** giá trị mới cho đến khi gặp vị trí trống (`NULL`), rồi chèn node mới vào đúng vị trí đó — luôn giữ đúng tính chất BST:

1. Nếu cây rỗng: node mới trở thành `root`.
2. Ngược lại: so sánh giá trị cần thêm với node hiện tại, đi sang trái nếu nhỏ hơn, sang phải nếu lớn hơn, lặp lại cho đến khi gặp `NULL` — chèn node mới vào đúng chỗ đó.
3. Nếu giá trị đã tồn tại trong cây: tùy quy ước, thường **không chèn trùng**.

### Vì sao hiệu năng phụ thuộc vào hình dạng cây?

Chi phí tìm kiếm/thêm tỉ lệ với **chiều cao cây (h)**, không phải số node (n):

- Nếu cây **cân bằng** (mỗi nhánh có chiều cao gần bằng nhau): `h ≈ log₂(n)` → chi phí O(log n), rất nhanh.
- Nếu dữ liệu được chèn theo thứ tự **đã sắp xếp sẵn** (ví dụ chèn lần lượt 1, 2, 3, 4, 5): cây suy biến thành một **đường thẳng** giống hệt danh sách liên kết → `h = n` → chi phí O(n), mất hoàn toàn lợi thế của BST.

Đây chính là động lực cho [Cây nhị phân tìm kiếm cân bằng — AVL](../45-avl-tree-fundamentals/): tự động giữ cây luôn cân bằng để đảm bảo O(log n) trong **mọi** trường hợp, không phụ thuộc thứ tự chèn dữ liệu.

## Độ phức tạp

| Thao tác | Cây cân bằng (best/average) | Cây suy biến (worst case) |
|---|---|---|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |

## Ví dụ

```
FUNCTION Search(node, x)
    IF node == NULL OR node.Data == x THEN RETURN node
    IF x < node.Data THEN RETURN Search(node.Left, x)
    ELSE RETURN Search(node.Right, x)
END FUNCTION

FUNCTION Insert(node, x)
    IF node == NULL THEN RETURN NewNode(x)
    IF x < node.Data THEN
        node.Left = Insert(node.Left, x)
    ELSE IF x > node.Data THEN
        node.Right = Insert(node.Right, x)
    END IF
    RETURN node        // x == node.Data: không chèn trùng
END FUNCTION
```

```
Chèn lần lượt: 8, 3, 10, 1, 6, 14, 4, 7

          8
        /   \
       3     10
      / \      \
     1   6      14
        / \
       4   7

LNR (in-order) của cây này: 1, 3, 4, 6, 7, 8, 10, 14 — đã sắp xếp tăng dần.
```

## Demo

Xem file [demo.html](./demo.html) — chèn/tìm kiếm giá trị trên BST, chạy từng bước để xem đường đi so sánh từ root xuống, và cây được cập nhật trực quan sau mỗi lần chèn.
