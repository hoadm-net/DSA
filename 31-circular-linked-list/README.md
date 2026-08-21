# Danh sách liên kết vòng (giới thiệu)

## Khái niệm

Danh sách liên kết vòng (circular linked list) là danh sách liên kết mà **node cuối cùng không trỏ tới `NULL`**, mà trỏ **quay ngược về node đầu tiên (head)** — tạo thành một vòng khép kín không có điểm kết thúc rõ ràng.

## Giải thích chi tiết

### Cấu trúc

Về cấu tạo node, danh sách liên kết vòng đơn giống hệt danh sách liên kết đơn thông thường (chỉ có `Data` và `Next`) — điểm khác biệt duy nhất nằm ở **giá trị của `Next` tại node cuối**: thay vì `NULL`, nó trỏ về `head`.

```
[data|next]->[data|next]->[data|next]-+
     ^_______________________________|
   head                          (node cuối trỏ về head)
```

Danh sách liên kết vòng cũng có thể xây dựng dựa trên danh sách liên kết đôi (mỗi node có cả `Next` và `Prev`, với `Prev` của head trỏ tới node cuối) — gọi là **danh sách liên kết đôi vòng**.

### Hệ quả quan trọng: không còn điều kiện dừng "gặp NULL"

Vì không có node nào trỏ tới `NULL`, điều kiện dừng khi duyệt **không thể** dùng `p != NULL` như danh sách thông thường — nếu dùng nhầm điều kiện này, vòng lặp duyệt sẽ **chạy vô hạn**, liên tục xoay vòng qua các node mãi mãi (vi phạm [tính dừng của giải thuật](../08-algorithm-characteristics/)).

Điều kiện dừng đúng khi duyệt một danh sách vòng: dừng lại khi con trỏ duyệt **quay trở lại head** (tức `p.Next == head`, hoặc dùng một biến đếm số node đã duyệt).

```
FUNCTION TraverseCircular(head)
    IF head == NULL THEN RETURN
    p = head
    DO
        Xử lý p.Data
        p = p.Next
    WHILE p != head        // dừng khi quay lại head, không phải khi gặp NULL
END FUNCTION
```

### Ứng dụng thực tế

- **Lập lịch quay vòng (round-robin scheduling)**: hệ điều hành cấp phát CPU luân phiên cho các tiến trình theo vòng, tiến trình cuối cùng lại quay về tiến trình đầu — mô hình tự nhiên bằng danh sách liên kết vòng.
- **Bộ đệm vòng (circular buffer)**: một số cài đặt hàng đợi vòng (xem [Cài đặt Queue bằng mảng dạng vòng](../38-queue-array-implementation/)) áp dụng ý tưởng tương tự, dù thường dùng mảng thay vì con trỏ.
- **Trò chơi/ứng dụng có tính chu kỳ**: ví dụ chia bài luân phiên cho nhiều người chơi theo vòng.

## Độ phức tạp

Độ phức tạp các thao tác cơ bản (thêm, xóa, duyệt) tương đương danh sách liên kết đơn thông thường — O(1) cho thêm vào đầu (nếu có giữ con trỏ tới node cuối để cập nhật `Next`), O(n) cho duyệt/tìm kiếm. Điểm khác biệt chỉ nằm ở **điều kiện dừng khi duyệt**, không phải ở độ phức tạp.

## Demo

Xem file [demo.html](./demo.html) — khởi tạo danh sách liên kết vòng, chạy từng bước để thấy con trỏ `p` đi qua các node và **quay trở lại head** thay vì dừng ở `NULL`; demo giới hạn số bước hiển thị để minh họa vòng lặp sẽ tiếp diễn vô hạn nếu không có điều kiện dừng đúng.
