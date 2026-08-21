# Mối quan hệ giữa cấu trúc dữ liệu và giải thuật

## Khái niệm

Cấu trúc dữ liệu (CTDL) và giải thuật là hai thành phần không thể tách rời của một chương trình máy tính. Niklaus Wirth — cha đẻ ngôn ngữ Pascal — đã đúc kết mối quan hệ này bằng công thức nổi tiếng:

```
Chương trình = Cấu trúc dữ liệu + Giải thuật
```

## Giải thích chi tiết

CTDL trả lời câu hỏi **"dữ liệu được tổ chức như thế nào?"**, còn giải thuật trả lời câu hỏi **"xử lý dữ liệu đó bằng cách nào?"**. Hai thành phần này tác động qua lại lẫn nhau:

- **CTDL quyết định giải thuật nào khả thi/hiệu quả**: một giải thuật tìm kiếm nhị phân chỉ chạy đúng và nhanh (O(log n)) khi dữ liệu được tổ chức trong mảng đã sắp xếp; nếu dùng danh sách liên kết (không truy xuất ngẫu nhiên O(1)) thì tìm kiếm nhị phân mất lợi thế.
- **Giải thuật cần thực hiện quyết định cách chọn CTDL**: nếu bài toán đòi hỏi thêm/xóa phần tử liên tục ở giữa danh sách, danh sách liên kết (O(1) khi đã có vị trí) phù hợp hơn mảng (O(n) do phải dịch chuyển phần tử).
- **Cùng một bài toán, các cặp (CTDL, giải thuật) khác nhau cho ra chi phí khác nhau**: ví dụ bài toán quản lý hàng đợi ưu tiên có thể dùng mảng chưa sắp xếp + giải thuật tìm max mỗi lần O(n), hoặc dùng cây heap + giải thuật duy trì heap O(log n) mỗi lần.

Vì vậy khi thiết kế phần mềm, người lập trình không chọn CTDL và giải thuật riêng lẻ, mà phải **cân nhắc đồng thời cả hai** dựa trên:
1. Thao tác nào được thực hiện thường xuyên nhất (thêm, xóa, tìm kiếm, sắp xếp, duyệt...)?
2. Ràng buộc về bộ nhớ và thời gian của hệ thống?
3. Dữ liệu có thay đổi kích thước liên tục hay cố định?

## Ví dụ

```
Bài toán: Xây dựng từ điển tra cứu nghĩa của từ.

Lựa chọn A: CTDL = mảng chưa sắp xếp
            Giải thuật tra cứu = tìm kiếm tuần tự O(n)

Lựa chọn B: CTDL = mảng đã sắp xếp theo alphabet
            Giải thuật tra cứu = tìm kiếm nhị phân O(log n)

Lựa chọn C: CTDL = cây tìm kiếm nhị phân cân bằng (AVL)
            Giải thuật tra cứu, thêm, xóa đều O(log n)

=> Giải thuật tốt (nhị phân, AVL) chỉ phát huy được khi đi cùng
   CTDL phù hợp (đã sắp xếp, cây cân bằng). Chọn sai CTDL sẽ khiến
   giải thuật tốt cũng không thể áp dụng hoặc mất lợi thế.
```
