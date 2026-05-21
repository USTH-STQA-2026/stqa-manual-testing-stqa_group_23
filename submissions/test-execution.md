# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | STQA_Group_23 |
| **Ngày thực thi** |20/05/2026|
| **Trình duyệt** |Zen-browser|
| **Hệ điều hành** |Linux|

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|----------------|----------------------------|-----------------|----------|------------|-----|
| TC-01 | Login | Redirects to home, shows "Nguyễn Thủ Thư" | As expected | Pass | [TC01](image.png) | - |
| TC-02 | Login | Redirects to home, shows "Nguyễn Học Bá" | As expected | Pass | [TC02](image-1.png) | - |
| TC-03 | Login | Displays error: "Mật khẩu không đúng" | As expected | Pass | [TC03](image-2.png) | - |
| TC-04 | Login | Displays error: "Không tìm thấy thành viên" | As expected | Pass | [TC04](image-3.png) | - |
| TC-05 | Login | Displays error for empty fields | As expected | Pass | [TC05](image-4.png) | - |
| TC-06 | Book listing | Displays 20 books with correct initial statuses | As expected | Pass | [TC06](image-5.png) | - |
| TC-07 | Book search | Displays BOOK001 for keyword "flutter" | As expected | Pass | [TC07](image-6.png) | - |
| TC-08 | Book search | Displays BOOK001 & BOOK009 for author search | As expected | Pass | [TC08](image-7.png) | - |
| TC-09 | Book search | Empty list, displays "Không tìm thấy sách" | As expected | Pass | [TC09](image-8.png) | - |
| TC-10 | Book filter | Displays only BOOK006 and BOOK016 | As expected | Pass | [TC10](image-9.png) | - |
| TC-11 | Borrow book | Borrow successful, books count = 2 | As expected | Pass | [TC11](image-10.png) | - |
| TC-12 | Borrow book | Borrowing is not allowed (button hidden/error) | As expected | Pass | [TC12](image-11.png) | - |
| TC-13 | Borrow book | Request denied, shows "Tạm ngưng" error | As expected | Pass | [TC13](image-12.png) | - |
| TC-14 | Borrow book | Request denied, shows "Hết hạn" error | As expected | Pass | [TC14](image-16.png) | - |
| TC-15 | Borrow book | Request denied, shows 3-book limit error | As expected | Pass | [TC15](image-14.png) | - |
| TC-16 | Return book | Return successful, status reverts to "Có sẵn" | As expected | Pass | [TC16](image-17.png) | - |
| TC-17 | Return book | Return successful BUT an overdue warning is displayed | Return successful, but NO warning is displayed on screen | Fail | [TC17](image-18.png) | BUG-01 |
| TC-18 | Overdue handling | Record BR001 status changes to "Quá hạn" | Show 0 outcome | Fail | [TC18](image-19.png) | BUG-02 |
| TC-19 | Member management | Fail added | Show domain invalid | Fail | [TC19](image-20.png) | BUG-03 |
| TC-20 | Member management | Creation blocked, shows duplicate email error | As expected | Pass | [TC20](image-21.png) | - |
| TC-21 | Member management | Shows invalid email format error | Unexpected | Fail | [TC21](image-22.png) | BUG-04 |
| TC-22 | Member management | Shows invalid phone format error | As expected | Pass | [TC22](image-23.png) | - |
| TC-23 | Record lookup | Displays only own records (BR001 & BR004) | As expected | Pass | [TC23](image-24.png) | - |
| TC-24 | Record lookup | Access denied / returns an empty list | Display 0 information | Pass | [TC24](image-25.png)| - |
| TC-25 | Record lookup | Displays all 5 initial borrow records | As expected | Pass | [TC25](image-26.png) | - |

---

## Tổng hợp kết quả

|      Chỉ số       | Giá trị |
|-------------------|---------|
| Tổng số test case |    25   |
|        Pass       |    21   |
|        Fail       |    4    |
|        Blocked    |    0    |
|        Not Run    |    0    |
|   **Tỷ lệ Pass**  | **84%** |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| Login | 5 | 5 | 0 | 100% |
| Book listing | 1 | 1 | 0 | 100% |
| Book search | 3 | 3 | 0 | 100% |
| Book filter | 1 | 1 | 0 | 100% |
| Borrow book | 5 | 5 | 0 | 100% |
| Return book | 2 | 1 | 1 | 50% |
| Overdue handling | 1 | 0 | 1 | 0% |
| Member management | 4 | 2 | 2 | 50% |
| Record lookup | 3 | 3 | 0 | 100% |

```
