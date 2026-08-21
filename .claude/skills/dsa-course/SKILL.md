---
name: dsa-course
description: Tiếp tục xây dựng bộ tài liệu giảng dạy môn Cấu trúc dữ liệu & Giải thuật (DSA) trong repo này — đọc checklist tiến độ, làm đúng 1 chủ đề tiếp theo rồi dừng lại chờ review. Dùng khi người dùng nói "làm tiếp DSA", "chủ đề tiếp theo", hoặc mở lại repo DSA để tiếp tục soạn nội dung.
---

# DSA Course Content Builder

Skill này lưu lộ trình và quy ước cho dự án soạn tài liệu môn Cấu trúc dữ liệu & Giải thuật (CTDL&GT), đặt tại repo `DSA`. Dự án gồm 49 folder nội dung, làm dần qua nhiều hội thoại — skill này là bộ nhớ bền vững giữa các hội thoại đó.

## Quy tắc cứng — đọc trước khi làm bất cứ điều gì

1. **Mỗi lần skill này được invoke, chỉ xử lý đúng 1 folder chủ đề** — là dòng đầu tiên trong checklist bên dưới còn đánh dấu `[ ]`.
2. Làm xong 1 folder (README.md, và demo.html nếu checklist ghi có demo) thì **dừng lại ngay**, tóm tắt ngắn gọn đã tạo gì, và **chờ người dùng review + xác nhận** trước khi đụng tới chủ đề kế tiếp.
3. Kể cả khi người dùng nói "làm luôn hết đi", "làm nhanh tất cả", vẫn phải nhắc lại quy tắc 1 chủ đề/lượt này và hỏi lại trước khi phá lệ — đây là yêu cầu tường minh của người dùng, không tự ý bỏ qua.
4. Sau khi hoàn thành 1 chủ đề và trước khi dừng, **cập nhật checklist bên dưới**: đổi `[ ]` → `[x]` cho dòng vừa làm.
5. Nếu người dùng xác nhận "ok, làm tiếp" ở lượt sau, đọc checklist để biết dòng `[ ]` tiếp theo là gì rồi lặp lại quy trình.
6. Không tự thêm/bớt/đổi thứ tự các folder trong danh sách này trừ khi người dùng yêu cầu — đây là lộ trình đã được người dùng chốt.

## Checklist tiến độ (49 chủ đề)

Cột "Demo" = có cần tạo `demo.html` tương tác hay không (chỉ nội dung cần trực quan hóa: thuật toán, thao tác trên cấu trúc dữ liệu).

### Buổi 1 — Tổng quan CTDL & kiểu dữ liệu
- [x] 01. `01-role-of-data-structures` — Vai trò của CTDL — Demo: không
- [x] 02. `02-relationship-data-structures-and-algorithms` — Mối quan hệ CTDL & giải thuật — Demo: không
- [x] 03. `03-evaluation-criteria-for-data-structures` — Tiêu chuẩn đánh giá CTDL — Demo: không
- [x] 04. `04-primitive-data-types` — Kiểu dữ liệu cơ bản — Demo: không
- [x] 05. `05-structured-data-types` — Kiểu dữ liệu có cấu trúc (mảng, struct) — Demo: không
- [x] 06. `06-abstract-data-types` — Trừu tượng hóa dữ liệu (ADT) — Demo: không

### Buổi 2 — Giải thuật, độ phức tạp, OOP C#
- [x] 07. `07-algorithm-concepts-and-representation` — Khái niệm giải thuật & cách mô tả — Demo: không
- [x] 08. `08-algorithm-characteristics` — Đặc trưng của giải thuật — Demo: không
- [x] 09. `09-algorithm-complexity-analysis` — Đánh giá độ phức tạp (Big-O) — Demo: có (biểu đồ so sánh tốc độ tăng)
- [x] 10. `10-oop-review-csharp` — Ôn tập OOP trên C# — Demo: không

### Buổi 3 — Tìm kiếm
- [x] 11. `11-need-for-search-and-sort` — Nhu cầu tìm kiếm & sắp xếp — Demo: không
- [x] 12. `12-search-problem-fundamentals` — Vấn đề tìm kiếm & tiêu chí đánh giá — Demo: không
- [x] 13. `13-linear-search` — Tìm kiếm tuần tự — Demo: có
- [x] 14. `14-binary-search` — Tìm kiếm nhị phân — Demo: có

### Buổi 4 — Sắp xếp cơ bản
- [x] 15. `15-sorting-problem-fundamentals` — Khái niệm bài toán sắp xếp — Demo: không
- [x] 16. `16-interchange-sort` — Đổi chỗ trực tiếp — Demo: có
- [x] 17. `17-bubble-sort` — Nổi bọt — Demo: có
- [x] 18. `18-selection-sort` — Chọn trực tiếp — Demo: có
- [x] 19. `19-insertion-sort` — Chèn trực tiếp — Demo: có

### Buổi 5 — Sắp xếp nâng cao
- [x] 20. `20-quick-sort` — Quick Sort — Demo: có
- [x] 21. `21-heap-sort` — Heap Sort — Demo: có
- [x] 22. `22-merge-sort` — Merge Sort — Demo: có

### Buổi 6 — Danh sách liên kết đơn
- [ ] 23. `23-linked-list-fundamentals` — Khái niệm DSLK & so sánh với mảng — Demo: không
- [ ] 24. `24-node-structure-and-list-types` — Cấu tạo Node & các loại DSLK — Demo: không
- [ ] 25. `25-singly-linked-list-init-and-traverse` — Khởi tạo và duyệt DSLK đơn — Demo: có
- [ ] 26. `26-insert-node-at-head-tail` — Thêm node vào đầu/cuối — Demo: có
- [ ] 27. `27-insert-node-by-position` — Chèn node theo vị trí/thứ tự — Demo: có
- [ ] 28. `28-delete-node` — Xóa node khỏi danh sách — Demo: có

### Buổi 7 — Sắp xếp trên DSLK, DSLK đôi/vòng
- [ ] 29. `29-sorting-a-linked-list` — Sắp xếp trên danh sách liên kết — Demo: có
- [ ] 30. `30-doubly-linked-list` — Danh sách liên kết đôi (giới thiệu) — Demo: có
- [ ] 31. `31-circular-linked-list` — Danh sách liên kết vòng (giới thiệu) — Demo: có

### Buổi 8 — Stack
- [ ] 32. `32-stack-fundamentals` — Khái niệm Stack (LIFO) — Demo: không
- [ ] 33. `33-stack-array-implementation` — Cài đặt Stack bằng mảng — Demo: có
- [ ] 34. `34-stack-linked-list-implementation` — Cài đặt Stack bằng DSLK — Demo: có
- [ ] 35. `35-stack-application-expression-evaluation` — Ứng dụng: Infix ↔ Postfix — Demo: có
- [ ] 36. `36-stack-application-recursion-removal` — Ứng dụng: khử đệ quy — Demo: có

### Buổi 9 — Queue
- [ ] 37. `37-queue-fundamentals` — Khái niệm Queue (FIFO) — Demo: không
- [ ] 38. `38-queue-array-implementation` — Cài đặt Queue bằng mảng (vòng) — Demo: có
- [ ] 39. `39-queue-linked-list-implementation` — Cài đặt Queue bằng DSLK — Demo: có
- [ ] 40. `40-queue-applications` — Ứng dụng Queue — Demo: có

### Buổi 10 — Cây tổng quát, cây nhị phân, BST
- [ ] 41. `41-general-tree-fundamentals` — Khái niệm cây tổng quát — Demo: không
- [ ] 42. `42-binary-tree-traversal` — Cây nhị phân: tính chất & duyệt (NLR/LNR/LRN) — Demo: có
- [ ] 43. `43-binary-search-tree` — BST: định nghĩa & thêm/tìm — Demo: có

### Buổi 11 — Xóa node BST, giới thiệu AVL
- [ ] 44. `44-bst-delete-node` — Xóa node khỏi BST (3 trường hợp) — Demo: có
- [ ] 45. `45-avl-tree-fundamentals` — Cây AVL: khái niệm & chỉ số cân bằng — Demo: không

### Buổi 12 — Phép quay & thêm/xóa AVL
- [ ] 46. `46-avl-rotations` — Các trường hợp mất cân bằng & phép quay (LL/LR/RR/RL) — Demo: có
- [ ] 47. `47-avl-insert-delete` — Thêm/xóa node trong cây AVL — Demo: có

### Mở rộng (ngoài 12 buổi chính thức)
- [ ] 48. `48-hash-table` — Bảng băm: hàm băm, xử lý đụng độ — Demo: có
- [ ] 49. `49-b-tree` — Cây nhiều nhánh (B-Tree): cấu trúc & xây dựng — Demo: có

## Template README.md cho mỗi folder

```markdown
# <Tên chủ đề>

## Khái niệm
<Định nghĩa ngắn gọn, dễ hiểu>

## Giải thích chi tiết
<Đặc điểm, cách hoạt động, so sánh nếu cần>

## Độ phức tạp
<Nếu áp dụng: best/average/worst case, Big-O>

## Ví dụ
<Pseudo-code hoặc code minh họa (C# nếu là nội dung OOP/cài đặt, ngược lại pseudo-code)>

## Demo
Xem file [demo.html](./demo.html) — mở trực tiếp bằng trình duyệt.
```
(Bỏ mục "Demo" nếu chủ đề không có demo.)

## Template demo.html

- File HTML đơn, tự chứa: vanilla HTML/CSS/JS, không dùng framework hay CDN ngoài, mở trực tiếp bằng trình duyệt (không cần build/server).
- Điều khiển tối thiểu: nút Run (tự động chạy), Step (chạy từng bước), Reset, và ô chỉnh tốc độ nếu có animation.
- Cho phép người học nhập dữ liệu đầu vào tùy ý (mảng số, chuỗi biểu thức...) khi hợp lý.
- Phong cách trực quan theo loại nội dung:
  - Sắp xếp/tìm kiếm trên mảng: thanh cột (bar chart) animate, highlight phần tử đang so sánh/hoán đổi.
  - Danh sách liên kết: vẽ node dạng hộp + mũi tên con trỏ, highlight node đang thao tác.
  - Stack/Queue: vẽ chồng/hàng phần tử, highlight thao tác push/pop hoặc enqueue/dequeue.
  - Cây (BST/AVL/B-Tree): vẽ cây bằng SVG hoặc canvas, highlight đường đi/node đang xét, hiện chỉ số cân bằng với AVL.
  - Hash Table: vẽ các bucket, highlight khi có đụng độ và cách xử lý.
- Giao diện tiếng Việt, đơn giản, không cần responsive phức tạp — ưu tiên rõ ràng dễ dạy trên lớp.

## Ghi chú khác

- Sau khi thêm folder mới, cập nhật link tương ứng trong `README.md` gốc (mục lục toàn khóa) nếu chưa có.
- Toàn bộ tên folder dùng tiếng Anh, kebab-case, số thứ tự 2 chữ số ở đầu.
