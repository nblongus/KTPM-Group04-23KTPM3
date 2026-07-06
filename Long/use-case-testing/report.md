# Use-Case Testing Report — FR-02: Đăng nhập và khóa tài khoản

## 1. Report information

| Field | Value |
|---|---|
| Feature ID | FR-02 |
| Technique | Use-Case Testing |
| Requirement source | `README.md` — EShop System Requirements Specification, version 2.0 |
| Test scope | 5 test case đã thiết kế cho S01–S05. S06 chưa có test case vì hành vi sau 30 giây khóa chưa được đặc tả. |
| Execution period | Missing information — chưa có thời gian thực thi do người dùng cung cấp. |
| Test environment | Thiết kế tham chiếu Frontend Web `http://localhost:5173` và Backend API `http://localhost:3000`; môi trường thực thi thực tế chưa được xác nhận. |
| Report status | Incomplete |

## 2. Executive summary

Báo cáo tổng hợp 5 test case đã sinh cho FR-02. Trạng thái hiện có trong artifact là trạng thái thiết kế mặc định `Not Run`, chưa phải kết quả thực thi do người dùng xác nhận.

| Metric | Count | Note |
|---|---:|---|
| Total test cases in scope | 5 | S01–S05 |
| Passed | 0 | Chưa có kết quả thực thi. |
| Failed | 0 | Chưa có kết quả thực thi. |
| Blocked | 0 | Chưa có trạng thái thực thi được xác nhận; một số TC có điều kiện có thể gây block. |
| Not Run | 5 | Trạng thái hiện tại trong các file TC. |
| Bug reports | 0 | Không có bug report trong scope. |

Ngoài 5 test case, scenario S06 — đăng nhập sau khi hết 30 giây khóa — vẫn là coverage gap ở mức analysis. Không có bằng chứng thực thi, actual result hoặc defect để đánh giá mức tuân thủ của hệ thống.

## 3. Requirement and scenario coverage

| Requirement ID | Scenario IDs | TC IDs | Execution status | Bug IDs | Coverage note |
|---|---|---|---|---|---|
| FR-02 — Đăng nhập thành công, trả/lưu/gửi JWT | S01, S04 | `TC_FR02_S01_LoginSuccess`, `TC_FR02_S04_LoginAfterPriorFailure` | Not Run | — | Design coverage có; chưa có execution evidence. Không assert điều hướng hoặc reset counter. |
| FR-02 — Email `type="email"` và HTML5 validation | S02 | `TC_FR02_S02_InvalidEmailFormat` | Not Run | — | Design coverage có; message và continuation sau validation là Missing information M8. |
| FR-02 — Mỗi lần đăng nhập sai tăng bộ đếm đúng 1 | S03, S04 | `TC_FR02_S03_LockAfterThreeFailures`, `TC_FR02_S04_LoginAfterPriorFailure` | Not Run | — | Design coverage có; cách thiết lập/quan sát counter là M3, phản hồi lần sai 1–2 là M4. |
| FR-02 — Khóa 30 giây từ lần sai liên tiếp thứ 3 | S03 | `TC_FR02_S03_LockAfterThreeFailures` | Not Run | — | Design coverage có; precondition counter = 0 chưa có cách thiết lập được đặc tả. |
| FR-02 — Thử đăng nhập trong thời gian khóa | S05 | `TC_FR02_S05_LoginWhileLocked` | Not Run | — | Partial design coverage; response và continuation là M5. |
| FR-02 — Hành vi sau khi hết 30 giây khóa | S06 | — | Blocked at design | — | Không có TC vì trạng thái/hành vi sau timeout là Missing information M2. |
| FR-02 — Lỗi không tiết lộ chi tiết nguyên nhân | S03 | `TC_FR02_S03_LockAfterThreeFailures` | Not Run | — | Chỉ assert nguyên tắc không tiết lộ; exact wording/status code không được đặc tả. |
| FR-22 — Kiểu trường Mật khẩu và vị trí thông báo lỗi | S01, S02, S03 | `TC_FR02_S01_LoginSuccess`, `TC_FR02_S02_InvalidEmailFormat`, `TC_FR02_S03_LockAfterThreeFailures` | Not Run | — | Supplemental coverage trong flow; required marker chưa assert do M9. |
| SEC-02 — JWT hợp lệ cho API bảo mật | S01, S04 | `TC_FR02_S01_LoginSuccess`, `TC_FR02_S04_LoginAfterPriorFailure` | Not Run | — | Kiểm tra header được thiết kế; endpoint/route cụ thể không có trong README. |

## 4. Test execution results

| TC ID | Scenario | Status | Actual result | Evidence | Related bug |
|---|---|---|---|---|---|
| `TC_FR02_S01_LoginSuccess` | S01 — Đăng nhập thành công | Not Run | Missing information | Missing information | — |
| `TC_FR02_S02_InvalidEmailFormat` | S02 — Email sai định dạng | Not Run | Missing information | Missing information | — |
| `TC_FR02_S03_LockAfterThreeFailures` | S03 — Khóa sau ba lần sai liên tiếp | Not Run | Missing information | Missing information | — |
| `TC_FR02_S04_LoginAfterPriorFailure` | S04 — Đăng nhập đúng sau một lần sai | Not Run | Missing information | Missing information | — |
| `TC_FR02_S05_LoginWhileLocked` | S05 — Thử đăng nhập trong thời gian khóa | Not Run | Missing information | Missing information | — |

## 5. Defect summary

| Bug ID | Related TC ID | Severity | Status | Summary |
|---|---|---|---|---|
| — | — | — | — | Chưa có test failed hoặc bug report do người dùng cung cấp. |

## 6. Coverage gaps, blocked tests, and limitations

- Chưa có trạng thái thực thi được người dùng xác nhận; 5 TC vẫn mang trạng thái thiết kế `Not Run`.
- S06 chưa có test case vì README không quy định trạng thái/hành vi sau khi hết 30 giây khóa (M2).
- M1: không rõ đăng nhập thành công có reset bộ đếm hay không.
- M3: không có cách đặc tả để thiết lập hoặc quan sát bộ đếm ban đầu; TC S03 và S04 có thể bị block khi thực thi.
- M4: không rõ phản hồi và continuation sau lần sai thứ 1–2.
- M5: không rõ response/message/continuation khi đăng nhập trong thời gian khóa.
- M6–M9: thiếu điều hướng thành công, exact error/status code, continuation của HTML5 validation và xác nhận required marker.
- Route/API cụ thể cho authenticated request không được README quy định; TC S01 và S04 chỉ có thể kiểm tra một request được hệ thống xác định là cần xác thực.
- Chưa có execution period, môi trường thực thi xác nhận, actual result, evidence hoặc bug report.

## 7. Conclusion and recommendation

Chưa đủ bằng chứng để đánh giá FR-02 là `Ready`, `Ready with known limitations` hay `Not ready`; README và người dùng cũng chưa cung cấp tiêu chí release readiness. Báo cáo vì vậy giữ trạng thái `Incomplete`.

Để hoàn tất báo cáo:

1. Thực thi hoặc xác nhận trạng thái của cả 5 TC và cung cấp actual result/evidence.
2. Xác định cách thiết lập/quan sát bộ đếm trước khi chạy S03–S05.
3. Làm rõ hành vi sau 30 giây để thiết kế và chạy TC cho S06.
4. Tạo bug report riêng cho mỗi TC failed trước khi cập nhật defect summary.

---

## Phụ lục A — Đánh giá feature ứng viên

---

### Use-Case Testing — Feature Candidates

## Source of truth

- Specification: `README.md` at workspace root
- System: EShop, specification version 2.0 (2026-05-14)
- Selection principle: prioritize observable actor–system flows with a success path and meaningful alternative/error paths.

## Recommended candidates

| Feature ID | Feature | Actor | End-to-end flow | Alternative/error flows | Suitability | Evidence | Missing information |
|---|---|---|---|---|---|---|---|
| FR-03 | Quên mật khẩu và đặt lại mật khẩu | Người dùng | Nhập email đã đăng ký → nhận OTP → nhập OTP và mật khẩu mới → đặt lại mật khẩu | Email không phù hợp với yêu cầu; OTP dùng cho email khác; mật khẩu yếu; xác nhận mật khẩu không khớp; quay lại đăng nhập | High | README quy định rõ quy trình 2 bước, dữ liệu ở từng bước, OTP gắn với email, điều kiện mật khẩu và Step Indicator. FR-01, FR-22 và SEC-07 là tham chiếu chéo. | Không nêu phản hồi khi email chưa đăng ký, OTP sai/hết hạn/đã dùng; không nêu điều hướng hoặc thông báo sau khi đặt lại thành công. |
| FR-08 | Thanh toán | Người dùng đã đăng nhập | Mở checkout với giỏ hàng → xem sản phẩm và tổng tiền hệ thống tính → tiến hành thanh toán → giỏ hàng được xóa | Người dùng chưa đăng nhập; client gửi `total_amount` bị chỉnh sửa; có thể áp dụng coupon theo FR-09 | High | README quy định actor phải đăng nhập, dữ liệu checkout, cách xác định tổng tiền ở UI/backend và success guarantee là xóa giỏ. FR-07, FR-09 và SEC-02 liên quan. | Không nêu điều kiện giỏ rỗng, thông tin giao hàng/phương thức thanh toán, thời điểm tạo đơn, thông báo và điều hướng thành công/thất bại. |
| FR-16 | Import sản phẩm từ CSV | Admin | Chọn/tải file CSV → hệ thống kiểm tra file và từng dòng → import toàn bộ → hiển thị báo cáo | Sai đuôi file; sai header; `name` rỗng; `price` không dương; lỗi một dòng làm rollback toàn bộ; trường chứa dấu phẩy có/không có quote hợp lệ | High | README quy định actor Admin, định dạng file, validation, nguyên tắc all-or-nothing và báo cáo cuối luồng. FR-12 là precondition phân quyền liên quan. | Không nêu giới hạn file, hành vi với file rỗng, category không tồn tại, dòng trùng, encoding, thông báo cụ thể và trạng thái khi header sai. |
| FR-02 | Đăng nhập và khóa tài khoản | Người dùng | Nhập email/mật khẩu → hệ thống xác thực → trả JWT → client lưu và gửi token cho yêu cầu xác thực | Sai thông tin làm tăng bộ đếm; sai liên tiếp từ lần 3 làm khóa 30 giây; thử đăng nhập khi đang khóa | High | README có actor, success result, error path theo lịch sử và trạng thái khóa. FR-22 và SEC-02 liên quan. | Không nêu reset bộ đếm sau đăng nhập đúng, hành vi chính xác sau 30 giây, kết quả với email không tồn tại và điều hướng sau đăng nhập. Do phụ thuộc trạng thái/lịch sử, State Transition Testing cũng đặc biệt phù hợp. |
| FR-07 | Quản lý giỏ hàng | Người dùng | Xem giỏ → thay đổi số lượng/xóa sản phẩm hoặc tiếp tục mua sắm → hệ thống cập nhật giỏ và tổng tiền | Thêm lại cùng sản phẩm; xác nhận trước khi xóa; giỏ hàng trống | Medium | README mô tả nhiều hành động của người dùng, phản hồi giỏ hàng và các trạng thái có thể quan sát. FR-06, FR-23 và FR-24 liên quan. | Không nêu hành vi khi giảm số lượng tại 1, lựa chọn/hành vi khi hủy dialog, cách tính lại tổng, persistence của giỏ và post-condition chung của use case. |
| FR-01 | Đăng ký tài khoản | Người dùng chưa có tài khoản | Nhập thông tin bắt buộc → hệ thống kiểm tra → tạo tài khoản → chuyển tới Đăng nhập | Email sai định dạng/trùng; mật khẩu yếu; xác nhận mật khẩu không khớp | Medium | README có actor, dữ liệu đầu vào, success destination và các đường từ chối. FR-22 áp dụng cho form. | Không nêu kết quả lưu dữ liệu khi thất bại, nội dung lỗi, việc giữ/xóa dữ liệu đã nhập và cách xử lý Họ Tên trống. Nhiều nhánh thiên về input validation nên UCT chỉ nên kiểm tra chúng trong flow đăng ký. |
| FR-19 | Admin quản lý người dùng | Admin | Mở danh sách người dùng → xem thông tin → chọn và xóa một người dùng khác | Không được xóa chính tài khoản Admin đang đăng nhập; danh sách không được lộ mật khẩu | Medium | README có actor, mục tiêu xem/xóa và một nhánh nghiệp vụ bị cấm. FR-12 và SEC-03 là precondition phân quyền liên quan. | Không nêu dialog xác nhận, xử lý user có dữ liệu liên quan, phản hồi sau xóa, hành vi khi user không tồn tại hoặc khi thao tác tự xóa bị từ chối. |

## Recommendation

Ưu tiên phân tích trước:

1. **FR-08 — Thanh toán:** luồng nghiệp vụ cốt lõi, có success guarantee rõ và nhánh bảo mật/backend quan trọng.
2. **FR-03 — Quên/đặt lại mật khẩu:** quy trình hai bước rõ, có nhiều alternative flow gắn với từng bước.
3. **FR-16 — Import sản phẩm từ CSV:** luồng Admin đầu-cuối với success/rollback rõ ràng.

FR-02 phù hợp nhưng có hành vi phụ thuộc lịch sử và thời gian, nên Use-Case Testing chỉ bao quát hành trình đăng nhập; State Transition Testing phù hợp hơn để phủ bộ đếm và khóa tài khoản.

## Not recommended as standalone Use-Case Testing features

| Feature ID | Reason |
|---|---|
| FR-05, FR-11, FR-13 | Chủ yếu là hiển thị, tìm kiếm hoặc tổng hợp dữ liệu; không có luồng nghiệp vụ đầu-cuối và alternative flow đủ rõ. |
| FR-09 | Các điều kiện coupon đứng riêng phù hợp hơn với Decision Table; chỉ nên đưa vào UCT như một subflow của Checkout. |
| FR-10, FR-18, phần hủy đơn của FR-20 | Trọng tâm là trạng thái và chuyển trạng thái; State Transition Testing phù hợp hơn. |
| FR-12 | Chủ yếu là kiểm soát quyền truy cập theo token/role, phù hợp kiểm thử authorization hoặc Decision Table hơn một use case độc lập. |
| FR-14, FR-15, FR-17 | Chủ yếu là CRUD và validation; README chưa mô tả đủ một flow nghiệp vụ liên tục cùng các kết quả/nhánh. |
| FR-20 | Là phạm vi chức năng Mobile tổng hợp, không phải một use case đơn lẻ. Nên chọn một feature con cụ thể. |
| FR-21–FR-24 | Là yêu cầu GUI xuyên suốt, dùng làm coverage bổ sung trong các use case thay vì feature UCT độc lập. |

## Review gate

Chưa tạo Use Case Overview, Basic Flow, Extensions, Scenarios hoặc test case.

Vui lòng xác nhận một hoặc nhiều feature cần phân tích ở Phase 2, ví dụ: `Confirm FR-08` hoặc `Confirm FR-03 và FR-16`.

---

## Phụ lục B — Phân tích use case đã duyệt

---

### FR-02 — Use Case Analysis: Đăng nhập và khóa tài khoản

## 1. Scope và nguồn requirement

| Item | Value |
|---|---|
| Feature ID | FR-02 |
| Feature | Đăng nhập và khóa tài khoản |
| Source of truth | `README.md`, EShop specification version 2.0 |
| Primary requirement | FR-02 |
| Related requirements | FR-22, SEC-02 |
| In scope | Đăng nhập thành công; đăng nhập sai; khóa sau các lần sai liên tiếp; sử dụng JWT sau đăng nhập |
| Out of scope | Cài đặt backend/frontend; nội dung thông báo cụ thể; cơ chế mã hóa/lưu mật khẩu; State Transition coverage đầy đủ |

### Explicit requirements

- Người dùng nhập Email và Mật khẩu.
- Mỗi lần đăng nhập sai làm bộ đếm tăng đúng 1.
- Từ 3 lần đăng nhập sai liên tiếp trở lên, tài khoản bị tạm khóa 30 giây.
- Khi khóa, hệ thống trả lỗi phù hợp và không để lộ chi tiết nguyên nhân.
- Đăng nhập thành công trả JWT; client lưu token và gửi token trong `Authorization: Bearer <token>` cho mọi yêu cầu cần xác thực.
- Trường Email dùng `type="email"` và HTML5 format validation.
- Theo FR-22, trường Mật khẩu dùng `type="password"`; trường nào được xác định là bắt buộc phải có `*`; thông báo lỗi nằm trên nút submit.
- Theo SEC-02, API bảo mật yêu cầu JWT hợp lệ.

### Assumptions requiring approval

| ID | Assumption | Reason |
|---|---|---|
| A1 | `Level` của use case là `User goal`. | README không phân loại level; đăng nhập là mục tiêu hoàn chỉnh của người dùng. |
| A2 | Basic Flow bắt đầu với tài khoản đã tồn tại, thông tin đăng nhập đúng và tài khoản không trong thời gian khóa. | Đây là điều kiện cần để thực hiện success scenario; README cung cấp tài khoản test nhưng không công bố trạng thái khóa hiện tại. |
| A3 | Nếu người dùng nhập đúng thông tin trước khi đạt ngưỡng khóa, hệ thống thực hiện Basic Flow; chưa giả định bộ đếm được reset. | FR-02 chỉ quy định khóa từ 3 lần sai liên tiếp, nhưng không mô tả rõ xử lý bộ đếm sau lần đăng nhập đúng. |

### Missing information

| ID | Missing information | Impact |
|---|---|---|
| M1 | Bộ đếm có reset sau đăng nhập thành công hay không và reset về giá trị nào. | Không thể khẳng định chuỗi sai → đúng → sai bắt đầu lại từ đầu. |
| M2 | Trạng thái/hành vi chính xác sau khi đủ 30 giây khóa. | Scenario đăng nhập sau timeout bị block. |
| M3 | Cách thiết lập hoặc quan sát giá trị bộ đếm trước khi test. | Test ngưỡng khóa khó tái lập độc lập và đáng tin cậy. |
| M4 | Phản hồi và bước tiếp theo sau lần đăng nhập sai thứ 1 hoặc 2. | Chỉ kiểm tra chắc chắn được việc tăng bộ đếm; continuation chưa xác định. |
| M5 | Hành vi khi gửi yêu cầu đăng nhập trong lúc tài khoản đang khóa. | Chưa xác định response, thông báo và continuation cho lần thử trong thời gian khóa. |
| M6 | Điều hướng hoặc giao diện đích sau đăng nhập thành công. | Expected result chỉ được dừng ở JWT và cách client sử dụng token. |
| M7 | Nội dung thông báo lỗi, status code và cách xử lý email không tồn tại so với mật khẩu sai. | Chỉ có thể yêu cầu không tiết lộ chi tiết trong trường hợp lỗi được FR-02 mô tả. |
| M8 | Hành vi tiếp theo khi HTML5 email validation thất bại. | Scenario email sai định dạng chỉ cover được thuộc tính/validation đã nêu, không thể khẳng định điều hướng hay message. |
| M9 | FR-02 không gọi rõ Email và Mật khẩu là “trường bắt buộc”, dù mô tả người dùng nhập cả hai. | Không khẳng định required marker `*` cho hai trường này nếu chưa có xác nhận. |

## 2. Use Case Overview

| Field | Value |
|---|---|
| Use Case Title | Đăng nhập và khóa tài khoản |
| Primary Actor | Người dùng |
| Level | `User goal` — Assumption A1 |
| Preconditions | Tài khoản đã tồn tại, thông tin đăng nhập đúng và tài khoản không bị khóa — Assumption A2. Với scenario lỗi, trạng thái bộ đếm ban đầu phải được thiết lập nhưng cách thiết lập là Missing information M3. |
| Minimal Guarantees | Sau mỗi lần đăng nhập sai, bộ đếm tăng đúng 1. Khi đạt từ 3 lần sai liên tiếp, tài khoản bị khóa 30 giây và hệ thống trả lỗi không tiết lộ chi tiết nguyên nhân. |
| Success Guarantees | Hệ thống trả JWT; client lưu token và gửi token qua `Authorization: Bearer <token>` trong các yêu cầu cần xác thực. README không nêu điều hướng sau thành công. |

## 3. Main Success Scenario / Basic Flow

1. **Người dùng** nhập Email và Mật khẩu.
2. **Hệ thống** xử lý yêu cầu đăng nhập với thông tin hợp lệ cho tài khoản không bị khóa.
3. **Hệ thống** trả về JWT Token khi đăng nhập thành công.
4. **Client** lưu JWT Token.
5. **Client** gửi JWT Token trong header `Authorization: Bearer <token>` với các yêu cầu cần xác thực.

> Step 2 chỉ mô tả success condition của FR-02; không giả định status code, nội dung response hoặc điều hướng.

## 4. Extensions / Alternative Flows

| Extension ID | Base step | Condition | System behavior | Continuation |
|---|---|---|---|---|
| 1a | 1 | Email sai định dạng HTML5. | Trường Email dùng `type="email"` và thực hiện HTML5 format validation. | `Missing information M8`: README không nêu message hoặc bước tiếp theo. |
| 2a | 2 | Thông tin đăng nhập sai và số lần sai liên tiếp sau lần này vẫn nhỏ hơn 3. | Hệ thống tăng bộ đếm đúng 1. | `Missing information M4`: README không nêu phản hồi hoặc bước tiếp theo. |
| 2b | 2 | Thông tin đăng nhập sai làm số lần sai liên tiếp đạt từ 3 trở lên. | Hệ thống tăng bộ đếm đúng 1, khóa tài khoản 30 giây và trả lỗi phù hợp mà không tiết lộ chi tiết nguyên nhân. | Dừng use case với lỗi. |
| 2c | 2 | Người dùng gửi yêu cầu đăng nhập khi tài khoản còn trong thời gian khóa 30 giây. | Tài khoản đang ở trạng thái tạm khóa; phản hồi cho yêu cầu mới không được README mô tả. | `Missing information M5`: chưa xác định tiếp tục, dừng hay quay lại bước nào. |
| 2d | 2 | Người dùng đăng nhập đúng sau 1–2 lần sai liên tiếp và chưa đạt ngưỡng khóa. | Theo Assumption A3, hệ thống tiếp tục success flow; hành vi reset bộ đếm chưa được quy định. | Tiếp tục tại bước 3 theo Assumption A3. |
| 2e | 2 | Đã đủ 30 giây kể từ khi tài khoản bị khóa. | `Missing information M2`: README không nêu trạng thái đích hoặc cách hệ thống xử lý yêu cầu tiếp theo. | `Missing information M2`: chưa xác định. |

## 5. Scenarios

| Scenario ID | Scenario name | Flow path | Test objective | Requirement coverage | Readiness |
|---|---|---|---|---|---|
| S01 | Đăng nhập thành công | `1-2-3-4-5` | Xác minh đăng nhập đúng trả JWT, client lưu và gửi token đúng header cho yêu cầu xác thực. | FR-02; SEC-02; Basic Flow 1–5 | Ready sau khi duyệt A1–A2 |
| S02 | Email sai định dạng | `1-1a` | Xác minh trường Email dùng `type="email"` và áp dụng HTML5 format validation trong flow đăng nhập. | FR-02; FR-22; Extension 1a | Partial — M8 chưa quy định phản hồi/continuation |
| S03 | Khóa sau ba lần đăng nhập sai liên tiếp | `1-2-2a-1-2-2a-1-2-2b` | Xác minh mỗi lần sai tăng đúng 1, tài khoản chỉ đạt ngưỡng khóa ở lần sai liên tiếp thứ 3, khóa 30 giây và lỗi không lộ nguyên nhân. | FR-02; FR-22; Extensions 2a, 2b | Partial — cần cách thiết lập/quan sát bộ đếm (M3) và phản hồi lần 1–2 (M4) |
| S04 | Đăng nhập đúng sau một lần sai | `1-2-2a-1-2-2d-3-4-5` | Xác minh người dùng vẫn có thể hoàn tất đăng nhập trước ngưỡng khóa; không khẳng định bộ đếm reset. | FR-02; Extensions 2a, 2d; Basic Flow 3–5 | Partial — phụ thuộc A3; reset counter là M1 |
| S05 | Thử đăng nhập trong thời gian khóa | `1-2-2c` | Xác minh tài khoản không thể hoàn tất success flow trong khoảng khóa 30 giây. | FR-02; Extension 2c | Partial — response và continuation là M5 |
| S06 | Đăng nhập sau khi hết 30 giây khóa | `1-2-2e` | Xác minh hành vi của hệ thống sau khi thời gian khóa kết thúc. | FR-02; Extension 2e | Blocked — trạng thái sau timeout là M2 |

### Scenario combination rationale

- S03 kết hợp hai lần đi qua 2a với 2b vì ngưỡng khóa chỉ có ý nghĩa sau chuỗi sai liên tiếp.
- S04 kết hợp error flow 2a với success flow để kiểm tra hành trình có thể phục hồi trước ngưỡng; không dùng scenario này để suy đoán reset counter.
- Không tổ hợp HTML5 validation với khóa tài khoản vì README không nói một email bị chặn bởi HTML5 được tính là lần đăng nhập sai.

## 6. Traceability

| Requirement | Use case step | Scenario ID | Planned TC ID | Status |
|---|---|---|---|---|
| FR-02 — Nhập Email và Mật khẩu | Basic 1 | S01, S03, S04, S05, S06 | `TC_FR02_S01_LoginSuccess`, `TC_FR02_S03_LockAfterThreeFailures`, `TC_FR02_S04_LoginAfterPriorFailure`, `TC_FR02_S05_LoginWhileLocked`, `TC_FR02_S06_LoginAfterTimeout` | Generated cho S01, S03–S05; S06 blocked |
| FR-02 — Email `type="email"`, HTML5 validation | Basic 1; 1a | S01, S02 | `TC_FR02_S01_LoginSuccess`, `TC_FR02_S02_InvalidEmailFormat` | Generated |
| FR-02 — Mỗi lần sai tăng đúng 1 | 2a, 2b | S03, S04 | `TC_FR02_S03_LockAfterThreeFailures`, `TC_FR02_S04_LoginAfterPriorFailure` | Generated; execution gaps M3, M4 remain |
| FR-02 — Khóa 30 giây từ 3 lần sai liên tiếp | 2b, 2c, 2e | S03, S05, S06 | `TC_FR02_S03_LockAfterThreeFailures`, `TC_FR02_S05_LoginWhileLocked`, `TC_FR02_S06_LoginAfterTimeout` | Generated cho S03, S05; S06 blocked by M2 |
| FR-02 — Lỗi phù hợp, không lộ nguyên nhân | 2b | S03 | `TC_FR02_S03_LockAfterThreeFailures` | Generated; exact message unspecified |
| FR-02 — JWT được trả và lưu | Basic 3–4 | S01, S04 | `TC_FR02_S01_LoginSuccess`, `TC_FR02_S04_LoginAfterPriorFailure` | Generated |
| FR-02; SEC-02 — Gửi JWT cho yêu cầu xác thực | Basic 5 | S01, S04 | `TC_FR02_S01_LoginSuccess`, `TC_FR02_S04_LoginAfterPriorFailure` | Generated |
| FR-22 — Password type và vị trí thông báo lỗi | Basic 1; 2b | S01, S03 | Các TC tương ứng của S01 và S03 | Generated as supplemental checks; required marker chưa assert do M9 |

## 7. Coverage và review questions

- Có 6 scenario: 1 Ready sau assumption approval, 4 Partial và 1 Blocked.
- Mọi extension khả thi đã được ánh xạ vào scenario; S06 chưa thể có expected result đáng tin cậy.
- Phase 3 đã tạo test case cho S01–S05. S06 không có test case file vì expected behavior sau 30 giây vẫn bị block bởi M2.

Vui lòng review và xác nhận:

1. Có chấp nhận Assumptions A1–A3 không?
2. Sau 30 giây, tài khoản có tự động trở lại trạng thái có thể đăng nhập không?
3. Đăng nhập thành công có reset số lần sai về 0 không?
4. Khi sai lần 1–2 hoặc thử trong lúc khóa, hệ thống phải phản hồi và kết thúc/tiếp tục như thế nào?

Chỉ sau khi analysis được xác nhận mới sinh test case chi tiết ở Phase 3.
