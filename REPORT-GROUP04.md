# REPORT-GROUP04 — Báo cáo tổng hợp kiểm thử nhóm 04

## 1. Phạm vi và quy ước

Báo cáo được tổng hợp từ ba file:

- `Long/SUMMARY-REPORT.md`
- `Thịnh/summary-report-23127484.md`
- `Thiện/summary-report-23127482.md`

Quy ước đếm:

- Test case được cộng theo inventory do từng thành viên tạo. Các TC có mục tiêu tương tự giữa các thành viên vẫn được tính riêng vì là artifact độc lập.
- `Passed` và `Failed` chỉ gồm TC đã có kết luận. `Executed — oracle pending` và `Not Run/Not executed` được giữ riêng, không quy đổi thành Pass hoặc Fail.
- Bug của mỗi thành viên được tính theo Bug ID/defect record unique trong summary của người đó. Bug trùng hành vi giữa các thành viên chưa được khử trùng lặp toàn nhóm; vì vậy số tổng là **bug records được ghi nhận**, không phải số product defect unique toàn cục.
- Long có một nhóm lỗi OTP được mô tả là bug candidate nhưng chưa có Bug ID; nhóm này không được tính vào tổng bug chính thức.

## 2. Tổng số test case của nhóm

| Thành viên | Tổng TC | Passed | Failed | Executed — oracle pending | Not Run / Not executed | Tỷ lệ đóng góp TC |
|---|---:|---:|---:|---:|---:|---:|
| Long | 100 | 48 | 26 | 18 | 8 | 41,3% |
| Thịnh | 117 | 79 | 38 | 0 | 0 | 48,3% |
| Thiện | 25 | 9 | 4 | 0 | 12 | 10,3% |
| **Tổng nhóm** | **242** | **136** | **68** | **18** | **20** | **100%** |

Nhóm đã tạo tổng cộng **242 test cases**. Có **204 TC đã có kết luận Pass/Fail**, tương ứng 84,3% inventory; 38 TC còn lại chưa có kết luận cuối.

- Pass rate trên các TC đã có kết luận: **136/204 = 66,7%**.
- Fail rate trên các TC đã có kết luận: **68/204 = 33,3%**.
- Nếu tính trên toàn bộ inventory: 56,2% Pass, 28,1% Fail, 7,4% oracle pending và 8,3% chưa chạy.

## 3. Coverage test case theo feature requirement

| Feature requirement / lifecycle | Long | Thịnh | Thiện | Tổng TC | Kỹ thuật chính |
|---|---:|---:|---:|---:|---|
| FR-02 — Login / account lock | 5 | 21 | 0 | **26** | Use Case, EP, BVA |
| FR-03 — Forgot/reset password | 18 | 0 | 6 | **24** | EP, BVA, Use Case |
| Password-reset lifecycle §1.3/§1.4 | 3 | 0 | 0 | **3** | State Transition |
| FR-06 — Product Detail / Add to Cart Mobile | 0 | 15 | 0 | **15** | EP, BVA |
| FR-08 — Checkout | 0 | 18 | 0 | **18** | State Transition, Use Case |
| FR-09 — Coupon | 11 | 43 | 11 | **65** | EP, BVA, Decision Table, Pairwise |
| FR-10 — Order state machine | 6 | 0 | 8 | **14** | EP, State Transition |
| FR-14 — Category CRUD | 0 | 20 | 0 | **20** | EP, BVA |
| FR-16 — Product import from CSV | 36 | 0 | 0 | **36** | EP, BVA |
| FR-20 — Mobile Checkout | 21 | 0 | 0 | **21** | EP, BVA |
| **Tổng** | **100** | **117** | **25** | **242** |  |

Nhóm bao phủ 9 Feature Requirement chính (`FR-02`, `FR-03`, `FR-06`, `FR-08`, `FR-09`, `FR-10`, `FR-14`, `FR-16`, `FR-20`) và một lifecycle API password reset. FR-09 có coverage lớn nhất với 65 TC; tiếp theo là FR-16 với 36 TC và FR-02 với 26 TC.

Lưu ý: password-reset lifecycle của Long dùng nguồn API §1.3/§1.4 nên được giữ thành một dòng riêng thay vì tự động gộp vào FR-03.

## 4. Coverage test case theo test design technique

Để tổng theo kỹ thuật không đếm trùng, các kỹ thuật kết hợp được gom thành bốn nhóm inventory loại trừ nhau.

| Nhóm kỹ thuật | Long | Thịnh | Thiện | Tổng TC | Feature coverage |
|---|---:|---:|---:|---:|---|
| Domain Testing / EP + BVA | 81 | 83 | 0 | **164** | FR-02, FR-03, FR-06, FR-09, FR-10, FR-14, FR-16, FR-20 |
| Decision Table + Pairwise | 11 | 16 | 11 | **38** | FR-09 |
| State Transition Testing | 3 | 9 | 8 | **20** | Password-reset lifecycle, FR-08, FR-10 |
| Use-Case Testing | 5 | 9 | 6 | **20** | FR-02, FR-03, FR-08 |
| **Tổng** | **100** | **117** | **25** | **242** |  |

Chi tiết từ các summary:

- Long: 81 Domain/EP+BVA; 11 Decision Table/Pairwise; 3 State Transition; 5 Use Case.
- Thịnh: 47 EP, 36 BVA, 6 Decision Table, 10 Pairwise, 9 State Transition, 9 Use Case.
- Thiện: 11 Decision Table kết hợp Pairwise, 8 State Transition, 6 Use Case.

EP/Domain và BVA chiếm 164/242 = **67,8%** inventory. Decision Table/Pairwise chiếm 15,7%; State Transition và Use Case mỗi nhóm chiếm 8,3%.

## 5. Status test case toàn nhóm

| Status | Số lượng | Tỷ lệ trên 242 TC | Diễn giải |
|---|---:|---:|---|
| Passed | **136** | 56,2% | Có execution result và kết luận Pass. |
| Failed | **68** | 28,1% | Có execution result và kết luận Fail, nhưng một số Fail của Long là lỗi fixture/test data. |
| Executed — oracle pending | **18** | 7,4% | Đã quan sát SUT nhưng chưa đủ requirement/oracle để kết luận. |
| Not Run / Not executed | **20** | 8,3% | Chưa có execution evidence hoặc chưa cập nhật trạng thái. |
| **Tổng** | **242** | **100%** |  |

Điểm cần lưu ý khi đọc số Failed:

- 6 case Pairwise FR-09 của Long fail do thiếu fixture `PW01`–`PW06`, chưa chứng minh product defect.
- 18 case FR-16 của Long đã chạy nhưng thiếu oracle, nên không được tính Pass.
- 12 case FR-03/FR-10 của Thiện chưa cập nhật trạng thái, dù 4 TC khác đã liên kết với bug report.

## 6. Tổng số bug của nhóm và từng thành viên

| Thành viên | Bug records unique trong summary | Critical | High | Medium | Low | Ghi chú |
|---|---:|---:|---:|---:|---:|---|
| Long | **8** | 2 | 5 | 1 | 0 | Tính các ID GH-1, GH-2, GH-4, GH-9, GH-10, GH-11, GH-12 và LOCAL-FR20-01. Không tính bug candidate OTP chưa có ID. |
| Thịnh | **20** | 4 | 8 | 8 | 0 | Đã khử trùng lặp nội bộ: 10 bug reports FR-08 từ hai kỹ thuật được quy về 5 lỗi unique. |
| Thiện | **4** | 0 | 3 | 1 | 0 | Hai bug FR-03 và hai bug FR-10; Bug ID là cục bộ theo folder. |
| **Tổng bug records** | **32** | **6** | **16** | **10** | **0** | Chưa khử trùng lặp giữa các thành viên. |

Nhóm đã ghi nhận **32 bug records theo attribution của từng thành viên**. Con số này phù hợp để báo cáo khối lượng phát hiện của từng người, nhưng không nên diễn đạt là “32 product defects unique” vì có các lỗi giống nhau được nhiều người phát hiện.

Đối với Long, summary dùng nhãn ưu tiên thay cho severity chính thức. Báo cáo nhóm chuẩn hóa `Medium/High` của GH-4 thành `High`; các nhãn `Critical`, `High`, `Medium` còn lại được giữ nguyên.

## 7. Coverage bug theo feature requirement

| Feature requirement | Long | Thịnh | Thiện | Tổng bug records | Nội dung lỗi chính |
|---|---:|---:|---:|---:|---|
| FR-02 | 0 | 0 | 0 | **0** | Chưa có bug record chính thức. |
| FR-03 | 1 | 0 | 2 | **3** | OTP không đủ định dạng; mật khẩu mạnh/hợp lệ bị xử lý sai. |
| FR-06 | 0 | 6 | 0 | **6** | Quantity 0, âm, thập phân, rỗng, mixed/alphabetic bị chấp nhận hoặc mặc định sai. |
| FR-08 | 0 | 5 | 0 | **5** | Editable/tampered total, cart không clear, empty-cart checkout, duplicate checkout. |
| FR-09 | 2 | 3 | 0 | **5** | Công thức percent, biên `>=`, authentication bypass. |
| FR-10 | 2 | 0 | 2 | **4** | Hủy đơn shipping và chuyển khỏi trạng thái cuối canceled. |
| FR-14 | 0 | 6 | 0 | **6** | Duplicate/empty category, access control, invalid ID deletion. |
| FR-16 | 0 | 0 | 0 | **0** | Có hành vi đáng ngờ nhưng 18 TC còn thiếu oracle. |
| FR-20 | 3 | 0 | 0 | **3** | Invalid cart/item/quantity, tin total client, mất item cuối. |
| **Tổng** | **8** | **20** | **4** | **32** |  |

Bug records tập trung nhiều nhất ở FR-06 và FR-14 (mỗi feature 6 record), sau đó FR-08 và FR-09 (mỗi feature 5 record). Tuy nhiên, số record không phản ánh trực tiếp mức độ rủi ro: các lỗi checkout/coupon liên quan tiền và access control có severity cao hơn.

## 8. Coverage bug theo severity

| Severity | Long | Thịnh | Thiện | Tổng | Tỷ lệ |
|---|---:|---:|---:|---:|---:|
| Critical | 2 | 4 | 0 | **6** | 18,8% |
| High | 5 | 8 | 3 | **16** | 50,0% |
| Medium | 1 | 8 | 1 | **10** | 31,3% |
| Low | 0 | 0 | 0 | **0** | 0% |
| **Tổng** | **8** | **20** | **4** | **32** | **100%** |

Các nhóm Critical/High chủ yếu liên quan:

- Backend tin `total_amount` từ client và tính coupon sai.
- Authentication/authorization bypass ở coupon và Category CRUD.
- Empty/invalid cart hoặc quantity vẫn tạo order.
- Cart không clear, duplicate checkout và mất item.
- Vi phạm state machine đơn hàng.
- Mật khẩu hợp lệ bị từ chối hoặc password-reset validation sai.

## 9. Trùng lặp bug giữa thành viên

Các overlap có thể xác định trực tiếp từ mô tả summary:

| Product behavior | Long | Thành viên khác |
|---|---|---|
| Công thức coupon phần trăm sai | GH-11 | Thịnh bug #1 |
| Coupon sai biên `>` thay vì `>=` | GH-12 | Thịnh bug #2 |
| Backend tin `total_amount` từ client | GH-10 | Thịnh BUG-FR08-002 |
| Empty-cart checkout | Một phần GH-9 | Thịnh BUG-FR08-004 |
| User hủy đơn `shipping` | GH-1 | Thiện FR-10 BUG-01 |
| `canceled` vẫn chuyển sang trạng thái khác | GH-2 | Thiện FR-10 BUG-02 |
| Mật khẩu mới hợp lệ/mạnh bị từ chối | GH-4 | Thiện FR-03 BUG-02 |

Do GH-9 của Long gộp nhiều biểu hiện vào một issue, trong khi thành viên khác có thể tách bug theo từng behavior, không thể suy ra chính xác số product defect unique toàn nhóm chỉ từ ba summary. Nhóm nên tạo một canonical bug registry với `Global Bug ID`, root cause/behavior, các TC liên quan và các Bug ID cục bộ.

## 10. Kết luận

Nhóm 04 đã tạo **242 test cases**, bao phủ 9 Feature Requirement, một password-reset lifecycle và đầy đủ sáu họ kỹ thuật: EP/Domain Testing, BVA, Decision Table, Pairwise, State Transition và Use Case.

Trong 204 TC đã có kết luận, **136 Passed** và **68 Failed**, tương ứng pass rate 66,7%. Ngoài ra còn 18 TC thiếu oracle và 20 TC chưa chạy/cập nhật trạng thái.

Ba thành viên ghi nhận tổng cộng **32 bug records**: Long 8, Thịnh 20 và Thiện 4. Severity gồm 6 Critical, 16 High và 10 Medium. Vì tồn tại nhiều phát hiện trùng hành vi giữa thành viên, 32 là tổng attribution record; cần canonical hóa trước khi công bố số product defect unique toàn nhóm.
