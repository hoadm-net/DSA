# Chèn node vào danh sách (theo vị trí/theo thứ tự)

## Khái niệm

Ngoài thêm vào đầu hoặc cuối, danh sách liên kết còn hỗ trợ **chèn node vào một vị trí bất kỳ ở giữa** — theo chỉ số vị trí cho trước, hoặc theo đúng thứ tự giá trị (nếu danh sách đang được duy trì có thứ tự).

## Giải thích chi tiết

### Chèn theo vị trí (Insert by Position)

Để chèn giá trị mới vào vị trí thứ `k` (0-based), cần:

1. Nếu `k == 0`: chèn vào đầu (xem [Thêm node vào đầu/cuối](../26-insert-node-at-head-tail/)).
2. Ngược lại: **duyệt tới node đứng trước vị trí `k`** (gọi là `prev`, node thứ `k-1`).
3. Tạo `newNode`, gán `newNode.Next = prev.Next`.
4. Gán `prev.Next = newNode`.

Thứ tự bước 3 rồi mới đến bước 4 là **bắt buộc** — nếu đổi ngược lại, con trỏ tới phần còn lại của danh sách (`prev.Next` cũ) sẽ bị mất trước khi kịp gán cho `newNode.Next`.

### Chèn theo thứ tự (Ordered Insert)

Khi danh sách đang được duy trì có thứ tự tăng dần, chèn một giá trị mới cần tìm đúng vị trí để **giữ nguyên tính có thứ tự** sau khi chèn:

1. Duyệt từ đầu danh sách, dùng con trỏ `prev` và `curr`, cho đến khi `curr == NULL` hoặc `curr.Data >= value` (đã tìm được vị trí thích hợp — ngay trước `curr`).
2. Tạo `newNode`, gán `newNode.Next = curr`.
3. Nếu `prev == NULL` (chèn ngay tại đầu): `head = newNode`. Ngược lại: `prev.Next = newNode`.

## Độ phức tạp

| Thao tác | Big-O |
|---|---|
| Chèn theo vị trí `k` (phải duyệt tới vị trí `k-1`) | O(k), tệ nhất O(n) |
| Chèn theo thứ tự (phải duyệt tìm đúng vị trí) | O(n) trong trường hợp xấu nhất |
| Bản thân thao tác chèn khi đã có `prev` | O(1) |

Lưu ý: chi phí chính nằm ở việc **duyệt tìm vị trí** (O(n)), không phải ở thao tác chèn (O(1)) — đây là điểm khác biệt so với chèn vào giữa mảng, nơi chi phí chính nằm ở việc **dịch chuyển phần tử** (cũng O(n), nhưng do dịch chuyển chứ không phải do duyệt).

## Ví dụ

```
FUNCTION InsertAtPosition(head, k, value)
    IF k == 0 THEN
        RETURN InsertAtHead(head, value)
    END IF
    prev = head
    FOR i = 1 TO k - 1
        prev = prev.Next
    END FOR
    newNode = Node(value)
    newNode.Next = prev.Next
    prev.Next = newNode
    RETURN head
END FUNCTION

FUNCTION OrderedInsert(head, value)
    newNode = Node(value)
    IF head == NULL OR head.Data >= value THEN
        newNode.Next = head
        RETURN newNode          // node mới trở thành head
    END IF
    prev = head
    WHILE prev.Next != NULL AND prev.Next.Data < value
        prev = prev.Next
    END WHILE
    newNode.Next = prev.Next
    prev.Next = newNode
    RETURN head
END FUNCTION
```

## Demo

Xem file [demo.html](./demo.html) — khởi tạo danh sách, chọn chèn theo vị trí cụ thể hoặc chèn theo đúng thứ tự tăng dần, chạy từng bước để xem con trỏ `prev` di chuyển tìm đúng vị trí trước khi chèn.
