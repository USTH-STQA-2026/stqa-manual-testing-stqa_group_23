# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | STQA_Group_23 |
| **Ngày tạo** | 20/05/2026|
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Email có tồn tại trong DB? | Có | `librarian@library.com` | Đăng nhập thành công |
| | Không | `noone@email.com` | Thông báo lỗi |
| Mật khẩu có đúng? | Đúng | `admin123` | Đăng nhập thành công |
| | Sai | `wrongpass` | Thông báo lỗi |
| Ô nhập có rỗng? | Không rỗng | (giá trị bất kỳ) | Xử lý bình thường |
| | Rỗng | `""` | Thông báo "Vui lòng nhập..." |

### IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

### IDM — Mượn sách (REQ-04, REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái sách? | Có sẵn | BOOK001 | Cho phép mượn |
| | Đang mượn | BOOK003 | Không cho phép |
| | Thất lạc | BOOK007 | Không cho phép |
| Trạng thái thành viên? | Hoạt động | MEM002 | Cho phép mượn |
| | Tạm ngưng | MEM004 | Từ chối, thông báo lỗi |
| | Hết hạn | MEM005 | Từ chối, thông báo lỗi |
| Số sách đang mượn? | < 3 (BVA: 0, 1, 2) | MEM006 (0 sách) | Cho phép mượn |
| | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách | Từ chối, thông báo vượt giới hạn |

### IDM — `<!-- Nhóm tự bổ sung cho REQ-05 đến REQ-08 -->`

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| `<!-- Nhóm tự điền -->` | | | |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|----------------|----------------|-----------------|------------------|-----|----------|
| TC-01 | Successful login with Librarian account | At Login page | 1. Enter email.<br>2. Enter password.<br>3. Click Login. |Email: `librarian@library.com`<br>Pass: `admin123` | Redirects to the homepage. AppBar displays "Nguyễn Thủ Thư - Thủ thư". | REQ-01 | EP |
| TC-02 | Successful login with Member account | At Login page | 1. Enter email.<br>2. Enter password.<br>3. Click Login. | Email: `ba.nguyen@email.com`<br>Pass: `password123` | Redirects to the homepage. AppBar displays "Nguyễn Học Bá - Thành viên". | REQ-01 | EP |
| TC-03 | Login failed due to incorrect password | At Login page | 1. Enter email.<br>2. Enter incorrect password.<br>3. Click Login. | Email: `ba.nguyen@email.com`<br>Pass: `wrong_pass` | Displays error message: "Mật khẩu không đúng". | REQ-01 | EP |
| TC-04 | Login failed due to non-existent email | At Login page | 1. Enter incorrect email.<br>2. Enter password.<br>3. Click Login. | Email: `nobody@test.com`<br>Pass: `password123` | Displays error message: "Không tìm thấy thành viên". | REQ-01 | EP |
| TC-05 | Login failed due to empty fields | At Login page | 1. Leave email and password blank.<br>2. Click Login. | Email: `""`<br>Pass: `""` | Displays error message: "Vui lòng nhập email và mật khẩu". | REQ-01 | EP |
| TC-06 | View initial book list | Successfully logged in | 1. Navigate to "Sách" tab.<br>2. Check the displayed list. | None | Displays all 20 book titles. BOOK003 shows status "Đã mượn", BOOK001 shows "Có sẵn". | REQ-02 | EP |
| TC-07 | Search books by title | At "Sách" tab | 1. Enter keyword in the search bar.<br>2. Click Search. | Keyword: `flutter` | Displays BOOK001: "Lập trình Flutter cơ bản". | REQ-03 | EP |
| TC-08 | Search books by author | At "Sách" tab | 1. Enter author's name.<br>2. Click Search. | Keyword: `Nguyễn Minh Đức` | Displays 2 books: BOOK001 and BOOK009. | REQ-03 | EP |
| TC-09 | Search books with no results | At "Sách" tab | 1. Enter a random keyword.<br>2. Click Search. | Keyword: `abcdxyz123` | List is empty, displays message: "Không tìm thấy sách". | REQ-03 | EP |
| TC-10 | Filter books by category | At "Sách" tab | 1. Open category filter.<br>2. Select a category. | Category: `Kỹ năng mềm` | Displays only BOOK006 and BOOK016. | REQ-03 | EP |
| TC-11 | Successful book borrowing | Logged in as `biet.hoang@email.com` | 1. Find an "Available" book.<br>2. Click "Mượn". | Book: `BOOK001` | Borrow successful. Book status changes to "Đã mượn". Current borrowed books count = 2. | REQ-04 | Decision Table, BVA |
| TC-12 | Borrow failed | Logged in as `dam.tran@email.com` | 1. Find a book currently borrowed.<br>2. Attempt to click "Mượn". | Book: `BOOK003` | Borrowing is not allowed. | REQ-04 | Decision Table, EP |
| TC-13 | Borrow failed due to "Suspended" account status | Logged in as `cu.le@email.com` | 1. Select an "Available" book.<br>2. Click "Mượn". | Book: `BOOK004` | Borrow request denied, displays an error message regarding "Tạm ngưng" status. | REQ-04 | Decision Table, EP |
| TC-14 | Borrow failed due to "Expired" account status | Logged in as `binh.pham@email.com` | 1. Select an "Available" book.<br>2. Click "Mượn". | Book: `BOOK004` | Borrow request denied, displays an error message regarding "Hết hạn" status. | REQ-04 | Decision Table, EP |
| TC-15 | Borrow failed due to reaching the maximum limit | Logged in as `dam.tran@email.com`, successfully borrowed 3 books in a row | 1. Select a 4th book.<br>2. Click "Mượn". | 4th Book: `BOOK010` | Request denied. Displays an error message indicating the 3-book limit is exceeded. | REQ-04 | Decision Table, BVA |
| TC-16 | Successful book return | Logged in as `biet.hoang@email.com`, borrowing BR003 | 1. Go to "Mượn/Trả" tab.<br>2. Find the borrow record.<br>3. Click "Trả". | Record: `BR003` | Return successful, no warnings. BOOK013 status reverts to "Có sẵn". | REQ-05 | EP, BVA |
| TC-17 | Book return with an overdue warning | Logged in as `ba.nguyen@email.com`, borrowing BR001 | 1. Go to "Mượn/Trả" tab.<br>2. Find the record.<br>3. Click "Trả". | Record: `BR001` | Return successful BUT a clear overdue warning is displayed. | REQ-05 | EP, BVA |
| TC-18 | Librarian updates overdue books | Logged in as Librarian | 1. Click "Kiểm tra quá hạn".<br>2. Review the borrow records list. | "Kiểm tra quá hạn" button | Record BR001 status changes from "Đang mượn" to "Quá hạn". | REQ-06 | EP |
| TC-19 | Add new member | Logged in as Librarian, at "Thành viên" tab | 1. Click Add Member.<br>2. Fill in the form.<br>3. Save. | Name: `some`, Email: `some@email.com`, Phone: `0987654321` | Fail added | REQ-07 | EP, BVA |
| TC-20 | Add member failed: Duplicate email | Logged in as Librarian, at "Thành viên" tab | 1. Click Add Member.<br>2. Fill in the form.<br>3. Save. | Duplicate Email: `ba.nguyen@email.com` | Displays an error email invalid; creation is blocked. | REQ-07 | EP |
| TC-21 | Add new member : Valid email format | Logged in as Librarian, at "Thành viên" tab | 1. Fill in the information.<br>2. Save. | Email: `user@domain` | Displays success regarding invalid email format. | REQ-07 | EP |
| TC-22 | Add member failed: Invalid phone number format | Logged in as Librarian, at "Thành viên" tab | 1. Fill in the information.<br>2. Save. | Phone: `012345` | Displays an error regarding invalid phone format. | REQ-07 | BVA |
| TC-23 | Member can only view their own borrow records | Logged in as `ba.nguyen@email.com` | 1. Go to "Mượn/Trả" tab.<br>2. Check the records list. | Personal data | Displays only BR001 and BR004. DOES NOT display dam.tran's BR002 record. | REQ-08 | EP |
| TC-24 | Member cannot search for another member's record | Logged in as `ba.nguyen@email.com` | 1. Attempt to search for another user's record ID. | Search query: `BR002` or MEM003 ID | Access is denied / returns an empty list. | REQ-08 | EP |
| TC-25 | Librarian can view all borrow records | Logged in as Librarian | 1. Go to "Mượn/Trả" tab.<br>2. View the list. | None | Displays all 5 initial borrow records. | REQ-08 | EP |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
| Login | 5 | REQ-01 | EP |
| Book listing, searching, and filtering | 5 | REQ-02, REQ-03 | EP |
| Borrow book | 5 | REQ-04 | EP, BVA, Decision Table |
| Return & Overdue handling | 3 | REQ-05, REQ-06 | EP, BVA |
| Member management | 4 | REQ-07 | EP, BVA |
| Borrow record lookup | 3 | REQ-08 | EP |
| **Total** | **25** | **REQ-01 → REQ-08** | **EP, BVA, Decision Table** |
