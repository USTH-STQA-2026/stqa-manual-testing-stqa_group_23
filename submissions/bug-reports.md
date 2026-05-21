# Bug Reports — Báo cáo lỗi

| Information | |
|---|---|
| **Group** | STQA_Group_23 |
| **Date of Report** | 20/05/2026 |

---

## BUG-01

| Attribute | Detail |
|-----------|---------|
| **Bug ID** | BUG-01 |
| **Related TC** | TC-17 |
| **Related REQ** | REQ-05 |
| **Severity** | Medium |
| **Reporter** | Tran Duc Minh |
| **Date** | 20/05/2026 |
| **Status** | Open |

**Title:**
The system does not display an overdue warning when a member returns a late book.

**Environment:**
- Browser: Zen-browser
- OS: Linux
- UI Language: Vietnamese

**Preconditions:**
Successfully logged in with a member account (`ba.nguyen@email.com`). The member has a borrow record that is past its due date (`BR001`).

**Steps to reproduce:**
1. Navigate to the "Mượn/Trả" (Borrow/Return) tab.
2. Locate the overdue borrow record `BR001`.
3. Click the corresponding "Trả" (Return) button.

**Expected Result:**
The return process is successful (book status reverts to "Có sẵn"), and the system must explicitly display an overdue warning/notification to the user.

**Actual Result:**
The return process is successful, but the system does not display any overdue warning on the screen.

**Impact:**
Users are unaware of their violation of the return policy, which complicates enforcement if the library has a penalty or tracking system for late returns.

**Evidence:**
[image-18.png]

**Proposed Solution:**
Implement logic to compare the actual return date with the due date. If it exceeds the due date, trigger a Toast/Modal warning immediately after successfully updating the return status.

---

## BUG-02

| Attribute | Detail |
|-----------|---------|
| **Bug ID** | BUG-02 |
| **Related TC** | TC-18 |
| **Related REQ** | REQ-06 |
| **Severity** | High |
| **Reporter** | Tran Duc Minh |
| **Date** | 20/05/2026 |
| **Status** | Open |

**Title:**
The "Kiểm tra quá hạn" (Check Overdue) function does not update the status of overdue borrow records.

**Environment:**
- Browser: Zen-browser
- OS: Linux
- UI Language: Vietnamese

**Preconditions:**
Successfully logged in with a Librarian account. There is at least one overdue borrow record currently in the system (e.g., `BR001`).

**Steps to reproduce:**
1. Navigate to the borrow/return management interface.
2. Click the "Kiểm tra quá hạn" (Check Overdue) button.
3. Observe the status of record `BR001`.

**Expected Result:**
The status of record `BR001` must be updated from "Đang mượn" (Borrowing) to "Quá hạn" (Overdue).

**Actual Result:**
The system reports `0 outcome` (no changes made). Record `BR001` retains its previous status instead of updating to overdue.

**Impact:**
A critical flaw that breaks the Librarian's workflow. The Librarian cannot retrieve an accurate list of overdue books to initiate recalls.

**Evidence:**
[image-19.png]

**Proposed Solution:**
Review the backend query invoked when the "Kiểm tra quá hạn" button is triggered. Ensure the system correctly queries for the condition `dueDate < currentDate` AND current status = "Đang mượn".

---

## BUG-03

| Attribute | Detail |
|-----------|---------|
| **Bug ID** | BUG-03 |
| **Related TC** | TC-21 |
| **Related REQ** | REQ-07 |
| **Severity** | Medium |
| **Reporter** | Tran Duc Minh |
| **Date** | 20/05/2026 |
| **Status** | Open |

**Title:**
The system fails to validate and accepts incomplete email formats when adding a new member.

**Environment:**
- Browser: Zen-browser
- OS: Linux
- UI Language: Vietnamese

**Preconditions:**
Successfully logged in with a Librarian account. Navigated to the "Thêm thành viên" (Add Member) form.

**Steps to reproduce:**
1. Fill in the required information in the new member form.
2. In the Email field, input an incomplete domain format: `user@domain` (missing a top-level domain extension like `.com`).
3. Click "Lưu" (Save).

**Expected Result:**
The system must catch the validation error and display an error message prompting the user to enter a valid email format.

**Actual Result:**
Unexpected behavior occurs. The system does not display an accurate format error warning and fails to block the invalid input appropriately.

**Impact:**
Causes data integrity issues. The library will store accounts with unreachable email addresses, negatively affecting future features such as notifications.

**Evidence:**
[image-22.png]

**Proposed Solution:**
Implement a standard Regex pattern (e.g., `^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$`) to enforce the inclusion of a complete Top-Level Domain before form submission.

---

## BUG-04

| Attribute | Detail |
|-----------|---------|
| **Bug ID** | BUG-04 |
| **Related TC** | TC-19 |
| **Related REQ** | REQ-07 |
| **Severity** | Medium |
| **Reporter** | Tran Duc Minh |
| **Date** | 20/05/2026 |
| **Status** | Open |

**Title:**
The system incorrectly rejects a valid email address format, claiming the domain is invalid.

**Environment:**
- Browser: Zen-browser
- OS: Linux
- UI Language: Vietnamese

**Preconditions:**
Successfully logged in with a Librarian account. Navigated to the "Thêm thành viên" (Add Member) form.

**Steps to reproduce:**
1. Click Add Member and fill in the form with valid data.
2. In the Email field, input a valid email address: `some@email.com`.
3. Click "Lưu" (Save).

**Expected Result:**
The system should accept the valid email format and successfully create the new member profile.

**Actual Result:**
The system blocks the creation process and incorrectly displays a "domain invalid" error message.

**Impact:**
Prevents the registration of legitimate users, directly impacting the core functionality of user management.

**Evidence:**
[image-20.png]

**Proposed Solution:**
Review the email validation logic or the third-party domain verification API being used. Ensure standard domains (like `@email.com`) are not falsely flagged as invalid by overly strict or broken validation rules.