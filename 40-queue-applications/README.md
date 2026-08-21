# Ứng dụng Queue: bộ đệm, quản lý tiến trình

## Khái niệm

Nguyên tắc FIFO của Queue khiến nó trở thành lựa chọn tự nhiên cho mọi tình huống cần xử lý các yêu cầu/tác vụ **theo đúng thứ tự chúng đến**, đặc biệt trong hai nhóm ứng dụng phổ biến: **bộ đệm (buffer)** và **quản lý tiến trình (process scheduling)**.

## Giải thích chi tiết

### Bộ đệm (Buffer)

Khi tốc độ tạo ra dữ liệu và tốc độ xử lý dữ liệu không khớp nhau, một **hàng đợi đệm** được dùng để tạm giữ dữ liệu chờ xử lý, đảm bảo không mất dữ liệu và xử lý đúng thứ tự đến:

- **Bàn phím/chuột**: các sự kiện gõ phím được xếp vào hàng đợi, hệ điều hành xử lý lần lượt.
- **Hàng đợi in ấn (print spooler)**: nhiều yêu cầu in được xếp hàng, máy in xử lý lần lượt theo thứ tự gửi đến.
- **Streaming dữ liệu mạng**: gói tin đến được xếp vào buffer chờ xử lý, tránh mất dữ liệu khi tốc độ mạng nhanh hơn tốc độ xử lý.

### Quản lý tiến trình — Lập lịch Round-Robin

Trong hệ điều hành đa nhiệm, nhiều tiến trình cùng chờ được cấp phát CPU. Giải thuật **Round-Robin (RR)** — một trong những giải thuật lập lịch phổ biến nhất — sử dụng Queue để đảm bảo mọi tiến trình đều được cấp CPU một cách công bằng, luân phiên:

1. Tất cả tiến trình đang chờ được xếp vào một hàng đợi (Queue).
2. Lấy tiến trình ở đầu hàng đợi (`Dequeue`), cấp CPU cho nó chạy trong tối đa một khoảng thời gian cố định gọi là **quantum** (lát cắt thời gian).
3. Nếu tiến trình chưa hoàn tất sau khi hết quantum: tạm dừng nó, đưa nó trở lại **cuối** hàng đợi (`Enqueue`) để chờ lượt tiếp theo.
4. Nếu tiến trình đã hoàn tất trong quantum đó: đánh dấu hoàn tất, không đưa trở lại hàng đợi.
5. Lặp lại từ bước 2 cho đến khi hàng đợi rỗng (mọi tiến trình đã hoàn tất).

Round-Robin đảm bảo **không có tiến trình nào phải chờ đợi vô hạn** (tránh hiện tượng đói tài nguyên — starvation), vì mọi tiến trình đều được luân phiên quay vòng qua Queue.

### Vì sao dùng Queue mà không dùng Stack?

Nếu dùng Stack (LIFO) để quản lý tiến trình chờ, tiến trình **mới được thêm vào gần đây nhất** sẽ luôn được ưu tiên xử lý trước — tiến trình đến sớm có thể bị "bỏ đói" vô thời hạn nếu liên tục có tiến trình mới chen vào. Queue (FIFO) đảm bảo tính công bằng: đến trước, được phục vụ trước.

## Độ phức tạp

| Thao tác | Big-O |
|---|---|
| Enqueue/Dequeue mỗi tiến trình | O(1) |
| Tổng thời gian lập lịch cho n tiến trình, mỗi tiến trình cần trung bình k lượt quantum | O(n·k) — mỗi lượt chỉ tốn O(1) cho thao tác Queue |

## Ví dụ

```
3 tiến trình: P1 (burst = 5), P2 (burst = 3), P3 (burst = 8), quantum = 3

t=0: Queue = [P1, P2, P3]
t=0..3: chạy P1 (còn 2)   → Queue = [P2, P3, P1]
t=3..6: chạy P2 (còn 0, HOÀN TẤT)  → Queue = [P3, P1]
t=6..9: chạy P3 (còn 5)   → Queue = [P1, P3]
t=9..11: chạy P1 (còn 0, HOÀN TẤT) → Queue = [P3]
t=11..14: chạy P3 (còn 2) → Queue = [P3]
t=14..16: chạy P3 (còn 0, HOÀN TẤT)

Thứ tự hoàn tất: P2 (t=6), P1 (t=11), P3 (t=16)
```

## Demo

Xem file [demo.html](./demo.html) — nhập danh sách tiến trình và quantum, chạy từng bước để xem hàng đợi luân phiên, CPU đang xử lý tiến trình nào, và biểu đồ Gantt được xây dựng dần theo giải thuật Round-Robin.
