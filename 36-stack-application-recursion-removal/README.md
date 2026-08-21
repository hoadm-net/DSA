# Ứng dụng Stack: khử đệ quy

## Khái niệm

Đệ quy (recursion) — một hàm tự gọi lại chính nó — được ngôn ngữ lập trình hiện thực bằng cách sử dụng **ngăn xếp lời gọi hàm (call stack)** ẩn bên dưới: mỗi lần gọi hàm, thông tin về lời gọi đó (tham số, biến cục bộ, vị trí cần quay lại) được **đẩy (push)** vào call stack; khi hàm kết thúc, thông tin đó được **lấy ra (pop)** để quay lại đúng chỗ đã dừng. "Khử đệ quy" là kỹ thuật **tự tay dùng một Stack tường minh** để mô phỏng chính xác cơ chế đó, biến một giải thuật đệ quy thành giải thuật lặp (iterative).

## Giải thích chi tiết

### Vì sao cần khử đệ quy?

- Tránh nguy cơ **tràn ngăn xếp (stack overflow)** khi độ sâu đệ quy quá lớn (call stack hệ thống có giới hạn kích thước).
- Trong một số ngôn ngữ/môi trường, vòng lặp tường minh chạy **hiệu quả hơn** đệ quy (tránh chi phí tạo/hủy stack frame của mỗi lời gọi hàm).
- Giúp hiểu rõ **bản chất hoạt động thật sự** của đệ quy — đây là mục tiêu chính khi học kỹ thuật này.

### Ý tưởng cốt lõi: mô phỏng "khung" (frame) bằng Stack tường minh

Với mỗi lời gọi đệ quy, ta lưu vào Stack một **"khung"** gồm: các tham số của lời gọi, và một **biến trạng thái (state)** đánh dấu hàm đang "dừng ở đâu" trong thân hàm (vì một hàm đệ quy thường gọi chính nó ở nhiều chỗ khác nhau, xen giữa các thao tác khác — ví dụ Hanoi gọi đệ quy 2 lần, trước và sau khi in ra một bước di chuyển).

Với bài toán kinh điển **Tháp Hà Nội (Tower of Hanoi)** — chuyển `n` đĩa từ cọc `from` sang cọc `to`, dùng cọc `via` làm trung gian:

```
FUNCTION Hanoi(n, from, to, via)      // bản đệ quy gốc
    IF n == 0 THEN RETURN
    Hanoi(n - 1, from, via, to)        // lời gọi đệ quy thứ 1
    In "Chuyển đĩa n từ from sang to"
    Hanoi(n - 1, via, to, from)        // lời gọi đệ quy thứ 2
END FUNCTION
```

Mỗi khung có 3 trạng thái tương ứng 3 việc cần làm khi khung đó "được xử lý":

- **state = 0**: mới được đẩy vào — chuẩn bị thực hiện lời gọi đệ quy thứ 1.
- **state = 1**: lời gọi đệ quy thứ 1 đã xong (đã quay lại) — in ra bước di chuyển, rồi chuẩn bị thực hiện lời gọi đệ quy thứ 2.
- **state = 2**: lời gọi đệ quy thứ 2 đã xong — khung này hoàn tất, lấy ra khỏi Stack (tương đương hàm `return`).

### Giải thuật khử đệ quy (dùng Stack tường minh)

```
Đẩy khung (n, from, to, via, state=0) vào Stack
WHILE Stack không rỗng
    top = đỉnh Stack (không lấy ra)
    IF top.state == 0 THEN
        top.state = 1
        IF top.n > 0 THEN
            Đẩy khung (top.n - 1, top.from, top.via, top.to, state=0)
        END IF
    ELSE IF top.state == 1 THEN
        top.state = 2
        IF top.n > 0 THEN
            In "Chuyển đĩa top.n từ top.from sang top.to"
            Đẩy khung (top.n - 1, top.via, top.to, top.from, state=0)
        END IF
    ELSE  // top.state == 2
        Lấy khung ra khỏi Stack (khung này đã xử lý xong)
    END IF
END WHILE
```

So khớp từng bước với hàm đệ quy gốc: "đẩy khung mới" ⟺ "gọi hàm con"; "lấy khung ra" ⟺ "hàm return, quay lại nơi gọi nó". Kỹ thuật đánh dấu `state` này áp dụng được cho **mọi** giải thuật đệ quy, không riêng gì Hanoi.

## Độ phức tạp

| | Bản đệ quy | Bản khử đệ quy (Stack tường minh) |
|---|---|---|
| Số lời gọi/khung xử lý | O(2ⁿ) (Hanoi có 2 lời gọi đệ quy mỗi lần) | O(2ⁿ) — không đổi |
| Bộ nhớ | O(n) (độ sâu call stack ẩn) | O(n) (độ sâu Stack tường minh) |

Khử đệ quy **không làm thay đổi độ phức tạp thời gian/không gian** của giải thuật — nó chỉ thay ngăn xếp lời gọi hàm **ẩn** (do ngôn ngữ quản lý) bằng một ngăn xếp **tường minh** (do người lập trình tự quản lý).

## Demo

Xem file [demo.html](./demo.html) — chọn số đĩa, chạy từng bước để xem Stack tường minh được đẩy/lấy ra như thế nào, đối chiếu với 3 cọc Tháp Hà Nội và nhật ký các bước di chuyển được sinh ra.
