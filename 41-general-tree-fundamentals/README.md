# Khái niệm cây tổng quát & cách biểu diễn

## Khái niệm

Cây (tree) là một cấu trúc dữ liệu **phi tuyến** (non-linear), biểu diễn quan hệ **phân cấp** giữa các phần tử — khác với các cấu trúc tuyến tính đã học (mảng, [danh sách liên kết](../23-linked-list-fundamentals/), [Stack](../32-stack-fundamentals/), [Queue](../37-queue-fundamentals/)), nơi mỗi phần tử chỉ có tối đa một phần tử "trước" và một phần tử "sau". Trong cây, một phần tử (node) có thể có **nhiều node con**, tạo thành cấu trúc phân nhánh.

## Giải thích chi tiết

### Thuật ngữ cơ bản

| Thuật ngữ | Ý nghĩa |
|---|---|
| **Node (nút)** | Đơn vị cơ bản của cây, chứa dữ liệu |
| **Root (gốc)** | Node duy nhất không có node cha, là điểm bắt đầu của cây |
| **Parent (cha) / Child (con)** | Quan hệ trực tiếp giữa hai node liền kề theo cấp bậc |
| **Sibling (anh em)** | Các node có chung node cha |
| **Leaf (lá)** | Node không có node con nào |
| **Subtree (cây con)** | Một node cùng toàn bộ các node con cháu của nó, tự nó cũng là một cây |
| **Degree (bậc của node)** | Số node con trực tiếp của một node |
| **Height (chiều cao cây)** | Số cạnh trên đường đi dài nhất từ root xuống một lá |
| **Depth/Level (độ sâu của node)** | Số cạnh trên đường đi từ root tới node đó |

### Tính chất

- Cây có đúng **một root**, mọi node khác đều có đúng **một node cha** (khác với đồ thị tổng quát, nơi một node có thể có nhiều "cha").
- Không có chu trình (cycle) — không thể đi từ một node quay trở lại chính nó qua các cạnh.
- Một cây gồm `n` node luôn có đúng `n - 1` cạnh (liên kết).

### Cây nhị phân — trường hợp đặc biệt quan trọng

Khi mỗi node có **tối đa 2 node con** (thường phân biệt rõ con trái/con phải), ta có **cây nhị phân (binary tree)** — trường hợp đặc biệt được dùng nhiều nhất trong CTDL&GT, sẽ được trình bày chi tiết ở [Cây nhị phân: tính chất & duyệt cây](../42-binary-tree-traversal/) và [Cây nhị phân tìm kiếm (BST)](../43-binary-search-tree/).

### Cách biểu diễn cây trong bộ nhớ

1. **Danh sách con (child list)**: mỗi node lưu một danh sách/mảng con trỏ tới tất cả các node con của nó — phù hợp với cây có số con không giới hạn.
2. **Con trỏ cố định (cho cây nhị phân)**: mỗi node chỉ cần 2 con trỏ `Left` và `Right` — đơn giản và hiệu quả, vì số con đã biết trước tối đa là 2.
3. **Biểu diễn bằng mảng**: với cây nhị phân gần như đầy đủ (ví dụ [Heap](../21-heap-sort/)), có thể lưu các node liên tục trong mảng, với node tại chỉ số `i` có con trái ở `2i+1`, con phải ở `2i+2` — không cần con trỏ.

### So sánh với các cấu trúc đã học

| Cấu trúc | Loại | Số "phần tử kế tiếp" tối đa mỗi phần tử |
|---|---|---|
| Mảng, Danh sách liên kết, Stack, Queue | Tuyến tính | 1 |
| Cây nhị phân | Phi tuyến, phân cấp | 2 (trái, phải) |
| Cây tổng quát | Phi tuyến, phân cấp | Không giới hạn |

## Ví dụ

```
                A               <- root, depth 0
              /   \
             B     C            <- depth 1, đều là con của A
            / \      \
           D   E      F         <- depth 2; D, E, F là lá (leaf)

Height của cây = 2 (đường dài nhất A -> B -> D hoặc A -> B -> E)
B có 2 con (degree = 2), C có 1 con (degree = 1), D/E/F đều là lá (degree = 0)
```
