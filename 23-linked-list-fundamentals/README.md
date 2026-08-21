# Khái niệm danh sách liên kết & so sánh với mảng

## Khái niệm

Danh sách liên kết (linked list) là cấu trúc dữ liệu gồm một dãy các **node**, mỗi node lưu trữ một giá trị dữ liệu và một (hoặc nhiều) **con trỏ (liên kết)** trỏ tới node kế tiếp. Các node không nhất thiết nằm liên tục trong bộ nhớ — chúng được kết nối với nhau thông qua con trỏ, thay vì thông qua vị trí liền kề như mảng.

## Giải thích chi tiết

### Cách hoạt động

Danh sách liên kết được truy cập thông qua một con trỏ đặc biệt gọi là **head** (đầu danh sách), trỏ tới node đầu tiên. Từ node đầu tiên, có thể lần theo con trỏ `next` của từng node để đi đến các node tiếp theo, cho tới khi gặp con trỏ `NULL` (báo hiệu hết danh sách).

### So sánh Mảng và Danh sách liên kết

| Tiêu chí | Mảng (Array) | Danh sách liên kết (Linked List) |
|---|---|---|
| Vị trí trong bộ nhớ | Liên tục | Rời rạc, liên kết bằng con trỏ |
| Kích thước | Cố định (mảng tĩnh) hoặc phải cấp phát lại khi đầy | Linh hoạt, mở rộng động theo từng node |
| Truy xuất phần tử thứ k | O(1) — tính trực tiếp theo địa chỉ | O(n) — phải duyệt từ đầu qua từng node |
| Thêm/xóa ở đầu danh sách | O(n) — phải dịch chuyển toàn bộ phần tử | O(1) — chỉ cần cập nhật con trỏ |
| Thêm/xóa ở giữa (đã biết vị trí node) | O(n) — phải dịch chuyển phần tử phía sau | O(1) — chỉ cập nhật con trỏ, không dịch chuyển |
| Bộ nhớ phụ | Không cần | Cần thêm bộ nhớ lưu con trỏ ở mỗi node |
| Duyệt tuần tự | Nhanh, tận dụng cache tốt (dữ liệu liên tục) | Chậm hơn do dữ liệu rời rạc trong bộ nhớ |

### Khi nào nên dùng danh sách liên kết?

- Khi số lượng phần tử **thay đổi thường xuyên** (thêm/xóa liên tục), đặc biệt ở đầu hoặc giữa danh sách.
- Khi **không cần truy xuất ngẫu nhiên** theo chỉ số, chỉ cần duyệt tuần tự.
- Khi kích thước dữ liệu **không xác định trước**, tránh lãng phí bộ nhớ do cấp phát dư thừa như mảng tĩnh.

Ngược lại, nếu cần truy xuất nhanh theo chỉ số (ví dụ [tìm kiếm nhị phân](../14-binary-search/)) hoặc dữ liệu ổn định về kích thước, mảng vẫn là lựa chọn hiệu quả hơn.

## Ví dụ

```
Mảng:              [10][20][30][40]   (liên tục trong bộ nhớ, truy xuất A[2] tức thời)

Danh sách liên kết: [10|•]->[20|•]->[30|•]->[40|NULL]
                     ^head
(các node có thể nằm rải rác trong bộ nhớ, muốn lấy giá trị thứ 3
 phải đi qua node 1, node 2 rồi mới tới node 3)
```
