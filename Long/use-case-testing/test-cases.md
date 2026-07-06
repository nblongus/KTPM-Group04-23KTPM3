# Use-Case Testing — Test Cases

---

## TC_FR02_S01_LoginSuccess — Đăng nhập thành công

| Field | Value |
|---|---|
| TC ID | TC_FR02_S01_LoginSuccess |
| Feature ID | FR-02 |
| Use Case Title | Đăng nhập và khóa tài khoản |
| Technique | Use-Case Testing |
| Scenario covered | S01 — Đăng nhập thành công; flow `1-2-3-4-5` |
| Preconditions | Frontend Web và Backend API đang hoạt động. Tài khoản `test@eshop.com` tồn tại và không trong thời gian khóa theo Assumption A2 đã duyệt. Có thể quan sát response, client storage và network request bằng công cụ trình duyệt. |
| Test data | Frontend: `http://localhost:5173`<br>Email: `test@eshop.com`<br>Mật khẩu: `Test1234!`<br>Authenticated action: mở chức năng Lịch sử đơn hàng của user theo FR-11; route/API cụ thể là `Missing information` trong README. |
| Expected result | Đăng nhập thành công trả về JWT; client lưu JWT; khi thực hiện authenticated action, client gửi chính token đó trong header `Authorization: Bearer <token>`. README không quy định trang điều hướng sau đăng nhập. |
| Post-condition | JWT được lưu phía client và được dùng cho yêu cầu cần xác thực. Không khẳng định trạng thái bộ đếm đăng nhập sai. |
| Requirement coverage | FR-02 — Basic Flow 1–5; FR-22 — kiểu trường Email/Mật khẩu; SEC-02 |
| Status | Not Run |

### Test steps

| Step | Actor | Action | Expected result |
|---|---|---|---|
| 1 | Người dùng | Mở giao diện đăng nhập của Frontend Web. | Giao diện có trường Email dùng `type="email"` và trường Mật khẩu dùng `type="password"`. |
| 2 | Người dùng | Nhập Email `test@eshop.com` và Mật khẩu `Test1234!`. | Dữ liệu đăng nhập đã được nhập; không khẳng định required marker vì README không gọi rõ hai trường là bắt buộc. |
| 3 | Người dùng | Gửi yêu cầu đăng nhập. | Hệ thống xử lý đăng nhập cho tài khoản không bị khóa. |
| 4 | Hệ thống | Hoàn tất đăng nhập. | Response chứa JWT Token. Không assert status code, message hoặc điều hướng vì README không quy định. |
| 5 | Client | Lưu token nhận được. | JWT tồn tại trong client storage; loại storage cụ thể không được README quy định. |
| 6 | Người dùng | Mở chức năng Lịch sử đơn hàng và quan sát request cần xác thực. | Request gửi header `Authorization: Bearer <token>` với token trùng token nhận ở bước 4. |

---

## TC_FR02_S02_InvalidEmailFormat — Email sai định dạng

| Field | Value |
|---|---|
| TC ID | TC_FR02_S02_InvalidEmailFormat |
| Feature ID | FR-02 |
| Use Case Title | Đăng nhập và khóa tài khoản |
| Technique | Use-Case Testing |
| Scenario covered | S02 — Email sai định dạng; flow `1-1a` |
| Preconditions | Frontend Web đang hoạt động và giao diện đăng nhập có thể truy cập. |
| Test data | Frontend: `http://localhost:5173`<br>Email: `invalid-email`<br>Mật khẩu: `Test1234!` |
| Expected result | Trường Email dùng `type="email"` và HTML5 format validation nhận diện `invalid-email` là không hợp lệ. Nội dung message và continuation sau validation là `Missing information M8`, nên không assert. |
| Post-condition | `Missing information M8`: README không quy định dữ liệu được giữ lại, request có được gửi hay trạng thái giao diện sau validation. |
| Requirement coverage | FR-02 — Extension 1a; FR-22 — kiểu trường Email/Mật khẩu |
| Status | Not Run |

### Test steps

| Step | Actor | Action | Expected result |
|---|---|---|---|
| 1 | Người dùng | Mở giao diện đăng nhập. | Trường Email có `type="email"`; trường Mật khẩu có `type="password"`. |
| 2 | Người dùng | Nhập Email `invalid-email` và Mật khẩu `Test1234!`. | Dữ liệu được nhập vào các trường tương ứng. |
| 3 | Người dùng | Thực hiện gửi form đăng nhập. | HTML5 format validation xác định Email không hợp lệ. Không assert wording, điều hướng hoặc continuation. |

---

## TC_FR02_S03_LockAfterThreeFailures — Khóa sau ba lần đăng nhập sai

| Field | Value |
|---|---|
| TC ID | TC_FR02_S03_LockAfterThreeFailures |
| Feature ID | FR-02 |
| Use Case Title | Đăng nhập và khóa tài khoản |
| Technique | Use-Case Testing |
| Scenario covered | S03 — Khóa sau ba lần đăng nhập sai liên tiếp; flow `1-2-2a-1-2-2a-1-2-2b` |
| Preconditions | Frontend Web và Backend API đang hoạt động. Tài khoản `test@eshop.com` tồn tại, không bị khóa và có bộ đếm đăng nhập sai bằng 0. Cách thiết lập/quan sát bộ đếm là `Missing information M3`; nếu không chứng minh được precondition này, đánh dấu test `Blocked` khi thực thi. |
| Test data | Frontend: `http://localhost:5173`<br>Email: `test@eshop.com`<br>Mật khẩu sai dùng cho cả 3 lần: `Wrong123!`<br>Khoảng cách giữa các lần thử: thực hiện liên tiếp, không chèn lần đăng nhập đúng. |
| Expected result | Mỗi lần sai tăng bộ đếm đúng 1. Sau lần sai thứ 3 liên tiếp, tài khoản bị khóa 30 giây và hệ thống hiển thị lỗi phù hợp phía trên nút submit, không tiết lộ chi tiết nguyên nhân. Phản hồi cụ thể sau lần 1–2 là `Missing information M4`. |
| Post-condition | Tài khoản ở trạng thái tạm khóa trong 30 giây kể từ khi đạt ngưỡng. Bộ đếm cụ thể sau khóa ngoài ba lần tăng không được README mô tả. |
| Requirement coverage | FR-02 — Extensions 2a, 2b; FR-22 — vị trí thông báo lỗi |
| Status | Not Run |

### Test steps

| Step | Actor | Action | Expected result |
|---|---|---|---|
| 1 | Người dùng | Nhập `test@eshop.com` và `Wrong123!`, rồi gửi yêu cầu đăng nhập lần 1. | Đăng nhập sai; bộ đếm tăng từ 0 lên 1. Phản hồi/continuation cụ thể không được assert do M4. |
| 2 | Người dùng | Nếu hệ thống cho phép thử lại, nhập cùng dữ liệu và gửi yêu cầu lần 2. | Đăng nhập sai; bộ đếm tăng từ 1 lên 2. Tài khoản chưa đạt ngưỡng 3. Phản hồi cụ thể không được assert do M4. |
| 3 | Người dùng | Nếu hệ thống cho phép thử lại, nhập cùng dữ liệu và gửi yêu cầu lần 3. | Đăng nhập sai; bộ đếm tăng từ 2 lên 3 và tài khoản bị khóa 30 giây. |
| 4 | Hệ thống | Trả phản hồi lỗi cho lần thứ 3. | Lỗi phù hợp, không tiết lộ chi tiết nguyên nhân và xuất hiện phía trên nút submit. Exact wording/status code không được assert. |

---

## TC_FR02_S04_LoginAfterPriorFailure — Đăng nhập đúng sau một lần sai

| Field | Value |
|---|---|
| TC ID | TC_FR02_S04_LoginAfterPriorFailure |
| Feature ID | FR-02 |
| Use Case Title | Đăng nhập và khóa tài khoản |
| Technique | Use-Case Testing |
| Scenario covered | S04 — Đăng nhập đúng sau một lần sai; flow `1-2-2a-1-2-2d-3-4-5` |
| Preconditions | Frontend Web và Backend API đang hoạt động. Tài khoản `test@eshop.com` tồn tại, không bị khóa và có bộ đếm sai bằng 0. Cách thiết lập/quan sát bộ đếm là `Missing information M3`; nếu không chứng minh được, đánh dấu test `Blocked` khi thực thi. Assumption A3 đã được duyệt khi chuyển sang Phase 3. |
| Test data | Frontend: `http://localhost:5173`<br>Email: `test@eshop.com`<br>Mật khẩu sai lần 1: `Wrong123!`<br>Mật khẩu đúng lần 2: `Test1234!`<br>Authenticated action: mở Lịch sử đơn hàng theo FR-11. |
| Expected result | Lần sai làm bộ đếm tăng đúng 1. Nếu có thể thử lại, lần đăng nhập đúng trước ngưỡng khóa trả JWT; client lưu và gửi token cho yêu cầu xác thực. Không assert việc reset bộ đếm vì đó là `Missing information M1`. |
| Post-condition | JWT được lưu phía client. Giá trị bộ đếm sau đăng nhập thành công là `Missing information M1`. |
| Requirement coverage | FR-02 — Extensions 2a, 2d và Basic Flow 3–5; SEC-02 |
| Status | Not Run |

### Test steps

| Step | Actor | Action | Expected result |
|---|---|---|---|
| 1 | Người dùng | Nhập `test@eshop.com` và `Wrong123!`, rồi gửi đăng nhập. | Đăng nhập sai; bộ đếm tăng từ 0 lên 1. Phản hồi/continuation cụ thể là M4. |
| 2 | Người dùng | Nếu hệ thống cho phép thử lại, nhập `test@eshop.com` và `Test1234!`, rồi gửi đăng nhập. | Theo Assumption A3, đăng nhập thành công và hệ thống trả JWT. Nếu không thể thử lại, ghi nhận test `Blocked` do M4. |
| 3 | Client | Lưu JWT nhận được. | JWT được lưu phía client; không assert loại storage. |
| 4 | Người dùng | Mở chức năng Lịch sử đơn hàng và quan sát request cần xác thực. | Client gửi header `Authorization: Bearer <token>` với token đã nhận. |
| 5 | Người kiểm thử | Kiểm tra hậu điều kiện liên quan bộ đếm. | Không đưa ra kết luận reset/không reset vì README không quy định M1. |

---

## TC_FR02_S05_LoginWhileLocked — Thử đăng nhập trong thời gian khóa

| Field | Value |
|---|---|
| TC ID | TC_FR02_S05_LoginWhileLocked |
| Feature ID | FR-02 |
| Use Case Title | Đăng nhập và khóa tài khoản |
| Technique | Use-Case Testing |
| Scenario covered | S05 — Thử đăng nhập trong thời gian khóa; flow `1-2-2c` |
| Preconditions | Frontend Web và Backend API đang hoạt động. Tài khoản `test@eshop.com` vừa bị khóa bởi 3 lần đăng nhập sai liên tiếp theo TC_FR02_S03_LockAfterThreeFailures; lần thử trong TC này bắt đầu trước khi đủ 30 giây. Nếu không thiết lập/quan sát được trạng thái khóa, đánh dấu test `Blocked` do M3. |
| Test data | Frontend: `http://localhost:5173`<br>Email: `test@eshop.com`<br>Mật khẩu đúng: `Test1234!`<br>Thời điểm thử: trong vòng 30 giây kể từ khi tài khoản đạt ngưỡng khóa. |
| Expected result | Tài khoản vẫn trong thời gian tạm khóa và không hoàn tất success flow đăng nhập. Response, message và continuation cụ thể là `Missing information M5`, nên không assert. |
| Post-condition | Tài khoản vẫn thuộc khoảng khóa 30 giây. Hành vi sau khi đủ 30 giây là `Missing information M2`. |
| Requirement coverage | FR-02 — Extension 2c |
| Status | Not Run |

### Test steps

| Step | Actor | Action | Expected result |
|---|---|---|---|
| 1 | Người kiểm thử | Xác nhận tài khoản vừa đạt 3 lần sai liên tiếp và chưa hết 30 giây khóa. | Precondition khóa đang có hiệu lực; nếu không quan sát được, test bị Blocked. |
| 2 | Người dùng | Trong thời gian khóa, nhập `test@eshop.com` và mật khẩu đúng `Test1234!`, rồi gửi đăng nhập. | Tài khoản không hoàn tất đăng nhập thành công trong thời gian tạm khóa. |
| 3 | Hệ thống | Xử lý yêu cầu trong lúc khóa. | Không assert response, message, status code hoặc continuation do M5. |
