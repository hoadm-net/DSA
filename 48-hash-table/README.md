# Bảng băm (Hash Table): hàm băm, xử lý đụng độ

## Khái niệm

Bảng băm (hash table) là cấu trúc dữ liệu ánh xạ **khóa (key)** tới **vị trí lưu trữ** thông qua một **hàm băm (hash function)**, cho phép đạt tốc độ truy xuất/thêm/xóa trung bình **O(1)** — nhanh hơn cả [cây tìm kiếm cân bằng](../45-avl-tree-fundamentals/) (O(log n)), đánh đổi bằng việc không giữ được thứ tự dữ liệu.

## Giải thích chi tiết

### Hàm băm (Hash Function)

Hàm băm `h(key)` biến đổi một khóa (số, chuỗi...) thành một **chỉ số hợp lệ** trong mảng lưu trữ có kích thước `capacity`:

```
h(key) = f(key) mod capacity
```

Với khóa là số nguyên, cách đơn giản nhất là `h(key) = key mod capacity`. Với khóa là chuỗi, thường cộng dồn mã ASCII (hoặc dùng đa thức Horner) của các ký tự trước khi lấy dư.

**Tiêu chí của một hàm băm tốt**:
- **Tính toán nhanh** — O(1), vì hàm băm được gọi ở mọi thao tác.
- **Phân bố đều** — rải khóa đồng đều khắp bảng, giảm thiểu đụng độ.
- **Xác định** — cùng một khóa luôn cho ra cùng một chỉ số.

### Đụng độ (Collision)

Vì số lượng khóa có thể có thường lớn hơn nhiều `capacity`, hai khóa khác nhau có thể có cùng giá trị băm — gọi là **đụng độ**. Đây là điều **không thể tránh khỏi hoàn toàn** (theo nguyên lý chuồng bồ câu), nên bảng băm cần một chiến lược xử lý đụng độ.

### Xử lý đụng độ bằng Nối kết (Chaining / Separate Chaining)

Mỗi vị trí trong bảng không lưu trực tiếp 1 giá trị, mà lưu **một danh sách liên kết** (xem [Danh sách liên kết đơn](../23-linked-list-fundamentals/)) chứa tất cả các khóa cùng băm về vị trí đó:

```
Thêm(key): tính idx = h(key), thêm key vào đầu danh sách liên kết tại items[idx]
Tìm(key): tính idx = h(key), duyệt danh sách liên kết tại items[idx] để tìm key
Xóa(key): tính idx = h(key), xóa key khỏi danh sách liên kết tại items[idx]
```

**Ưu điểm**: đơn giản, không giới hạn số phần tử băm về cùng 1 vị trí (danh sách tự mở rộng).
**Nhược điểm**: nếu đụng độ nhiều (hàm băm kém hoặc bảng quá tải), các danh sách liên kết dài ra, thao tác tụt xuống gần O(n).

### Xử lý đụng độ bằng Địa chỉ mở (Open Addressing) — Dò tuyến tính (Linear Probing)

Không dùng danh sách liên kết phụ — khi vị trí `h(key)` đã bị chiếm, **dò tuần tự** sang các vị trí tiếp theo (`h(key)+1`, `h(key)+2`, ... theo `mod capacity`, quay vòng như [hàng đợi vòng](../38-queue-array-implementation/)) cho đến khi tìm được ô trống:

```
Thêm(key): idx = h(key)
           WHILE items[idx] đã có giá trị
               idx = (idx + 1) mod capacity
           items[idx] = key
```

**Ưu điểm**: không cần cấp phát thêm bộ nhớ cho danh sách liên kết, dữ liệu liên tục trong mảng (tận dụng cache tốt).
**Nhược điểm**: dễ xảy ra hiện tượng **tụ cụm (clustering)** — nhiều khóa dồn liên tiếp thành từng cụm dài, làm chậm dần các thao tác; và bảng có giới hạn kích thước cố định (không thể chứa nhiều hơn `capacity` phần tử).

### Hệ số tải (Load Factor)

```
LoadFactor = Số phần tử đang lưu / capacity
```

Hệ số tải càng cao, đụng độ càng nhiều, hiệu năng càng giảm. Quy tắc thường dùng: khi `LoadFactor` vượt một ngưỡng (ví dụ 0.7), tự động **cấp phát lại bảng lớn hơn** (thường gấp đôi) và băm lại toàn bộ dữ liệu cũ (rehashing) — tương tự cách mảng động tự mở rộng.

## Độ phức tạp

| Thao tác | Trung bình (hàm băm tốt, tải hợp lý) | Xấu nhất (đụng độ nhiều / hàm băm kém) |
|---|---|---|
| Thêm | O(1) | O(n) |
| Tìm kiếm | O(1) | O(n) |
| Xóa | O(1) | O(n) |

## Ví dụ

```
capacity = 7, h(key) = key mod 7
Thêm lần lượt: 10, 3, 17, 5

h(10) = 3   -> items[3] = [10]
h(3)  = 3   -> ĐỤNG ĐỘ với 10!
h(17) = 3   -> ĐỤNG ĐỘ với 10, 3!
h(5)  = 5   -> items[5] = [5]

Với Chaining:        items[3] = [10, 3, 17] (danh sách liên kết)
Với Linear Probing:  items[3]=10, items[4]=3 (dò +1), items[5] đã có 5
                      nên items[6]=17 (dò tiếp tới vị trí trống)
```

## Demo

Xem file [demo.html](./demo.html) — chọn cách xử lý đụng độ (Chaining hoặc Linear Probing), thêm giá trị và quan sát hàm băm tính chỉ số, cách đụng độ được xử lý trực quan trên các bucket.
