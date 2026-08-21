# Đặc trưng của giải thuật

## Khái niệm

Không phải mọi dãy các bước xử lý đều là một giải thuật hợp lệ. Để được coi là một giải thuật đúng nghĩa, dãy các bước đó phải thỏa mãn đồng thời 5 đặc trưng sau.

## Giải thích chi tiết

### 1. Tính đúng đắn (Correctness)

Giải thuật phải cho ra **kết quả đúng** với mọi trường hợp đầu vào hợp lệ (bao gồm cả các trường hợp biên/đặc biệt), không chỉ đúng với một vài ví dụ thử nghiệm.

### 2. Tính dừng (Finiteness)

Giải thuật phải **kết thúc sau một số hữu hạn bước**, với mọi bộ dữ liệu đầu vào hợp lệ. Một chương trình lặp vô hạn (ví dụ vòng lặp thiếu điều kiện dừng đúng) không phải là một giải thuật.

### 3. Tính xác định (Determinism)

Mỗi bước của giải thuật phải được mô tả **rõ ràng, không mập mờ** — tại mỗi thời điểm, chỉ có duy nhất một thao tác tiếp theo được xác định (không phụ thuộc vào diễn giải chủ quan của người thực hiện).

### 4. Tính hiệu quả (Effectiveness)

Mỗi bước trong giải thuật phải **đủ đơn giản để có thể thực hiện được** trong thời gian hữu hạn bằng các công cụ/phép toán cơ bản sẵn có (không yêu cầu những thao tác không thể thực hiện, ví dụ "đoán một số bất kỳ chính xác tuyệt đối"). Ngoài ra, "hiệu quả" còn được hiểu theo nghĩa giải thuật nên tối ưu về thời gian và bộ nhớ sử dụng (xem [Đánh giá độ phức tạp giải thuật](../09-algorithm-complexity-analysis/)).

### 5. Tính phổ quát (Generality)

Giải thuật nên áp dụng được cho **một lớp bài toán** (với các bộ dữ liệu đầu vào khác nhau trong phạm vi bài toán), không chỉ giải quyết một trường hợp cụ thể, đơn lẻ.

## Ví dụ

```
Bài toán: Tìm ước chung lớn nhất (UCLN) của 2 số nguyên dương a, b.

Giải thuật Euclid (thỏa cả 5 đặc trưng):
    FUNCTION UCLN(a, b)
        WHILE b != 0
            r = a MOD b
            a = b
            b = r
        END WHILE
        RETURN a
    END FUNCTION

- Đúng đắn: luôn trả về đúng UCLN với mọi a, b nguyên dương.
- Dừng: b giảm dần và luôn đạt 0 sau hữu hạn bước (chứng minh được).
- Xác định: mỗi bước (MOD, gán) đều rõ ràng, không mập mờ.
- Hiệu quả: phép chia lấy dư là thao tác cơ bản, thực hiện được ngay.
- Phổ quát: áp dụng cho MỌI cặp số nguyên dương, không chỉ 1 cặp cụ thể.

Phản ví dụ (KHÔNG phải giải thuật hợp lệ):
    WHILE a != b
        Đoán xem a hay b lớn hơn
        Trừ số lớn hơn cho số nhỏ hơn
    -> Vi phạm tính xác định ("đoán" không rõ ràng) và có thể vi phạm
       tính dừng nếu a, b không nguyên (không chắc đạt điều kiện dừng).
```
