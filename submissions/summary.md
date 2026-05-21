# Test Summary — Báo cáo tổng hợp kiểm thử

> **Hướng dẫn**: Đây là hoạt động **Quality Assurance** — bạn đánh giá chất lượng tổng thể của phần mềm, không chỉ liệt kê lỗi.

---

## 1. Thông tin nhóm

| Mục | Thông tin |
|-----|----------|
| **Nhóm** | STQA_Group_23 |
| **Lớp** |ICT2.012|
| **Ngày báo cáo** |20/05/2026|
| **Hệ thống kiểm thử** | https://stqa.rbc.vn — v1.0 |

---

## 2. Tổng quan kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | 25 |
| Pass | 21 |
| Fail | 4 |
| Blocked | 0 |
| Not Run | 0 |
| **Tỷ lệ Pass** | 84% |
| **Số bug phát hiện** | 4 |

### Phân bổ theo nhóm chức năng

| Nhóm chức năng | TC | Pass | Fail | Bug | Đánh giá |
|----------------|----|------|------|-----|----------|
| Đăng nhập (Login) | 5 | 5 | 0 | 0 | Hoạt động rất ổn định, phân quyền chính xác giữa các tài khoản |
| Danh sách sách (Book listing) | 1 | 1 | 0 | 0 | Hiển thị đầy đủ số lượng và trạng thái ban đầu chính xác |
| Tìm kiếm & Lọc sách (Search & Filter) |----|------|------|-----| Tìm kiếm theo tên/tác giả tốt, bộ lọc danh mục hoạt động đúng |
| Mượn sách (Borrow book) | 4 | 4 | 0 | 0 | Kiểm tra tốt các ràng buộc về số lượng sách, trạng thái tài khoản |
| Trả sách (Return book) | 5 | 5 | 0 | 0 | Trả sách thành công nhưng không cảnh báo khi thành viên trả muộn |
| Xử lý quá hạn (Overdue handling) | 2 | 1 | 1 | 1 | Lỗi nghiêm trọng: Nút quét kiểm tra quá hạn không hoạt động |
| Quản lý thành viên (Member management) | 1 | 0 | 1 | 1 | Lỗi logic: Validate Email bị ngược (cho qua email sai, chặn email đúng) |
| Tra cứu lịch sử mượn (Record lookup) | 3 | 3 | 0 | 0 | Bảo mật tốt, thành viên không xem được bản ghi của người khác |



### Phân bổ bug theo mức độ

| Mức độ | Số lượng | Bug IDs |
|--------|---------|---------|
| High | 1 | BUG-02 |
| Medium | 3 | BUG-01, BUG-03, BUG-04 |
| Low | 0 | |

---

## 3. Kỹ thuật thiết kế đã sử dụng

| Kỹ thuật | Áp dụng cho REQ nào? | Số TC sử dụng | Giải thích cách áp dụng |
|----------|---------------------|---------------|------------------------|
| Phân lớp tương đương (EP) | REQ-01, REQ-02, REQ-03, REQ-04, REQ-05, REQ-06, REQ-07, REQ-08 | 25 | Chia các miền đầu vào (như định dạng email, loại tài khoản, từ khóa tìm kiếm) thành các phân vùng hợp lệ và không hợp lệ để giảm thiểu số lượng test case cần chạy. |
| Phân tích giá trị biên (BVA) | REQ-04, REQ-05, REQ-07 | 6 | Áp dụng để kiểm tra các ngưỡng số lượng sách mượn (ngưỡng giới hạn 3 cuốn ở TC-15) và độ dài/định dạng số điện thoại khi thêm thành viên. |
| Bảng quyết định (Decision Table) | REQ-04 | 5 | Kết hợp các điều kiện trạng thái sách (Có sẵn/Đã mượn) và trạng thái thành viên (Hoạt động/Tạm ngưng/Hết hạn) để xác định quyền mượn sách. |

---

## 4. Phân tích chất lượng phần mềm

### 4.1. Điểm mạnh
 - Tính năng cốt lõi ổn định: Các chức năng Đăng nhập (REQ-01), Tìm kiếm sách (REQ-03) và Quy trình mượn sách (REQ-04) hoạt động chính xác theo đúng tài liệu đặc tả.

 - Đảm bảo an toàn phân quyền: Hệ thống phân tách rất tốt quyền hạn giữa Thủ thư và Thành viên (REQ-08). Thành viên không thể xem hoặc tra cứu trái phép lịch sử mượn của người khác.

 - Xử lý ràng buộc tốt: Hệ thống chặn thành công các tài khoản bị khóa/hết hạn hoặc mượn quá số lượng sách quy định.

### 4.2. Điểm yếu
 - Lỗi nghiêm trọng trong quản trị quá hạn: Chức năng "Kiểm tra quá hạn" của thủ thư bị liệt hoàn toàn (BUG-02), khiến hệ thống không tự động cập nhật trạng thái các sách quá hạn, trực tiếp ảnh hưởng đến quy trình vận hành thư viện.

 - Hệ thống Validation Email bị lỗi logic ngược: Hệ thống chặn các email hợp lệ chuẩn quốc tế như some@email.com (BUG-04) nhưng lại cho phép lưu các định dạng thiếu TLD (Top-Level Domain) như user@domain (BUG-03).

 - Thiếu sót trải nghiệm người dùng (UX): Khi thành viên trả sách muộn, hệ thống không đưa ra bất kỳ cảnh báo vi phạm nào trên màn hình (BUG-01).

---

## 5. Đề xuất ưu tiên sửa lỗi

> 💡 Đây là phần **Quality Assurance**: bạn không chỉ tìm lỗi mà còn **đề xuất thứ tự ưu tiên** sửa chữa và đánh giá tác động.
> Nêu rõ tiêu chí ưu tiên: dựa vào **severity** (mức độ nghiêm trọng kỹ thuật) và/hoặc **priority** (mức độ ưu tiên kinh doanh).

| Thứ tự | Bug | Mức độ | Lý do ưu tiên |
|--------|-----|--------|---------------|
| 1 | BUG-02 | High | Ưu tiên hàng đầu (Blocker cho vận hành): Lỗi này làm gãy hoàn toàn luồng quản lý của Thủ thư. Nếu không sửa, thư viện không thể xác định được ai đang nợ sách quá hạn để gửi yêu cầu thu hồi. |
| 2 | BUG-04 | Medium | Ảnh hưởng trực tiếp đến người dùng: Lỗi chặn email đúng khiến các thành viên mới không thể đăng ký tài khoản bằng các email phổ thông. Cần sửa ngay để giải phóng luồng đăng ký. |
| 3 | BUG-03 | Medium | Ảnh hưởng đến tính toàn vẹn dữ liệu: Cho phép lưu email rác/sai định dạng sẽ khiến hệ thống tích tụ dữ liệu bẩn, làm hỏng tính năng gửi thông báo tự động (Notification) sau này. |
| 4 | BUG-01 | Medium | Cải thiện trải nghiệm & Nhận thức: Lỗi này không chặn luồng nghiệp vụ chính (sách vẫn được trả về kho "Có sẵn"), nhưng cần bổ sung sớm để người dùng nhận thức được việc họ đã vi phạm thời hạn mượn sách. |

---

## 6. Kết luận

Hệ thống hiện tại CHƯA SẴN SÀNG PHÁT HÀNH.

Mặc dù tỷ lệ Pass đạt khá cao (84%) và các tính năng cốt lõi như Mượn sách/Tìm kiếm hoạt động rất tốt, nhưng hệ thống đang vướng phải 1 lỗi High (Liệt chức năng quét quá hạn) và 2 lỗi Medium liên quan trực tiếp đến dữ liệu thành viên (Lỗi validation ngược đối với Email). Nếu phát hành phiên bản v1.0 này, thư viện sẽ gặp khủng hoảng trong việc đăng ký thành viên mới và hoàn toàn mất kiểm soát đối với việc quản lý sách quá hạn.

Khuyến nghị: Đội phát triển cần tập trung vá gấp BUG-02 và sửa lại Regex của phần cấu hình Email Validation trước khi tiến hành nghiệm thu lại.

---

## 7. Bài học rút ra (Tùy chọn)

Hiểu sâu về kiểm thử dòng dữ liệu: Việc viết test case cần bao phủ cả các trường hợp kiểm thử logic nghiệp vụ kết hợp (như trạng thái tài khoản + trạng thái sách) thay vì chỉ kiểm tra giao diện đơn thuần.

Tầm quan trọng của Regex: Một lỗi sai nhỏ trong chuỗi Regex kiểm tra định dạng dữ liệu đầu vào (Validation) có thể dẫn đến hệ quả nghiêm trọng, làm đảo lộn toàn bộ logic của hệ thống (chặn đúng, cho sai).

---

## 8. Khai báo sử dụng AI (Tùy chọn)

> Nếu nhóm có sử dụng công cụ AI (ChatGPT, Copilot, Gemini...), hãy ghi rõ bên dưới. Khai báo trung thực **không ảnh hưởng điểm** — đây là kỹ năng minh bạch trong nghề.

| Công cụ AI | Dùng cho phần nào | Bạn đã kiểm tra/chỉnh sửa thế nào |
|------------|-------------------|-----------------------------------|
| | | |
