# Các trường hợp mất cân bằng & phép quay (LL, LR, RR, RL)

## Khái niệm

Khi một node trong cây AVL có [chỉ số cân bằng](../45-avl-tree-fundamentals/) vượt ra ngoài khoảng `{-1, 0, 1}` (tức `BalanceFactor ≥ 2` hoặc `≤ -2`), cây cần được **cấu trúc lại cục bộ** bằng một hoặc hai **phép quay (rotation)** để khôi phục tính chất AVL — mà **không làm mất tính chất thứ tự của BST**.

## Giải thích chi tiết

### Hai phép quay cơ bản

**Quay phải (Rotate Right)** — dùng khi cây con **trái** quá cao:

```
      y                x
     / \              / \
    x   T3    -->    T1  y
   / \                   / \
  T1 T2                 T2 T3
```
```
FUNCTION RotateRight(y)
    x = y.Left
    T2 = x.Right
    x.Right = y
    y.Left = T2
    RETURN x        // x trở thành gốc mới của cây con
END FUNCTION
```

**Quay trái (Rotate Left)** — đối xứng, dùng khi cây con **phải** quá cao:

```
    x                    y
   / \                  / \
  T1  y      -->       x   T3
     / \               / \
    T2 T3             T1 T2
```
```
FUNCTION RotateLeft(x)
    y = x.Right
    T2 = y.Left
    y.Left = x
    x.Right = T2
    RETURN y        // y trở thành gốc mới của cây con
END FUNCTION
```

Cả hai phép quay đều **O(1)** — chỉ thay đổi một vài con trỏ, không đụng vào phần còn lại của cây. Quan trọng: sau phép quay, LNR (in-order) của cây con **không đổi** — tính chất thứ tự BST luôn được bảo toàn.

### Bốn trường hợp mất cân bằng

Sau khi chèn (hoặc xóa) một node, việc mất cân bằng tại node `z` (là node gần nhất tính từ dưới lên có `BF ∉ {-1,0,1}`) rơi vào đúng 1 trong 4 trường hợp, tùy theo **nhánh nào bị lệch**:

| Trường hợp | Điều kiện | Cách khắc phục |
|---|---|---|
| **LL** | `z` lệch trái (BF ≥ 2), và con trái của `z` cũng lệch trái (hoặc cân bằng) | 1 phép quay phải tại `z` |
| **RR** | `z` lệch phải (BF ≤ -2), và con phải của `z` cũng lệch phải (hoặc cân bằng) | 1 phép quay trái tại `z` |
| **LR** | `z` lệch trái (BF ≥ 2), nhưng con trái của `z` lại lệch **phải** | 2 phép quay: quay trái tại con trái của `z`, rồi quay phải tại `z` |
| **RL** | `z` lệch phải (BF ≤ -2), nhưng con phải của `z` lại lệch **trái** | 2 phép quay: quay phải tại con phải của `z`, rồi quay trái tại `z` |

Cách nhớ: tên trường hợp ghép từ **hướng lệch của z** rồi đến **hướng lệch của con** gây mất cân bằng đó. Nếu hai hướng **giống nhau** (LL, RR) → chỉ cần 1 phép quay đơn. Nếu hai hướng **ngược nhau** (LR, RL) → cần 2 phép quay (quay kép), vì phải "duỗi thẳng" nhánh trước khi quay đơn mới có tác dụng.

### Trường hợp LR và RL — vì sao cần quay kép?

Nếu chỉ áp dụng 1 phép quay phải trực tiếp cho trường hợp LR (giống như LL), cây con lệch phải ở giữa sẽ khiến kết quả **vẫn mất cân bằng** theo hướng khác. Phép quay đầu tiên (quay trái tại con trái của `z`) có tác dụng biến đổi hình dạng LR trở thành hình dạng LL, sau đó phép quay thứ hai (quay phải tại `z`) mới thực sự cân bằng được cây — tương tự RL biến đổi thành RR trước khi quay trái.

## Độ phức tạp

| | Big-O |
|---|---|
| 1 phép quay (đơn hoặc mỗi phép trong quay kép) | O(1) |
| Xác định trường hợp nào (dựa vào BF của z và con) | O(1) |

Phép quay chỉ tốn O(1) vì chỉ thao tác cục bộ trên 2-3 node — đây là lý do [Thêm/xóa node trong AVL](../47-avl-insert-delete/) vẫn giữ được tổng chi phí O(log n) dù có thêm bước cân bằng lại.

## Ví dụ

```
Trường hợp LL — chèn 10, 20, 30 (theo thứ tự giảm dần khi duyệt xuống):

    30                20
   /                  /  \
  20        -->      10   30
 /
10

Trường hợp LR — chèn 30, 10, 20:

    30                20
   /                  /  \
  10        -->      10   30
   \
    20
```

## Demo

Xem file [demo.html](./demo.html) — chọn 1 trong 4 trường hợp (LL/RR/LR/RL), xem cây ban đầu bị mất cân bằng (chỉ số BF hiển thị tại mỗi node), rồi chạy từng bước để xem phép quay khôi phục lại cân bằng.
