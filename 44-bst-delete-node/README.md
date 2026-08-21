# Xóa node khỏi BST (3 trường hợp: lá, 1 con, 2 con)

## Khái niệm

Xóa một node khỏi [cây nhị phân tìm kiếm (BST)](../43-binary-search-tree/) phức tạp hơn xóa trên [danh sách liên kết](../28-delete-node/), vì sau khi xóa, cây **phải tiếp tục thỏa mãn tính chất thứ tự của BST**. Cách xử lý phụ thuộc vào node cần xóa có bao nhiêu con — chia thành 3 trường hợp.

## Giải thích chi tiết

### Trường hợp 1 — Node cần xóa là lá (không có con)

Đơn giản nhất: chỉ cần cho node cha của nó trỏ tới `NULL` thay vì trỏ tới node đó.

```
      8                    8
     / \        xóa 1     / \
    3   10     ------>   3   10
   /
  1
```

### Trường hợp 2 — Node cần xóa có đúng 1 con

Cho node cha trỏ thẳng tới **con duy nhất** của node cần xóa, "bỏ qua" node đó — giống hệt cách [xóa node giữa danh sách liên kết](../28-delete-node/).

```
      8                    8
     / \        xóa 10    / \
    3   10     ------>   3   14
          \
           14
```

### Trường hợp 3 — Node cần xóa có đủ 2 con

Phức tạp nhất: không thể chỉ đơn giản nối node cha với một trong hai con (sẽ mất con còn lại). Giải pháp chuẩn:

1. Tìm **node thế mạng (successor)** — chính là **phần tử nhỏ nhất trong cây con phải** của node cần xóa (đi sang phải một lần, rồi liên tục sang trái cho đến khi hết con trái). Giá trị này là giá trị **nhỏ nhất trong số các giá trị lớn hơn** node cần xóa — vị trí hợp lệ duy nhất để thay thế mà không phá vỡ tính chất BST.
2. **Sao chép giá trị** của successor vào node cần xóa (node cần xóa "biến thành" successor về mặt giá trị, nhưng vẫn giữ nguyên vị trí và các liên kết ban đầu).
3. **Xóa node successor gốc** khỏi vị trí cũ của nó. Vì successor là phần tử nhỏ nhất của cây con phải, nó **chắc chắn không có con trái** — nên việc xóa nó luôn rơi vào Trường hợp 1 hoặc Trường hợp 2 (đệ quy đơn giản hơn, không bao giờ quay lại Trường hợp 3).

```
      8                         8                         10
     / \         copy 10       / \         xóa 10 gốc     / \
    3   14      ------>       3   14       (TH2)  ---->  3   14
       /                         /
      10                       10 (giá trị đã copy lên trên)
```
*(Ví dụ trên: xóa node 8 có 2 con → successor là 10 (nhỏ nhất bên phải) → copy 10 lên vị trí node 8 → xóa node 10 gốc, node 10 gốc không có con nên rơi vào Trường hợp 1.)*

**Lưu ý**: có thể dùng **predecessor** (phần tử lớn nhất trong cây con trái) thay cho successor — cả hai đều hợp lệ và cho kết quả đúng, chỉ khác cây kết quả có hình dạng hơi khác nhau. Bài học này dùng successor theo quy ước phổ biến.

## Độ phức tạp

| Bước | Big-O |
|---|---|
| Tìm node cần xóa | O(h) |
| Tìm successor (nếu Trường hợp 3) | O(h) |
| Cập nhật liên kết | O(1) |
| **Tổng cộng** | **O(h)** — O(log n) nếu cây cân bằng, O(n) nếu cây suy biến |

Giống [Insert/Search](../43-binary-search-tree/), chi phí xóa phụ thuộc vào **chiều cao cây (h)**, không phải số node — đây tiếp tục là lý do cần cây cân bằng như [AVL](../45-avl-tree-fundamentals/).

## Ví dụ

```
FUNCTION Delete(node, x)
    IF node == NULL THEN RETURN NULL
    IF x < node.Data THEN
        node.Left = Delete(node.Left, x)
    ELSE IF x > node.Data THEN
        node.Right = Delete(node.Right, x)
    ELSE
        // đã tìm thấy node cần xóa
        IF node.Left == NULL THEN RETURN node.Right     // TH1 (lá) hoặc TH2 (chỉ có con phải)
        IF node.Right == NULL THEN RETURN node.Left      // TH2 (chỉ có con trái)

        // TH3: có đủ 2 con — tìm successor (nhỏ nhất bên phải)
        successor = node.Right
        WHILE successor.Left != NULL
            successor = successor.Left
        END WHILE
        node.Data = successor.Data                       // copy giá trị
        node.Right = Delete(node.Right, successor.Data)   // xóa successor gốc
    END IF
    RETURN node
END FUNCTION
```

## Demo

Xem file [demo.html](./demo.html) — dựng cây, chọn giá trị cần xóa, chạy từng bước để xem quá trình tìm node, xác định trường hợp (lá/1 con/2 con), và với trường hợp 2 con: tìm successor rồi xóa nó khỏi vị trí gốc.
