# Sắp xếp trên danh sách liên kết

## Khái niệm

Các giải thuật sắp xếp đã học ([Buổi 4](../15-sorting-problem-fundamentals/), [Buổi 5](../20-quick-sort/)) đều có thể áp dụng cho danh sách liên kết, nhưng vì danh sách liên kết **không hỗ trợ truy xuất ngẫu nhiên** theo chỉ số (xem [Khái niệm danh sách liên kết](../23-linked-list-fundamentals/)), việc cài đặt cần điều chỉnh lại cách tiếp cận so với sắp xếp trên mảng.

## Giải thích chi tiết

### Hai cách hoán đổi vị trí trên danh sách liên kết

Khi một giải thuật sắp xếp cần "đổi chỗ" hai phần tử, trên danh sách liên kết có hai cách thực hiện:

1. **Hoán đổi dữ liệu (swap Data)**: giữ nguyên các node và liên kết `Next`, chỉ đổi giá trị `Data` bên trong hai node cho nhau. Cách này **đơn giản**, gần như giống hệt thao tác trên mảng (vì duyệt tuần tự qua `Next` đóng vai trò tương tự chỉ số mảng) — nhưng làm mất "định danh" ban đầu của node (nếu node đại diện cho một đối tượng phức tạp cần giữ nguyên danh tính, cách này không phù hợp).
2. **Hoán đổi liên kết (relink Node)**: giữ nguyên dữ liệu bên trong mỗi node, mà thay đổi các con trỏ `Next` để *thực sự di chuyển* node tới vị trí mới trong chuỗi liên kết. Cách này phức tạp hơn (dễ làm đứt liên kết nếu thao tác sai thứ tự, xem [Chèn node](../27-insert-node-by-position/)) nhưng giữ nguyên danh tính của từng node.

Với các giải thuật sắp xếp cơ bản (Selection Sort, Insertion Sort, Bubble Sort/Interchange Sort), cách 1 (hoán đổi dữ liệu) được dùng phổ biến trong giảng dạy vì đơn giản, tư duy giống hệt sắp xếp mảng.

### Mức độ phù hợp của từng giải thuật với danh sách liên kết

| Giải thuật | Mức độ phù hợp | Ghi chú |
|---|---|---|
| Selection Sort, Insertion Sort, Bubble Sort | Phù hợp tốt | Chỉ cần duyệt tuần tự, không cần truy xuất ngẫu nhiên |
| Merge Sort | **Rất phù hợp** | Chia đôi danh sách bằng kỹ thuật con trỏ nhanh/chậm (fast/slow pointer) thay vì tính `mid` theo chỉ số; bước trộn chỉ cần nối lại con trỏ `Next`, không cần mảng phụ như khi sắp mảng |
| Quick Sort | Kém phù hợp hơn | Bước phân hoạch (partition) trong cài đặt chuẩn cần duyệt từ hai đầu hoặc truy xuất theo chỉ số — phức tạp hơn khi chỉ có con trỏ một chiều |
| Heap Sort | Không phù hợp | Cấu trúc heap dựa vào công thức chỉ số `2i+1`, `2i+2` — đòi hỏi truy xuất ngẫu nhiên O(1), điều danh sách liên kết không có |

## Độ phức tạp

Độ phức tạp thời gian của mỗi giải thuật khi áp dụng cho danh sách liên kết về cơ bản **giữ nguyên** so với khi áp dụng cho mảng (O(n²) cho các giải thuật cơ bản, O(n log n) cho Merge Sort) — chỉ khác ở hằng số chi phí duyệt (không có bộ nhớ đệm liên tục như mảng nên chậm hơn về mặt hằng số thực tế), và ở việc **không cần thêm bộ nhớ phụ O(n)** khi Merge Sort trên danh sách liên kết (nhờ trộn bằng cách nối lại con trỏ thay vì cần mảng phụ).

## Ví dụ

```
FUNCTION SelectionSortList(head)
    p = head
    WHILE p != NULL
        minNode = p
        q = p.Next
        WHILE q != NULL
            IF q.Data < minNode.Data THEN
                minNode = q
            END IF
            q = q.Next
        END WHILE
        Đổi chỗ p.Data và minNode.Data   // hoán đổi dữ liệu, không đổi liên kết
        p = p.Next
    END WHILE
END FUNCTION
```

## Demo

Xem file [demo.html](./demo.html) — khởi tạo danh sách, chạy từng bước Selection Sort trực tiếp trên chuỗi node-liên kết (đổi chỗ dữ liệu giữa các node), quan sát vùng đã sắp xếp mở rộng dần từ đầu danh sách.
