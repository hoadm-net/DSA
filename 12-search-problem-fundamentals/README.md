# Vấn đề tìm kiếm & tiêu chí đánh giá

## Khái niệm

Bài toán tìm kiếm (searching problem) là bài toán xác định xem một giá trị cho trước (gọi là **khóa tìm kiếm**) có xuất hiện trong một tập hợp dữ liệu hay không, và nếu có thì xác định vị trí (hoặc lấy ra) bản ghi tương ứng.

## Giải thích chi tiết

### Khóa và mẫu tin

- **Mẫu tin (record)**: đơn vị dữ liệu đầy đủ, có thể gồm nhiều trường thông tin — ví dụ một mẫu tin sinh viên gồm mã số, họ tên, ngày sinh, điểm...
- **Khóa (key)**: một hoặc một tổ hợp trường trong mẫu tin, được dùng làm **tiêu chí để nhận diện và tìm kiếm** mẫu tin đó. Khóa cần có tính chất phân biệt (thường là duy nhất) để việc tìm kiếm cho ra kết quả chính xác — ví dụ mã số sinh viên là khóa tốt hơn họ tên (vì có thể trùng tên).

Phát biểu tổng quát của bài toán tìm kiếm: *cho một tập hợp mẫu tin và một giá trị khóa x, tìm mẫu tin có khóa bằng x (nếu tồn tại)*.

### Kết quả của bài toán tìm kiếm

- **Tìm thấy**: trả về vị trí (chỉ số, con trỏ...) hoặc chính mẫu tin có khóa khớp.
- **Không tìm thấy**: trả về một giá trị/tín hiệu đặc biệt (ví dụ -1, null) báo hiệu khóa không tồn tại trong tập dữ liệu.

### Tiêu chí đánh giá một giải thuật tìm kiếm

1. **Số lần so sánh** (chi phí thời gian): trung bình và trong trường hợp xấu nhất cần bao nhiêu lần so sánh khóa để tìm ra (hoặc kết luận không có) kết quả — đây là tiêu chí quan trọng nhất, biểu diễn bằng [Big-O](../09-algorithm-complexity-analysis/).
2. **Yêu cầu về cấu trúc dữ liệu đầu vào**: giải thuật có đòi hỏi dữ liệu phải được sắp xếp trước hay không ([tìm kiếm nhị phân](../14-binary-search/) đòi hỏi dữ liệu đã sắp xếp, còn [tìm kiếm tuần tự](../13-linear-search/) thì không).
3. **Bộ nhớ phụ sử dụng**: giải thuật có cần thêm cấu trúc dữ liệu phụ trợ (ví dụ bảng băm, cây chỉ mục) để tăng tốc hay không.
4. **Tính ổn định khi dữ liệu thay đổi**: nếu dữ liệu thường xuyên được thêm/xóa, giải thuật/CTDL đi kèm có duy trì được hiệu năng tìm kiếm tốt hay phải tổ chức lại (ví dụ sắp xếp lại) sau mỗi thay đổi.

Hai giải thuật tìm kiếm cơ bản nhất, minh họa rõ sự đánh đổi giữa các tiêu chí trên, là [Tìm kiếm tuần tự](../13-linear-search/) và [Tìm kiếm nhị phân](../14-binary-search/).

## Ví dụ

```
Tập dữ liệu: mảng điểm thi đã sắp xếp tăng dần
    [3, 5, 7, 12, 18, 25, 31, 40]

Bài toán: Tìm xem điểm số 25 có trong danh sách không, ở vị trí nào?

Khóa tìm kiếm: giá trị điểm thi (x = 25)
Mẫu tin: mỗi phần tử trong mảng (ở đây mẫu tin đơn giản chỉ gồm điểm số)

Kết quả mong đợi: "Tìm thấy tại vị trí 5 (chỉ số bắt đầu từ 0)"
```
