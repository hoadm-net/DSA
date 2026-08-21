# Tiêu chuẩn đánh giá cấu trúc dữ liệu

## Khái niệm

Với cùng một bài toán, có thể có nhiều cách tổ chức dữ liệu khác nhau. Để chọn được CTDL phù hợp, cần dựa trên một bộ tiêu chuẩn đánh giá khách quan thay vì cảm tính.

## Giải thích chi tiết

Các tiêu chuẩn chính khi đánh giá một CTDL:

1. **Phản ánh đúng thực tế của bài toán**: CTDL phải mô tả được đầy đủ và chính xác các đối tượng dữ liệu cùng mối quan hệ giữa chúng trong bài toán thực tế (ví dụ: quan hệ cha-con trong cây, quan hệ trước-sau trong danh sách).

2. **Phù hợp với các thao tác trên dữ liệu**: CTDL phải hỗ trợ hiệu quả các thao tác mà bài toán cần thực hiện thường xuyên — thêm, xóa, tìm kiếm, sắp xếp, duyệt qua tất cả phần tử... Một CTDL "tốt" cho bài toán này có thể không tốt cho bài toán khác.

3. **Tiết kiệm không gian lưu trữ (space complexity)**: CTDL nên sử dụng bộ nhớ hợp lý — không lãng phí (ví dụ cấp phát mảng quá lớn so với nhu cầu thực) nhưng cũng không quá phức tạp khi không cần thiết.

4. **Thời gian xử lý hợp lý (time complexity)**: các thao tác trên CTDL cần có độ phức tạp thời gian chấp nhận được so với quy mô dữ liệu thực tế của hệ thống (xem thêm [Đánh giá độ phức tạp giải thuật](../09-algorithm-complexity-analysis/)).

Hai tiêu chuẩn 3 và 4 thường **đánh đổi lẫn nhau** (time-space tradeoff): CTDL dùng thêm bộ nhớ phụ (ví dụ bảng băm, cây chỉ mục) thường đổi lại tốc độ xử lý nhanh hơn CTDL tiết kiệm bộ nhớ nhưng xử lý chậm (mảng, danh sách liên kết đơn giản).

Ngoài ra còn có các tiêu chuẩn mang tính kỹ thuật phần mềm:

- **Tính đơn giản, dễ cài đặt**: CTDL càng đơn giản càng dễ code đúng, dễ bảo trì, ít lỗi.
- **Tính tổng quát/tái sử dụng**: CTDL có thể áp dụng cho nhiều kiểu dữ liệu khác nhau (thông qua kiểu tổng quát/generic) thay vì phải viết lại cho từng kiểu.

## Ví dụ

```
Bài toán: Lưu trữ danh sách 10 triệu giao dịch ngân hàng, cần:
  - Thêm giao dịch mới liên tục (rất thường xuyên)
  - Hiếm khi tra cứu giao dịch cũ theo mã số

So sánh 2 phương án theo tiêu chuẩn đánh giá:

  Mảng động (Array List):
    + Thêm vào cuối: O(1) trung bình — phù hợp thao tác chính
    + Bộ nhớ: liên tục, ít overhead
    - Tra cứu theo mã số: O(n) — nhưng ít khi cần nên chấp nhận được

  Cây tìm kiếm cân bằng theo mã số:
    + Tra cứu: O(log n) — nhanh nhưng không cần thiết vì ít tra cứu
    - Thêm: O(log n), chậm hơn mảng cho thao tác chính
    - Bộ nhớ: tốn thêm con trỏ, cấu trúc cây

=> Với đặc điểm bài toán này, mảng động đáp ứng tốt tiêu chuẩn
   "phù hợp với thao tác thường xuyên" hơn, dù về lý thuyết cây
   có độ phức tạp tra cứu tốt hơn.
```
