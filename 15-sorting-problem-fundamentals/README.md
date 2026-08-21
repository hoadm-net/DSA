# Khái niệm bài toán sắp xếp & tiêu chí đánh giá

## Khái niệm

Bài toán sắp xếp (sorting problem) là bài toán sắp xếp lại các phần tử trong một dãy dữ liệu theo một **thứ tự xác định** (tăng dần hoặc giảm dần) dựa trên giá trị của khóa sắp xếp.

## Giải thích chi tiết

### Phát biểu bài toán

Cho dãy `A[0..n-1]` gồm n phần tử, tìm một hoán vị của dãy sao cho `A[0] ≤ A[1] ≤ ... ≤ A[n-1]` (sắp xếp tăng dần) hoặc theo chiều ngược lại (giảm dần).

### Vì sao cần sắp xếp?

Như đã đề cập ở [Nhu cầu tìm kiếm & sắp xếp](../11-need-for-search-and-sort/), dữ liệu đã sắp xếp giúp tìm kiếm nhanh hơn ([tìm kiếm nhị phân](../14-binary-search/)), trình bày dễ đọc hơn, và là bước chuẩn bị cho nhiều giải thuật khác.

### Tiêu chí đánh giá một giải thuật sắp xếp

1. **Số phép so sánh và số phép hoán vị (swap)**: đây là hai loại thao tác cơ bản nhất mà hầu hết giải thuật sắp xếp thực hiện — độ phức tạp thời gian của giải thuật được tính dựa trên tổng số các thao tác này theo n (xem [Đánh giá độ phức tạp giải thuật](../09-algorithm-complexity-analysis/)).
2. **Bộ nhớ phụ sử dụng**: giải thuật sắp xếp **tại chỗ** (in-place, ví dụ Bubble Sort, Selection Sort, Insertion Sort, Quick Sort) chỉ cần O(1) bộ nhớ phụ; giải thuật **không tại chỗ** (ví dụ Merge Sort) cần thêm bộ nhớ phụ tỉ lệ với kích thước dữ liệu.
3. **Tính ổn định (stability)**: giải thuật ổn định giữ nguyên thứ tự tương đối giữa các phần tử có khóa bằng nhau; điều này quan trọng khi sắp xếp dữ liệu theo nhiều tiêu chí (ví dụ sắp theo điểm, các sinh viên cùng điểm giữ nguyên thứ tự alphabet đã sắp trước đó).
4. **Hiệu năng theo dữ liệu đầu vào**: một số giải thuật có độ phức tạp phụ thuộc mạnh vào thứ tự ban đầu của dữ liệu (best/average/worst case rất khác nhau — ví dụ Insertion Sort rất nhanh O(n) nếu dữ liệu gần như đã sắp xếp).
5. **Độ phức tạp cài đặt**: một số giải thuật đơn giản, dễ hiểu, dễ cài đặt đúng (Bubble, Selection, Insertion) — phù hợp dữ liệu nhỏ hoặc mục đích giảng dạy; một số phức tạp hơn nhưng hiệu quả hơn nhiều với dữ liệu lớn (Quick Sort, Heap Sort, Merge Sort).

### Phân loại giải thuật sắp xếp trong chương trình học

| Nhóm | Giải thuật | Độ phức tạp trung bình |
|---|---|---|
| Sắp xếp cơ bản (đơn giản, O(n²)) | [Đổi chỗ trực tiếp](../16-interchange-sort/), [Nổi bọt](../17-bubble-sort/), [Chọn trực tiếp](../18-selection-sort/), [Chèn trực tiếp](../19-insertion-sort/) | O(n²) |
| Sắp xếp nâng cao (hiệu quả, O(n log n)) | Quick Sort, Heap Sort, Merge Sort | O(n log n) |

Các giải thuật cơ bản dễ hiểu, thường được dạy trước để nắm vững nguyên lý so sánh — hoán vị, trước khi tiếp cận các giải thuật nâng cao dùng chiến lược "chia để trị" hoặc cấu trúc dữ liệu phụ trợ (heap) để đạt hiệu năng tốt hơn.

## Ví dụ

```
Đầu vào:  A = [5, 2, 9, 1, 5, 6]
Đầu ra (tăng dần): [1, 2, 5, 5, 6, 9]

Lưu ý tính ổn định: hai phần tử "5" giữ nguyên thứ tự tương đối
(phần tử 5 ở vị trí 0 vẫn đứng trước phần tử 5 ở vị trí 4) nếu
giải thuật sắp xếp là ổn định.
```
