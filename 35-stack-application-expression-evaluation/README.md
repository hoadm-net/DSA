# Ứng dụng Stack: tính giá trị biểu thức (Infix ↔ Postfix)

## Khái niệm

Một trong những ứng dụng kinh điển nhất của Stack là xử lý biểu thức toán học: **chuyển đổi biểu thức trung tố (Infix) sang hậu tố (Postfix)**, và **tính giá trị biểu thức hậu tố** — cả hai đều dựa hoàn toàn vào nguyên tắc LIFO của Stack.

## Giải thích chi tiết

### Ba dạng biểu thức

| Dạng | Ví dụ | Đặc điểm |
|---|---|---|
| Infix (trung tố) | `3 + 4 * 2` | Toán tử nằm **giữa** hai toán hạng — cách viết quen thuộc với con người, nhưng cần quy tắc ưu tiên và dấu ngoặc để không mập mờ |
| Postfix (hậu tố) | `3 4 2 * +` | Toán tử nằm **sau** các toán hạng — không cần dấu ngoặc, không mập mờ, **máy tính xử lý trực tiếp bằng Stack rất hiệu quả** |
| Prefix (tiền tố) | `+ 3 * 4 2` | Toán tử nằm **trước** các toán hạng — ít dùng hơn trong giảng dạy nhập môn |

### Vì sao cần chuyển sang Postfix?

Với biểu thức Infix, máy tính phải liên tục xử lý độ ưu tiên toán tử (`*`, `/` trước `+`, `-`) và dấu ngoặc — phức tạp khi tính trực tiếp. Biểu thức Postfix loại bỏ hoàn toàn nhu cầu này: **chỉ cần duyệt từ trái sang phải một lần, dùng một Stack**, không cần biết quy tắc ưu tiên hay dấu ngoặc nữa (vì thứ tự đã được "mã hóa" sẵn trong cách sắp xếp token).

### Thuật toán chuyển Infix → Postfix (dùng Stack toán tử)

Duyệt từng token của biểu thức Infix:
1. Nếu token là **toán hạng** (số): đưa thẳng vào chuỗi kết quả Postfix.
2. Nếu token là `(`: đẩy vào Stack toán tử.
3. Nếu token là `)`: lần lượt lấy toán tử ra khỏi Stack đưa vào Postfix cho đến khi gặp `(` (rồi bỏ luôn dấu `(` đó, không đưa vào Postfix).
4. Nếu token là **toán tử**: trong khi đỉnh Stack là toán tử có độ ưu tiên **lớn hơn hoặc bằng** toán tử hiện tại, lấy nó ra đưa vào Postfix; sau đó đẩy toán tử hiện tại vào Stack.
5. Sau khi duyệt hết: lấy nốt toàn bộ toán tử còn lại trong Stack đưa vào Postfix.

### Thuật toán tính giá trị biểu thức Postfix (dùng Stack toán hạng)

Duyệt từng token của biểu thức Postfix:
1. Nếu token là **toán hạng**: đẩy vào Stack.
2. Nếu token là **toán tử**: lấy ra **2 toán hạng** ở đỉnh Stack (`b` lấy trước, `a` lấy sau — vì LIFO), tính `a toán_tử b`, rồi đẩy kết quả trở lại Stack.

Sau khi duyệt hết token, giá trị còn lại duy nhất trong Stack chính là **kết quả của biểu thức**.

## Độ phức tạp

| Giai đoạn | Big-O (với n token) |
|---|---|
| Chuyển Infix → Postfix | O(n) — mỗi token được đẩy/lấy khỏi Stack tối đa 1 lần |
| Tính giá trị Postfix | O(n) |

## Ví dụ

```
Infix:    3 + 4 * 2 - ( 1 + 5 )
Postfix:  3 4 2 * + 1 5 + -

Tính Postfix:
  Đọc 3        → Stack: [3]
  Đọc 4        → Stack: [3, 4]
  Đọc 2        → Stack: [3, 4, 2]
  Đọc *        → lấy 4, 2 ra, tính 4*2=8   → Stack: [3, 8]
  Đọc +        → lấy 3, 8 ra, tính 3+8=11  → Stack: [11]
  Đọc 1        → Stack: [11, 1]
  Đọc 5        → Stack: [11, 1, 5]
  Đọc +        → lấy 1, 5 ra, tính 1+5=6   → Stack: [11, 6]
  Đọc -        → lấy 11, 6 ra, tính 11-6=5 → Stack: [5]

Kết quả: 5
```

## Demo

Xem file [demo.html](./demo.html) — nhập biểu thức Infix (các token cách nhau bởi khoảng trắng), chạy từng bước để xem quá trình chuyển sang Postfix bằng Stack toán tử, sau đó tính giá trị Postfix bằng Stack toán hạng.
