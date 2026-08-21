# Cây nhị phân: tính chất & duyệt cây (NLR, LNR, LRN)

## Khái niệm

Cây nhị phân (binary tree) là cây mà **mỗi node có tối đa 2 node con**, được phân biệt rõ ràng là **con trái (Left)** và **con phải (Right)**. Duyệt cây (traversal) là quá trình đi qua tất cả các node của cây theo một thứ tự xác định — vì cây là cấu trúc phi tuyến, có nhiều cách duyệt hợp lý khác nhau, không chỉ một cách như duyệt danh sách liên kết.

## Giải thích chi tiết

### Cấu tạo Node của cây nhị phân

```csharp
class TreeNode
{
    public int Data;
    public TreeNode Left;
    public TreeNode Right;
}
```

### Ba cách duyệt dựa trên đệ quy (Depth-First)

Cả ba cách đều duyệt theo chiều sâu (đi hết một nhánh trước khi quay lại), chỉ khác nhau ở **thời điểm "thăm" (xử lý) node hiện tại** so với việc duyệt hai cây con:

| Tên gọi | Thứ tự | Thời điểm xử lý Node |
|---|---|---|
| **NLR** (Node — Left — Right) | Tiền tố / Pre-order | Xử lý Node **trước**, rồi mới duyệt cây con trái, cây con phải |
| **LNR** (Left — Node — Right) | Trung tố / In-order | Duyệt cây con trái trước, xử lý Node **ở giữa**, rồi duyệt cây con phải |
| **LRN** (Left — Right — Node) | Hậu tố / Post-order | Duyệt cả hai cây con trước, xử lý Node **sau cùng** |

### Đặc điểm và ứng dụng của từng cách

- **NLR (Pre-order)**: phù hợp khi cần xử lý node cha **trước** node con (ví dụ: sao chép/nhân bản cây — phải tạo node cha trước khi tạo các con).
- **LNR (In-order)**: với [cây nhị phân tìm kiếm (BST)](../43-binary-search-tree/), duyệt LNR luôn cho ra dãy giá trị **đã sắp xếp tăng dần** — đây là tính chất quan trọng nhất của LNR.
- **LRN (Post-order)**: phù hợp khi cần xử lý node con **trước** node cha (ví dụ: giải phóng bộ nhớ của cây — phải giải phóng hết các con trước khi giải phóng node cha; tính giá trị biểu thức từ cây biểu thức).

### Cả ba cách đều dùng đệ quy tự nhiên

```
FUNCTION NLR(node)
    IF node == NULL THEN RETURN
    Xử lý node.Data
    NLR(node.Left)
    NLR(node.Right)
END FUNCTION

FUNCTION LNR(node)
    IF node == NULL THEN RETURN
    LNR(node.Left)
    Xử lý node.Data
    LNR(node.Right)
END FUNCTION

FUNCTION LRN(node)
    IF node == NULL THEN RETURN
    LRN(node.Left)
    LRN(node.Right)
    Xử lý node.Data
END FUNCTION
```

Về bản chất, đệ quy ở đây hoạt động dựa trên [ngăn xếp lời gọi hàm](../36-stack-application-recursion-removal/) — mỗi lời gọi đệ quy tương ứng với việc "đi xuống" một node con, và quay lui khi gặp `NULL`.

## Độ phức tạp

| Thao tác | Big-O |
|---|---|
| Duyệt toàn bộ cây có n node (cả 3 cách) | O(n) — mỗi node được thăm đúng 1 lần |
| Bộ nhớ phụ (độ sâu ngăn xếp đệ quy) | O(h), với h là chiều cao cây — O(log n) nếu cây cân bằng, O(n) nếu cây suy biến thành đường thẳng |

## Ví dụ

```
          8
        /   \
       3     10
      / \      \
     1   6      14
        / \
       4   7

NLR (Pre-order):  8, 3, 1, 6, 4, 7, 10, 14
LNR (In-order):    1, 3, 4, 6, 7, 8, 10, 14   <- kết quả có thứ tự tăng dần vì đây là BST
LRN (Post-order):  1, 4, 7, 6, 3, 14, 10, 8
```

## Demo

Xem file [demo.html](./demo.html) — nhập một dãy giá trị để dựng cây (theo cách chèn của [BST](../43-binary-search-tree/)), chọn kiểu duyệt NLR/LNR/LRN, rồi chạy từng bước để xem thứ tự đệ quy "đi vào" từng node và thời điểm mỗi node được in ra.
