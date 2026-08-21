# Cây nhiều nhánh (B-Tree): cấu trúc & xây dựng

## Khái niệm

B-Tree là cây tìm kiếm cân bằng **nhiều nhánh** (mỗi node có thể có nhiều hơn 2 con, khác với [BST](../43-binary-search-tree/)/[AVL](../45-avl-tree-fundamentals/) chỉ có tối đa 2 con), được thiết kế để **tối thiểu hóa số lần truy cập đĩa/bộ nhớ ngoài** — mỗi node B-Tree chứa nhiều khóa, tương ứng với việc đọc một khối dữ liệu (block) lớn trong một lần truy cập.

## Giải thích chi tiết

### Vì sao cần cây nhiều nhánh?

Với dữ liệu cực lớn (không nằm vừa trong RAM, phải lưu trên đĩa), chi phí đắt nhất không phải là số lần so sánh mà là **số lần truy cập đĩa**. Một cây nhị phân với hàng triệu node có chiều cao `log₂(n)` khá lớn (~20 với 1 triệu node) → 20 lần truy cập đĩa cho mỗi tìm kiếm. B-Tree cho mỗi node chứa **hàng trăm khóa** thay vì 1, khiến chiều cao cây giảm mạnh (`log_m(n)` với `m` lớn) → chỉ vài lần truy cập đĩa cho cả triệu bản ghi. Đây là lý do B-Tree (và các biến thể B+Tree) là cấu trúc lõi trong **hệ quản trị cơ sở dữ liệu** và **hệ thống tệp**.

### Định nghĩa (bậc tối thiểu t)

Một B-Tree có **bậc tối thiểu (minimum degree) t** thỏa các tính chất:

1. Mỗi node (trừ root) chứa từ `t - 1` đến `2t - 1` khóa (đã sắp xếp tăng dần trong node).
2. Mỗi node có `k` khóa thì có `k + 1` con (nếu không phải lá).
3. Root có ít nhất 1 khóa (trừ khi cây rỗng).
4. **Mọi node lá đều có cùng độ sâu** — đây là điểm khác biệt lớn với BST/AVL: B-Tree cân bằng bằng cách "phát triển đồng đều từ dưới lên" thay vì cân bằng từng nhánh riêng lẻ.
5. Với node nội bộ có khóa `k₁ < k₂ < ... < kₙ`, con thứ `i` chứa toàn bộ khóa nằm trong khoảng `(kᵢ₋₁, kᵢ)` — tổng quát hóa tính chất thứ tự của BST cho nhiều khóa hơn.

Bài học này minh họa với **t = 2** (mỗi node tối đa `2t - 1 = 3` khóa, tối đa `2t = 4` con) — trường hợp đặc biệt còn gọi là **cây 2-3-4**, đơn giản để hình dung nhưng vẫn thể hiện đầy đủ nguyên lý tổng quát của B-Tree bậc bất kỳ.

### Thêm khóa (Insert) — chiến lược "tách trước" (proactive splitting)

Khi một node đã đầy (`2t - 1` khóa) mà cần thêm khóa vào, nó phải được **tách (split)** làm đôi: khóa ở giữa được **đẩy lên node cha**, hai nửa còn lại trở thành hai node con riêng biệt.

Để tránh phải quay lui xử lý tách nhiều lần (backtracking), B-Tree áp dụng chiến lược: **trong lúc đi xuống tìm vị trí chèn, hễ gặp node con nào đã đầy thì tách nó trước khi đi tiếp vào đó** — đảm bảo khi đến được node lá, chắc chắn còn chỗ trống để chèn ngay, không cần quay lại xử lý.

```
FUNCTION InsertNonFull(node, key)
    IF node.IsLeaf THEN
        Chèn key vào đúng vị trí (giữ thứ tự) trong node.Keys
    ELSE
        i = tìm vị trí con cần đi xuống dựa theo key
        IF node.Children[i] đã đầy (2t-1 khóa) THEN
            SplitChild(node, i)              // tách trước khi đi xuống
            IF key > node.Keys[i] THEN i = i + 1
        END IF
        InsertNonFull(node.Children[i], key)
    END IF
END FUNCTION

FUNCTION Insert(tree, key)
    IF root đã đầy THEN
        Tạo root mới, con duy nhất là root cũ
        SplitChild(root mới, 0)              // tách root cũ, cây tăng thêm 1 tầng
    END IF
    InsertNonFull(root, key)
END FUNCTION
```

Vì luôn "tách trước", chiều cao cây B-Tree chỉ tăng lên **duy nhất khi root bị tách** — đây chính là cách B-Tree đảm bảo mọi lá luôn cùng độ sâu (tính chất 4 ở trên) mà không cần các phép quay phức tạp như AVL.

## Độ phức tạp

| Thao tác | Big-O (n khóa, bậc tối thiểu t) |
|---|---|
| Tìm kiếm | O(log_t n) |
| Thêm | O(log_t n) |
| Xóa | O(log_t n) |
| Số lần truy cập đĩa mỗi thao tác | O(log_t n) — nhỏ hơn nhiều so với O(log₂ n) của cây nhị phân khi t lớn |

## Ví dụ

```
Chèn lần lượt 10, 20, 30 vào cây B-Tree rỗng với t=2 (tối đa 3 khóa/node):

Chèn 10, 20:  [10, 20]                     (node lá duy nhất, chưa đầy)

Chèn 30:      [10, 20, 30]                 (đã đầy, 3 khóa = 2t-1)

Chèn 40:      Node lá đã đầy (3 khóa) → phải tách trước khi chèn:
                    [20]
                   /    \
              [10]      [30]
              rồi chèn 40 vào node lá bên phải:
                    [20]
                   /    \
              [10]      [30, 40]
```

## Demo

Xem file [demo.html](./demo.html) — chèn từng khóa vào cây B-Tree (t=2), chạy từng bước để xem quá trình đi xuống tìm vị trí và các lần tách node khi gặp node đầy.
