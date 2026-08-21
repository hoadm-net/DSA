# Vai trò của cấu trúc dữ liệu

## Khái niệm

Cấu trúc dữ liệu (CTDL) là cách tổ chức, lưu trữ dữ liệu trong bộ nhớ máy tính sao cho có thể sử dụng dữ liệu đó một cách hiệu quả. Cùng một tập dữ liệu, nhưng tổ chức theo CTDL khác nhau sẽ dẫn đến hiệu năng xử lý (thêm, xóa, tìm kiếm, sắp xếp...) rất khác nhau.

## Giải thích chi tiết

Một chương trình về bản chất gồm hai thành phần không tách rời:

```
Chương trình = Cấu trúc dữ liệu + Giải thuật
```

CTDL đóng vai trò là "nền móng" mà giải thuật vận hành trên đó. Vai trò cụ thể của CTDL trong một hệ thống phần mềm:

- **Tổ chức dữ liệu hợp lý**: quyết định dữ liệu được lưu liên tục (mảng) hay rời rạc có liên kết (danh sách liên kết, cây...), ảnh hưởng trực tiếp đến cách truy xuất.
- **Quyết định hiệu năng của giải thuật**: cùng một bài toán tìm kiếm, nếu dữ liệu lưu trong mảng chưa sắp xếp thì phải duyệt tuần tự O(n); nếu lưu trong cây tìm kiếm nhị phân cân bằng thì chỉ mất O(log n).
- **Quản lý tài nguyên bộ nhớ**: một số CTDL cấp phát tĩnh (mảng), một số cấp phát động (danh sách liên kết, cây), ảnh hưởng đến việc sử dụng và giải phóng bộ nhớ khi chương trình chạy.
- **Là nền tảng để xây dựng các hệ thống phức tạp hơn**: cơ sở dữ liệu, hệ điều hành, trình biên dịch, mạng máy tính... đều dựa trên các CTDL nền tảng như mảng, danh sách liên kết, cây, bảng băm, đồ thị.
- **Ảnh hưởng đến khả năng bảo trì và mở rộng phần mềm**: chọn đúng CTDL giúp code rõ ràng, dễ mở rộng khi yêu cầu bài toán thay đổi.

Ví dụ minh họa vai trò của CTDL: một danh bạ điện thoại với hàng triệu số điện thoại.
- Nếu lưu bằng mảng không sắp xếp → tìm một số điện thoại phải duyệt qua trung bình một nửa danh sách.
- Nếu lưu bằng cây tìm kiếm nhị phân cân bằng (hoặc bảng băm) → tìm gần như tức thời.

Việc chọn CTDL phù hợp không làm thay đổi *kết quả* bài toán, nhưng làm thay đổi *chi phí* (thời gian, bộ nhớ) để đạt được kết quả đó — đây chính là lý do CTDL là một trong hai trụ cột (cùng với giải thuật) của khoa học máy tính.

## Ví dụ

```
Bài toán: Quản lý danh sách sinh viên, thường xuyên cần thêm sinh viên mới
và tra cứu theo mã số sinh viên.

Phương án 1 — Mảng không sắp xếp:
  Thêm sinh viên: O(1)
  Tra cứu theo mã số: O(n)

Phương án 2 — Cây tìm kiếm nhị phân cân bằng theo mã số:
  Thêm sinh viên: O(log n)
  Tra cứu theo mã số: O(log n)

=> Với hệ thống có rất nhiều lượt tra cứu, phương án 2 (chọn CTDL phù hợp)
   hiệu quả hơn hẳn dù việc thêm mới chậm hơn một chút.
```
