# Nhu cầu tìm kiếm & sắp xếp trong hệ thống thông tin

## Khái niệm

Tìm kiếm (search) và sắp xếp (sort) là hai thao tác xuất hiện ở hầu như mọi hệ thống thông tin — từ ứng dụng nhỏ đến hệ thống lớn — vì mục tiêu cuối cùng của việc lưu trữ dữ liệu luôn là để **truy xuất lại thông tin đó một cách nhanh chóng, chính xác** khi cần.

## Giải thích chi tiết

### Vì sao cần tìm kiếm?

Hầu hết ứng dụng đều cần tra cứu dữ liệu theo một tiêu chí nào đó: tìm sinh viên theo mã số, tìm sản phẩm theo tên, tìm giao dịch theo mã hóa đơn... Khi dữ liệu càng lớn (hàng nghìn, hàng triệu bản ghi), thời gian tìm kiếm càng trở thành yếu tố quyết định trải nghiệm người dùng và hiệu năng hệ thống.

### Vì sao cần sắp xếp?

Sắp xếp thường không phải là mục tiêu cuối cùng, mà là **bước chuẩn bị** để phục vụ mục tiêu khác:

- **Tăng tốc độ tìm kiếm**: dữ liệu đã sắp xếp cho phép dùng [tìm kiếm nhị phân](../14-binary-search/) (O(log n)) thay vì [tìm kiếm tuần tự](../13-linear-search/) (O(n)).
- **Trình bày dữ liệu dễ đọc hơn**: danh sách sản phẩm theo giá tăng dần, danh sách sinh viên theo điểm giảm dần...
- **Là bước trung gian cho các giải thuật khác**: nhiều bài toán (tìm phần tử trùng lặp, tìm khoảng cách gần nhất, gộp hai danh sách...) trở nên đơn giản hơn nhiều nếu dữ liệu đã được sắp xếp trước.

### Mối quan hệ giữa tìm kiếm và sắp xếp

Đây là một sự **đánh đổi (tradeoff)** kinh điển trong CTDL&GT: bỏ chi phí sắp xếp một lần (O(n log n) với các giải thuật hiệu quả) để đổi lấy chi phí tìm kiếm rẻ hơn rất nhiều ở mỗi lần tra cứu sau đó (O(log n) thay vì O(n)). Quyết định "có nên sắp xếp trước hay không" phụ thuộc vào:

1. Dữ liệu có được tìm kiếm nhiều lần hay chỉ một lần?
2. Dữ liệu có thay đổi (thêm/xóa) thường xuyên hay ổn định?
3. Chi phí sắp xếp lại mỗi khi dữ liệu thay đổi có chấp nhận được không?

## Ví dụ

```
Hệ thống tra cứu điểm thi của 50,000 thí sinh, được tra cứu hàng triệu
lượt bởi thí sinh và phụ huynh trong 1 tuần công bố điểm.

Phương án 1 — Không sắp xếp, tìm tuần tự mỗi lần tra cứu:
  Mỗi lượt tra cứu: trung bình 25,000 phép so sánh (O(n))
  Với hàng triệu lượt tra cứu -> cực kỳ tốn tài nguyên

Phương án 2 — Sắp xếp 1 lần theo số báo danh, sau đó tìm nhị phân:
  Sắp xếp ban đầu: ~50,000 x log(50,000) ≈ 800,000 phép so sánh (1 lần)
  Mỗi lượt tra cứu sau đó: chỉ ~16 phép so sánh (O(log n))

=> Vì dữ liệu điểm thi ổn định (không đổi trong tuần công bố) và được
   tra cứu rất nhiều lần, sắp xếp trước là lựa chọn rõ ràng hiệu quả hơn.
```
