# Báo cáo tổng hợp kiểm thử EShop

## 1. Phạm vi tổng hợp

Báo cáo này tổng hợp các artifact kiểm thử trong thư mục `A-05`, bao gồm:

- `ai-audit-report.md`
- `Test case/FR09_Test_Cases.md`
- `Test Design/Decision_Table_Design.md`
- `Test Design/Pairwise_Design.md`
- `test-cases/`
- `test-runs/sprint-1-test-run.md`
- `test-summary/traceability-matrix.md`
- `23127484/generated/`
- `23127484/skills/`
- `23127484/templates/`

Các kỹ thuật được tổng hợp:

- Equivalence Partitioning (EP)
- Boundary Value Analysis (BVA)
- Decision Table Testing
- Pairwise Testing
- State Transition Testing
- Use-case Testing

Ghi chú dữ liệu: `traceability-matrix.md` có 83 dòng test case thực tế trong bảng, trong khi phần `Coverage Summary` cũ ghi tổng 82. Chênh lệch là `TC-CAT-SEC-001` thuộc FR-14. Báo cáo này dùng cách đếm trực tiếp từ artifact test case/traceability, nên tổng EP+BVA là 83.

---

## 2. Tổng số test cases đã tạo

| Kỹ thuật thiết kế | Feature requirements covered | Số test cases | Passed | Failed |
| --- | --- | ---: | ---: | ---: |
| EP | FR-02, FR-06, FR-09, FR-14 | 47 | 32 | 15 |
| BVA | FR-02, FR-06, FR-09, FR-14 | 36 | 30 | 6 |
| Decision Table | FR-09 | 6 | 4 | 2 |
| Pairwise | FR-09 | 10 | 5 | 5 |
| State Transition | FR-08 | 9 | 4 | 5 |
| Use-case | FR-08 | 9 | 4 | 5 |
| **Tổng** | **FR-02, FR-06, FR-08, FR-09, FR-14** | **117** | **79** | **38** |

---

## 3. Coverage của test cases theo feature requirement

| Feature requirement | Kỹ thuật áp dụng | Số test cases | Passed | Failed | Ghi chú coverage |
| --- | --- | ---: | ---: | ---: | --- |
| FR-02 Login | EP, BVA | 21 | 21 | 0 | Bao phủ login hợp lệ/không hợp lệ, SQL injection input, lockout attempts, password length boundaries. |
| FR-06 Product Detail / Add to Cart Mobile | EP, BVA | 15 | 8 | 7 | Bao phủ xem chi tiết sản phẩm, thêm vào giỏ, quantity hợp lệ/không hợp lệ, boundary quantity. |
| FR-08 Checkout | State Transition, Use-case | 18 | 8 | 10 | Bao phủ guest/auth checkout, checkout review, editable total, tampered total_amount, empty cart, cart clear, duplicate checkout. |
| FR-09 Coupon | EP, BVA, Decision Table, Pairwise | 43 | 31 | 12 | Bao phủ C1-C5 coupon conditions, threshold boundaries, percent/fixed formula, auth, usage limit, expired/inactive/non-existent coupon. |
| FR-14 Category CRUD | EP, BVA | 20 | 11 | 9 | Bao phủ create/delete category, duplicate/empty/whitespace name, access control, invalid IDs, security/XSS case. |
| **Tổng** |  | **117** | **79** | **38** |  |

---

## 4. Coverage của test cases theo kỹ thuật thiết kế

### EP

- Tổng: 47 test cases.
- Covered requirements: FR-02, FR-06, FR-09, FR-14.
- Mục tiêu coverage: phân vùng hợp lệ/không hợp lệ, input security, access control, business rule validation.
- Status: 32 passed, 15 failed.

### BVA

- Tổng: 36 test cases.
- Covered requirements: FR-02, FR-06, FR-09, FR-14.
- Mục tiêu coverage: min-1, min, min+1, max/max+1, nominal values cho password length, login attempts, order total threshold, usage count, expiry date, category name length, ID, quantity.
- Status: 30 passed, 6 failed.

### Decision Table

- Tổng: 6 test cases.
- Covered requirement: FR-09.
- Mục tiêu coverage: reduced one-fault model cho 5 điều kiện coupon C1-C5 và effects E1/E2.
- Status: 4 passed, 2 failed.

### Pairwise

- Tổng: 10 test cases.
- Covered requirement: FR-09.
- Mục tiêu coverage: high-risk combinations giữa coupon type, order total vs min, expiry, authentication, usage count.
- Status: 5 passed, 5 failed.

### State Transition

- Tổng: 9 test cases.
- Covered requirement: FR-08.
- Mục tiêu coverage: checkout states từ anonymous/authenticated cart, checkout review, submitting, success/cart-cleared, blocked states.
- Status: 4 passed, 5 failed.

### Use-case

- Tổng: 9 test cases.
- Covered requirement: FR-08.
- Mục tiêu coverage: actor goal checkout flow, main success scenario, alternative flows, exception flows.
- Status: 4 passed, 5 failed.

---

## 5. Status tổng hợp của test cases

| Status | Số lượng | Tỷ lệ |
| --- | ---: | ---: |
| Passed | 79 | 67.52% |
| Failed | 38 | 32.48% |
| Blocked / Not Run | 0 | 0.00% |
| **Total** | **117** | **100.00%** |

---

## 6. Tổng số bugs đã tìm được

Tổng số bugs unique: **20**.

Cách tính:

- 14 bugs từ `test-summary/traceability-matrix.md` và `test-runs/sprint-1-test-run.md` cho EP/BVA.
- 1 bug bổ sung từ Decision Table/Pairwise FR-09: authentication bypass khi apply coupon không có `user_id`/auth context. Hai bug còn lại trong Decision Table/Pairwise trùng với bug FR-09 đã có: percent formula và threshold boundary.
- 5 bugs unique từ FR-08 checkout. State Transition và Use-case đều phát hiện cùng 5 lỗi này, nên chỉ tính unique bugs một lần.

Ghi chú: trong artifact có 10 file bug report cho FR-08 vì mỗi kỹ thuật State Transition và Use-case có bộ bug report riêng, nhưng chúng map về cùng 5 lỗi checkout unique.

---

## 7. Coverage của bugs theo feature requirement

| Feature requirement | Số bugs unique | Bug IDs / mô tả ngắn |
| --- | ---: | --- |
| FR-06 | 6 | #9 quantity = 0 accepted; #10 negative quantity accepted; #11 decimal quantity rounded/accepted; #12 empty quantity defaults; #13 mixed quantity parsed; #14 alphabetic quantity defaults. |
| FR-08 | 5 | BUG-FR08-001 editable checkout total; BUG-FR08-002 backend trusts client total_amount; BUG-FR08-003 cart not cleared; BUG-FR08-004 empty cart checkout creates order; BUG-FR08-005 duplicate checkout after success. |
| FR-09 | 3 | #1 percent discount formula; #2 threshold boundary uses `>` instead of `>=`; FR09-AUTH-BYPASS anonymous/no-user coupon apply accepted. |
| FR-14 | 6 | #3 duplicate category allowed; #4 empty/whitespace category name allowed; #5 normal user can create category; #6 normal user can delete category; #7 invalid negative/zero ID deletion accepted; #8 non-numeric/invalid ID deletion accepted. |
| FR-02 | 0 | No bugs found in current artifacts. |
| **Tổng** | **20** |  |

---

## 8. Coverage của bugs theo severity

Severity của FR-08 được lấy trực tiếp từ bug report files. Severity của bug cũ (#1-#14) không có trường riêng trong artifact, nên được phân loại dựa trên impact từ mô tả lỗi và test evidence.

| Severity | Số bugs unique | Bugs |
| --- | ---: | --- |
| Critical | 4 | FR09-AUTH-BYPASS; #5 normal user create category; #6 normal user delete category; BUG-FR08-002 backend trusts client `total_amount`. |
| High | 8 | #1 percent formula; #4 empty/whitespace category name; #9 quantity 0 accepted; #10 negative quantity accepted; BUG-FR08-001 editable total; BUG-FR08-003 cart not cleared; BUG-FR08-004 empty cart checkout; BUG-FR08-005 duplicate checkout. |
| Medium | 8 | #2 threshold boundary; #3 duplicate category; #7 invalid ID deletion; #8 non-numeric ID deletion; #11 decimal quantity; #12 empty quantity defaults; #13 mixed quantity parsed; #14 alphabetic quantity defaults. |
| Low | 0 | None identified. |
| **Tổng** | **20** |  |

---

## 9. Chi tiết bug coverage theo kỹ thuật

| Kỹ thuật | Bugs exposed | Ghi chú |
| --- | --- | --- |
| EP | #1, #3, #4, #5, #6, #7, #8, #9, #10, #11, #12, #13, #14 | Phát hiện nhiều lỗi validation, access control và input partition. |
| BVA | #2, #4, #7, #8, #9 | Phát hiện lỗi boundary threshold, boundary category name/ID, boundary quantity. |
| Decision Table | #1, FR09-AUTH-BYPASS | Phát hiện lỗi formula và auth rule trên điều kiện C4. |
| Pairwise | #1, #2, FR09-AUTH-BYPASS | Phát hiện lỗi qua tổ hợp high-risk giữa auth, threshold và coupon type. |
| State Transition | BUG-FR08-001 đến BUG-FR08-005 | Phát hiện lỗi transition/postcondition checkout. |
| Use-case | BUG-UC-FR08-001 đến BUG-UC-FR08-005 | Phát hiện cùng 5 lỗi FR-08 theo actor goal và alternative/exception flows. |

---

## 10. Kết luận

Tổng cộng đã tạo **117 test cases** trên 6 kỹ thuật thiết kế kiểm thử, bao phủ **5 feature requirements**: FR-02, FR-06, FR-08, FR-09 và FR-14.

Kết quả thực thi cho thấy **79 test cases passed** và **38 test cases failed**. Các failure đã giúp phát hiện **20 bugs unique**, tập trung nhiều nhất ở FR-06, FR-08 và FR-14. Các lỗi có rủi ro cao nhất nằm ở nhóm access control và dữ liệu tài chính checkout/coupon, đặc biệt là backend tin `total_amount` từ client và coupon authentication bypass.
