# Báo cáo tổng hợp test case 

## 1. Phạm vi và nguyên tắc tổng hợp

Báo cáo tổng hợp toàn bộ 9 file Markdown trong thư mục `Long`, gồm bốn phương pháp: Domain Testing/Equivalence Partitioning (EP) và Boundary Value Analysis (BVA), Decision Table Testing kết hợp Pairwise, State Transition Testing, và Use-Case Testing.

Mỗi Test Case ID chỉ được tính một lần. Bộ FR-09 xuất hiện ở cả `domain-testing/test-cases.md` và `decision-table/FR-09-test-case-and-test-design.md`; bản trong thư mục `decision-table` được dùng làm kết quả mới nhất vì có actual result và trạng thái thực thi, còn bản nhúng trong `domain-testing` vẫn ghi `Not executed`.

Quy ước trạng thái:

- `Pass`/`Fail`: artifact có kết luận thực thi.
- `Executed — oracle pending`: đã quan sát SUT nhưng requirement/expected oracle chưa đủ để kết luận Pass/Fail.
- `Not Run`: chưa có execution evidence. Nhãn `Executable`, `Partial`, `Blocked` của State Transition là mức sẵn sàng thiết kế, không phải kết quả chạy.

## 2. Executive summary

| Phương pháp | Feature | Tổng TC | Pass | Fail | Oracle pending | Not Run | Nhận định |
|---|---|---:|---:|---:|---:|---:|---|
| Domain Testing / EP + BVA | FR-03, FR-10, FR-16, FR-20 | 81 | 44 | 19 | 18 | 0 | Đã chạy toàn bộ; FR-16 còn nhiều case thiếu oracle. |
| Decision Table + Pairwise (+ BVA) | FR-09 | 11 | 4 | 7 | 0 | 0 | 1 lỗi sản phẩm có bằng chứng; 6 fail do thiếu fixture PW01–PW06. |
| State Transition Testing | Password-reset lifecycle | 3 | 0 | 0 | 0 | 3 | 1 executable, 1 partial, 1 blocked; chưa chạy. |
| Use-Case Testing | FR-02 | 5 | 0 | 0 | 0 | 5 | Cả 5 case ở trạng thái thiết kế `Not Run`. |
| **Tổng** | **7 feature/lifecycle** | **100** | **48** | **26** | **18** | **8** | **74 case đã có kết luận Pass/Fail.** |

- Tỷ lệ Pass trên các case đã có kết luận: **48/74 = 64,9%**.
- Tỷ lệ Fail trên các case đã có kết luận: **26/74 = 35,1%**.
- Tỷ lệ Pass trên toàn bộ inventory: **48/100 = 48%**; không nên dùng con số này như pass rate thực thi vì 26 case chưa có kết luận cuối (`oracle pending` hoặc `Not Run`).
- Coverage mapping của State Transition đạt 3/3 transition ở mức thiết kế, nhưng executable transition coverage chỉ 1/3.
- Use-Case Testing còn thiếu S06 — đăng nhập sau khi hết 30 giây khóa.

## 3. Tổng hợp theo phương pháp

### 3.1 Domain Testing / Equivalence Partitioning và BVA

#### FR-03 — Forgot password and password reset

Tổng 18 TC: 13 Pass, 5 Fail. Bộ test phủ miền OTP, mật khẩu, action quay lại và các biên độ dài OTP/mật khẩu.

| TC ID | Mục tiêu | Kết quả |
|---|---|---|
| FR03-EP-OTP-002 | OTP 4 số nhưng sai | Fail |
| FR03-EP-OTP-003 | OTP ngắn hơn 4 số | Fail |
| FR03-EP-OTP-004 | OTP dài hơn 4 số | Fail |
| FR03-EP-OTP-005 | OTP chứa ký tự không phải số | Fail |
| FR03-EP-OTP-006 | OTP rỗng | Pass |
| FR03-EP-PWD-001 | Mật khẩu hợp lệ `ValidPass1!` | Fail — GH-4 |
| FR03-EP-PWD-002 | Mật khẩu dưới 8 ký tự | Pass |
| FR03-EP-PWD-003 | Mật khẩu thiếu chữ hoa | Pass |
| FR03-EP-PWD-004 | Mật khẩu thiếu chữ thường | Pass |
| FR03-EP-PWD-005 | Mật khẩu thiếu số | Pass |
| FR03-EP-PWD-006 | Mật khẩu thiếu ký tự đặc biệt | Pass |
| FR03-EP-PWD-007 | Mật khẩu rỗng | Pass |
| FR03-EP-ACT-002 | Action quay lại | Pass |
| FR03-BVA-TC-001 | OTP dài 3 ký tự (B−1) | Pass |
| FR03-BVA-TC-002 | OTP dài 4 ký tự; mật khẩu dài 8 ký tự (B) | Pass |
| FR03-BVA-TC-003 | OTP dài 5 ký tự (B+1) | Pass |
| FR03-BVA-TC-004 | Mật khẩu dài 7 ký tự (B−1) | Pass |
| FR03-BVA-TC-006 | Mật khẩu dài 9 ký tự (B+1) | Pass |

Phát hiện chính: validation OTP không phân biệt đúng OTP sai, độ dài hoặc ký tự chữ; đồng thời mật khẩu thỏa rule công bố vẫn bị từ chối. Có độ lệch cần rà soát giữa EP và BVA: EP ghi nhận OTP 3/5 ký tự không được phát hiện, trong khi BVA tương ứng được đánh dấu Pass; evidence và oracle của hai nhóm cần được đối chiếu lại.

#### FR-10 — Order state machine

Tổng 6 TC: 4 Pass, 2 Fail. Không sinh BVA vì trạng thái là miền rời rạc, phù hợp hơn với EP/State Transition.

| TC ID | Mục tiêu | Kết quả |
|---|---|---|
| FR10-EP-001 | Hủy đơn `pending` | Pass |
| FR10-EP-005 | Chặn hủy đơn `shipping` | Fail — GH-1 |
| FR10-EP-006 | Chặn hủy lại đơn `canceled` | Pass |
| FR10-EP-009 | Hủy đơn `confirmed` | Pass |
| FR10-EP-010 | Chặn `canceled → delivered` | Fail — GH-2 |
| FR10-EP-011 | Chặn hủy đơn `delivered` | Pass |

Rủi ro chính: API cho phép hủy đơn đang giao và cho phép trạng thái cuối `canceled` chuyển sang `delivered`, phá vỡ tính bất biến của state machine.

#### FR-16 — Product import from CSV

Tổng 36 TC: 18 Pass, 18 `Executed — oracle pending`, 0 Fail. Tất cả đã chạy ngày 2026-06-29, nhưng một nửa chưa có requirement/oracle black-box đủ rõ.

| Trạng thái | TC ID |
|---|---|
| Pass (18) | FR16-EP-001, FR16-EP-002, FR16-EP-004, FR16-EP-005, FR16-EP-009, FR16-EP-010, FR16-EP-011, FR16-EP-012, FR16-EP-014, FR16-EP-018, FR16-EP-019, FR16-EP-020, FR16-EP-021, FR16-EP-022, FR16-EP-023, FR16-EP-024, FR16-EP-025, FR16-EP-027 |
| Executed — oracle pending (18) | FR16-EP-003, FR16-EP-006, FR16-EP-007, FR16-EP-008, FR16-EP-013, FR16-EP-015, FR16-EP-016, FR16-EP-017, FR16-EP-026; FR16-BVA-TC-001, FR16-BVA-TC-002, FR16-BVA-TC-003, FR16-BVA-TC-004, FR16-BVA-TC-005, FR16-BVA-TC-006, FR16-BVA-TC-007, FR16-BVA-TC-008, FR16-BVA-TC-009 |

Các miền đã phủ gồm: file hợp lệ/không chọn/rỗng/chỉ header/sai extension; delimiter và quote; header alias/sai/thiếu/thừa/trùng; name, price, category, image URL, duplicate, Unicode, whitespace, nhiều row và mixed-validity; token/quyền; empty product array; các candidate boundary về số row, độ dài name và số header nhận diện.

Các hành vi đáng chú ý nhưng chưa được phép kết luận defect: chấp nhận `.txt`, xử lý sai quoted comma/unclosed quote, lưu price âm hoặc text, lưu category không tồn tại, và hành vi non-admin. Cần chốt requirement trước khi đổi 18 case này thành Pass/Fail.

#### FR-20 — Mobile Checkout

Tổng 21 TC: 9 Pass, 12 Fail. Bộ test phủ cart, quantity, session, coupon, total, network, address, stale product và các biên BVA.

| TC ID | Mục tiêu | Kết quả |
|---|---|---|
| MCHECKOUT-EP-001 | Cart một sản phẩm hợp lệ | Pass |
| MCHECKOUT-EP-002 | Cart rỗng | Fail — GH-9 |
| MCHECKOUT-EP-005 | Quantity = 0 | Fail — GH-9 |
| MCHECKOUT-EP-010 | Chưa đăng nhập | Pass |
| MCHECKOUT-EP-011 | Session invalid/expired | Pass |
| MCHECKOUT-EP-012 | Voucher không tồn tại | Pass |
| MCHECKOUT-EP-013 | Voucher hết hạn | Pass |
| MCHECKOUT-EP-014 | Total client/server mismatch | Fail — GH-10 |
| MCHECKOUT-EP-015 | Network/API lỗi | Pass |
| MCHECKOUT-EP-017 | Shipping address Unicode | Pass |
| MCHECKOUT-EP-018 | Cart nhiều sản phẩm | Fail — LOCAL-FR20-01 |
| MCHECKOUT-EP-019 | Voucher hợp lệ | Fail — GH-11 |
| MCHECKOUT-EP-020 | Quantity âm | Fail — GH-9 |
| MCHECKOUT-EP-021 | Quantity không nguyên | Fail — GH-9 |
| MCHECKOUT-EP-022 | Product trong cart không còn tồn tại | Fail — GH-9 |
| MCHECKOUT-EP-023 | Total = 0 | Fail — GH-10 |
| MCHECKOUT-EP-024 | Total âm | Fail — GH-10 |
| MCHECKOUT-EP-025 | Coupon đúng ngưỡng 300.000 | Fail — GH-12 |
| MCHECKOUT-BVA-QTY-003 | Quantity = 2 (B+1) | Pass |
| MCHECKOUT-BVA-COUPON-001 | Coupon total = 299.999 (B−1) | Pass |
| MCHECKOUT-BVA-COUPON-003 | Coupon total = 300.001 (B+1) | Fail — GH-11 |

Nhóm lỗi tập trung:

- Backend chấp nhận empty cart, quantity 0/âm/thập phân và stale product (GH-9).
- Backend tin `total_amount` từ client, kể cả 0, âm hoặc không khớp (GH-10).
- Công thức giảm theo phần trăm tạo discount âm và final amount tăng (GH-11).
- Sai toán tử biên: requirement là `>=`, implementation hành xử như `>` (GH-12).
- Checkout nhiều sản phẩm bỏ item cuối khỏi request (`cart.slice(0, -1)`) nhưng vẫn dùng tổng của cả cart (LOCAL-FR20-01).

### 3.2 Decision Table Testing — FR-09 Mã giảm giá

Thiết kế gồm 5 điều kiện Boolean (32 luật đầy đủ), rút gọn thành 6 luật R1–R6. Luật rủi ro cao R6 được mở rộng bằng 6 case pairwise, bao phủ toàn bộ cặp giá trị của coupon type, total so với min, expiry và usage. Tổng 11 TC: 4 Pass, 7 Fail.

| TC ID | Rule/coverage | Kết quả |
|---|---|---|
| FR09-DT-001 | R1 — mã không tồn tại/inactive | Pass |
| FR09-DT-002 | R2 — mã hết hạn | Pass |
| FR09-DT-003 | R3 + BVA — total 299.999 dưới min | Fail — coupon vẫn được áp dụng và tính tiền sai |
| FR09-DT-004 | R4 — không có JWT | Pass |
| FR09-DT-005 | R5 — hết lượt dùng | Pass |
| FR09-PW-001 | R6/CR1 — percent, bằng min, expiry gần, usage 0 | Fail — thiếu fixture PW01 |
| FR09-PW-002 | R6/CR1 — percent, bằng min, expiry xa, usage 1 | Fail — thiếu fixture PW02 |
| FR09-PW-003 | R6/CR2 — fixed, trên min, expiry gần, usage 0 | Fail — thiếu fixture PW03 |
| FR09-PW-004 | R6/CR2 — fixed, trên min, expiry xa, usage 1 | Fail — thiếu fixture PW04 |
| FR09-PW-005 | R6/CR1 — percent, trên min, expiry gần, usage 1 | Fail — thiếu fixture PW05 |
| FR09-PW-006 | R6/CR2 + BVA — fixed, bằng min, expiry xa, usage 0 | Fail — thiếu fixture PW06 |

Diễn giải thận trọng: sáu case Pairwise hiện là **test setup/fixture failures**, chưa chứng minh lỗi công thức percent/fixed hay luật R6. FR09-DT-003 mới là failure có bằng chứng hành vi sản phẩm. Kết quả này trùng root cause coupon với FR-20/GH-11 và sai biên với GH-12.

### 3.3 State Transition Testing — Password-reset lifecycle

Mô hình có ba trạng thái S0 (chưa nhận token), S1 (đã nhận token), S2 (reset hoàn tất); ba transition T01–T03. Design mapping coverage là 100%, nhưng chỉ T01 có oracle đầy đủ. Chưa có TC nào được thực thi.

| TC ID | Loại | Transition | Readiness / execution |
|---|---|---|---|
| STT-PASSWORD-RESET-V-001 | Valid | T01: S0 → S1 | Executable; Not Run |
| STT-PASSWORD-RESET-V-002 | Valid/end-to-end | T01: S0 → S1; T02: S1 → S2 | Partial; T02 thiếu success response/cách quan sát S2; Not Run |
| STT-PASSWORD-RESET-I-001 | Invalid | T03: S0 → Unspecified | Blocked; thiếu rejection oracle và trạng thái đích; Not Run |

Khoảng trống chính: response reset thành công, cách xác nhận mật khẩu đã đổi, token-email matching, invalid token, expiry/timezone, single-use/reuse, token replacement, password policy, retry/rate limit và session invalidation.

### 3.4 Use-Case Testing — FR-02 Đăng nhập và khóa tài khoản

Tổng 5 TC, tất cả `Not Run`. Thiết kế phủ success flow, email sai định dạng, khóa sau ba lần sai, đăng nhập đúng sau một lần sai và thử đăng nhập trong thời gian khóa.

| TC ID | Scenario | Kết quả hiện tại |
|---|---|---|
| TC_FR02_S01_LoginSuccess | Đăng nhập thành công, nhận/lưu/gửi JWT | Not Run |
| TC_FR02_S02_InvalidEmailFormat | HTML5 validation cho email sai định dạng | Not Run |
| TC_FR02_S03_LockAfterThreeFailures | Khóa 30 giây sau ba lần sai liên tiếp | Not Run; có thể Blocked nếu không quan sát được counter |
| TC_FR02_S04_LoginAfterPriorFailure | Đăng nhập đúng sau một lần sai | Not Run; có thể Blocked nếu không thiết lập/quan sát được counter |
| TC_FR02_S05_LoginWhileLocked | Đăng nhập trong thời gian khóa | Not Run; có thể Blocked nếu không thiết lập được trạng thái khóa |

Coverage gap: S06 — hành vi sau khi hết 30 giây — mới có planned ID `TC_FR02_S06_LoginAfterTimeout`, chưa có test case chi tiết nên không nằm trong tổng 100 TC. Requirement cũng chưa rõ reset counter sau login đúng, phản hồi lần sai 1–2, response trong lúc khóa, điều hướng thành công, exact error/status và continuation của HTML5 validation.

## 4. Defect và rủi ro nổi bật

| Mức ưu tiên | Khu vực | Bằng chứng | Rủi ro |
|---|---|---|---|
| Critical | Checkout tin total từ client | GH-10; FR20-EP-014/023/024 | Có thể tạo đơn với số tiền bị sửa, bằng 0 hoặc âm. |
| Critical | Công thức coupon phần trăm sai | GH-11; FR20-EP-019/BVA-COUPON-003; FR09-DT-003 | Discount âm, thành tiền tăng mạnh; ảnh hưởng trực tiếp tài chính. |
| High | Checkout không validate cart/item/quantity | GH-9; 5 TC Fail | Tạo order rỗng hoặc chứa dữ liệu không hợp lệ/stale. |
| High | Mất item cuối ở cart nhiều sản phẩm | LOCAL-FR20-01 | Order không bảo toàn nội dung cart. |
| High | Vi phạm state machine đơn hàng | GH-1, GH-2 | Hủy đơn đang giao hoặc hồi sinh đơn đã hủy. |
| High | OTP validation không đúng | 4 TC FR-03 Fail | Có thể làm yếu hoặc phá luồng reset mật khẩu. |
| Medium/High | Mật khẩu hợp lệ bị từ chối | GH-4 | Chặn người dùng hoàn tất reset. |
| Medium | Sai biên coupon `>=` thành `>` | GH-12 | Từ chối coupon hợp lệ đúng ngưỡng. |
| Process risk | Thiếu fixture Pairwise | FR09-PW-001…006 | Sáu kết quả Fail chưa đánh giá được sản phẩm. |
| Oracle risk | FR-16 thiếu oracle cho 18 TC | 18 case pending | Hành vi nguy hiểm có thể bị bỏ sót hoặc kết luận sai. |

## 5. Chất lượng bộ test và điểm không nhất quán

1. FR-09 bị sao chép ở hai nơi với trạng thái khác nhau: bản Domain ghi `Not executed`, bản Decision Table ghi 4 Pass/7 Fail. Cần giữ một nguồn kết quả duy nhất hoặc tự động đồng bộ.
2. FR-03 có dấu hiệu mâu thuẫn giữa EP và BVA cho OTP dài 3/5 ký tự. Cần so sánh test setup, expected oracle và evidence trước khi chốt regression status.
3. `FR03-BVA-TC-005` được artifact ghi rõ là test case đã loại, vì vậy không nằm trong inventory 100 case; các ID dạng `FR03-BVA-*-MIN/MAX` chỉ là Boundary ID, không phải TC ID.
4. Một số FR-20 Pass dựa trên source-assisted/static verification thay vì runtime screenshot/trace đầy đủ; nên gắn nhãn evidence type trong dashboard.
5. Sáu Pairwise case không nên được tính là product defect cho đến khi tạo đúng fixture PW01–PW06 và chạy lại.
6. `Executed — oracle pending` không đồng nghĩa Pass. FR-16 cần acceptance criteria rõ cho CSV parsing, validation dữ liệu, quyền non-admin và boundary trước khi release decision.
7. State Transition và Use-Case có thiết kế/traceability tốt nhưng chưa có execution evidence, nên không được dùng để kết luận chất lượng SUT.

## 6. Khuyến nghị hành động

1. Ưu tiên sửa và regression test các lỗi tài chính/toàn vẹn checkout: GH-10, GH-11, GH-9, LOCAL-FR20-01, sau đó GH-12.
2. Sửa policy state transition và chạy lại toàn bộ 6 case FR-10, đặc biệt hai terminal-state invariants.
3. Xác minh lại FR-03 bằng một bộ evidence thống nhất để giải quyết mâu thuẫn EP/BVA; điều tra GH-4 và validation OTP.
4. Tạo/activate fixture PW01–PW06, reset coupon usage đúng precondition rồi chạy lại sáu Pairwise case. Tách `Blocked/Test Data Error` khỏi `Fail` nếu framework hỗ trợ.
5. Chốt requirement FR-16; sau đó phân loại lại 18 oracle-pending case và tạo bug cho các hành vi thực sự vi phạm.
6. Bổ sung oracle cho password reset (§1.4, invalid token, expiry/reuse) rồi chạy ba STT case.
7. Thiết lập cách reset/quan sát login failure counter, làm rõ hành vi sau 30 giây và chạy năm UCT case; bổ sung TC cho S06.

## 7. Kết luận

Bộ artifact có phạm vi rộng và truy vết khá tốt, đặc biệt ở Decision Table, BVA và State Transition design. Tuy nhiên, hệ thống **chưa đủ căn cứ để đánh giá sẵn sàng phát hành**: 26/74 case đã có kết luận đang Fail, trong đó có lỗi tài chính và toàn vẹn đơn hàng mức cao; 18 case thiếu oracle và 8 case chưa chạy. Trọng tâm gần nhất nên là sửa các lỗi checkout/coupon, chuẩn hóa test data và oracle, rồi chạy regression trên cùng một nguồn kết quả thống nhất.
