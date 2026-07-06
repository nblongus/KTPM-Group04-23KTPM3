---
name: decision-table-test-design
description: Phân tích requirement và thiết kế test bằng Decision Table theo pipeline xác định điều kiện/nguyên nhân/kết quả, lập bảng chân trị, rút gọn luật, chọn luật rủi ro để áp dụng pairwise, rồi sinh test case có truy vết. Dùng khi business rule có nhiều điều kiện hữu hạn kết hợp để quyết định một hoặc nhiều kết quả.
---

# Mục tiêu

Tạo bộ test dựa trên requirement, không dựa trên hành vi lỗi của implementation. Giữ truy vết từ điều kiện đến luật và test case. Không dùng pairwise thay thế các luật nghiệp vụ bắt buộc của Decision Table.

# Input cần có

- Requirement và acceptance criteria.
- Điểm vào UI/API, dữ liệu nền, role, trạng thái và side effect liên quan.
- Đặc tả API hoặc mã nguồn chỉ để làm rõ cách thực thi; khi mâu thuẫn, lấy requirement làm expected result và ghi nhận mâu thuẫn.
- Mức rủi ro nếu người dùng đã cung cấp; nếu chưa có, đánh giá theo tác động và khả năng xảy ra.

# Pipeline

## B1 — Lọc requirement và xác định điều kiện, nguyên nhân, kết quả

1. Liệt kê các requirement ứng viên.
2. Ưu tiên requirement có từ hai điều kiện hữu hạn trở lên, kết quả quan sát được và quy tắc kết hợp rõ (`AND`, `OR`, loại trừ, trạng thái, role).
3. Loại hoặc chuyển sang kỹ thuật khác nếu requirement chủ yếu là trình tự, giao diện tĩnh, hiệu năng hoặc miền giá trị độc lập. Gợi ý State Transition cho state machine và EP/BVA cho một biến đơn lẻ.
4. Chấm mỗi ứng viên theo thang 0–2 cho: số điều kiện kết hợp, độ rõ của kết quả, khả năng kiểm soát dữ liệu, tác động rủi ro. Ghi lý do chọn requirement cuối cùng.
5. Chuẩn hóa mỗi điều kiện thành một mệnh đề có thể nhận `T/F`. Nếu điều kiện có nhiều giá trị loại trừ nhau, dùng các giá trị rời rạc thay vì ép thành nhiều cờ Boolean gây tổ hợp bất khả thi.
6. Tách rõ:
   - `Cause/Condition`: input hoặc trạng thái làm thay đổi quyết định.
   - `Action/Result`: output, lỗi, phép tính, thay đổi dữ liệu hoặc điều hướng quan sát được.
7. Gắn nguồn requirement cho từng condition/action. Đánh dấu giả định và tổ hợp bất khả thi; không tự bịa thứ tự ưu tiên lỗi.

Xuất bảng sàng lọc requirement và bảng `ID | Condition/Cause | T | F | Nguồn`, tiếp theo là bảng `ID | Action/Result | Nguồn`.

## B2 — Lập bảng chân trị và Decision Table

1. Với `n` điều kiện Boolean độc lập, tạo đủ `2^n` tổ hợp. Nếu có ràng buộc, vẫn ghi tổ hợp rồi đánh dấu `Impossible`, hoặc loại kèm giải trình.
2. Xác định action cho từng tổ hợp chỉ từ requirement.
3. Tách bảng quyết định phụ khi một thuộc tính chỉ ảnh hưởng cách tính sau khi luật chính thành công, ví dụ loại giảm giá `percent/fixed`. Không làm phình bảng eligibility nếu thuộc tính đó không ảnh hưởng việc chấp nhận.
4. Kiểm tra mỗi tổ hợp khả thi có đúng một kết quả nghiệp vụ. Nếu nhiều luật cùng khớp, chỉ chấp nhận khi chúng dẫn đến cùng action hoặc requirement định nghĩa priority.

Xuất bảng chân trị với một dòng cho mỗi rule và bảng quyết định ở dạng condition/action.

## B3 — Rút gọn Decision Table

1. Gộp hai luật chỉ khi chúng có cùng action và chỉ khác giá trị của một condition; thay condition đó bằng `-` (don't care).
2. Lặp lại đến khi không thể gộp mà vẫn giữ nguyên hành vi.
3. Cho phép các luật rút gọn chồng lấp chỉ khi action hoàn toàn giống nhau. Không gán error message cụ thể cho các luật chồng lấp nếu requirement không định nghĩa ưu tiên lỗi.
4. Chứng minh tính tương đương:
   - Mọi tổ hợp khả thi của bảng đầy đủ được ít nhất một luật rút gọn bao phủ.
   - Không luật rút gọn nào bao phủ tổ hợp có action khác.
   - Luật thành công và thất bại không xung đột.
5. Lập ma trận `Rule đầy đủ → Rule rút gọn`; ghi số luật trước và sau khi rút gọn.

## B4 — Chọn vùng rủi ro, áp dụng pairwise và tạo test case

1. Chấm rủi ro từng luật theo `Risk = Impact (1–3) × Likelihood (1–3)`. Ưu tiên luật có tiền, bảo mật, quyền truy cập, mất dữ liệu hoặc nhiều nhánh tính toán.
2. Chọn các factor nằm bên trong luật rủi ro, chẳng hạn loại dữ liệu, giá trị biên hợp lệ, thời hạn gần/xa, trạng thái quota. Mọi giá trị factor phải vẫn thỏa condition cố định của luật đó.
3. Tạo covering array pairwise sao cho mọi cặp giá trị giữa hai factor xuất hiện ít nhất một lần. Tôn trọng constraint và kiểm tra coverage bằng ma trận cặp; không chỉ tuyên bố “đã pairwise”.
4. Giữ ít nhất một test cho mỗi luật rút gọn. Dùng các test pairwise để thay hoặc mở rộng test đại diện của luật rủi ro, không xóa test của luật khác.
5. Với mỗi test case, ghi:
   - Test Case ID, Rule ID, Technique.
   - Objective, Preconditions, Test data.
   - Steps có endpoint/UI cụ thể.
   - Expected result gồm trạng thái chấp nhận/từ chối, phép tính và side effect liên quan.
   - Actual result và Status là `Not executed` nếu chưa chạy.
6. Không khẳng định HTTP status hoặc nội dung message chính xác nếu requirement không quy định; dùng kỳ vọng có thể kiểm chứng như `4xx`, “thông báo phù hợp”, và “không áp dụng giảm giá”.

# Output bắt buộc

Trả kết quả theo thứ tự:

1. Nguồn đã dùng và phạm vi.
2. B1 — Sàng lọc requirement; condition/cause; action/result.
3. B2 — Bảng chân trị đầy đủ và bảng quyết định phụ nếu có.
4. B3 — Bảng rút gọn, giải thích phép gộp và kiểm tra tương đương.
5. Đánh giá rủi ro và mô hình pairwise.
6. Ma trận chứng minh pair coverage.
7. Bộ test case cuối cùng và traceability `Requirement → Condition → Rule → Test Case`.
8. Assumption, điểm chưa rõ và mâu thuẫn requirement–implementation.

# Checklist chất lượng

- [ ] Requirement được chọn thực sự có logic kết hợp.
- [ ] Condition là mệnh đề kiểm soát/quan sát được và không chứa action.
- [ ] Bảng đầy đủ có đủ tổ hợp khả thi.
- [ ] Don't-care không làm thay đổi action.
- [ ] Pairwise chỉ mở rộng luật rủi ro và mọi cặp đã được chứng minh bao phủ.
- [ ] Mỗi luật rút gọn có ít nhất một test.
- [ ] Biên có dấu `>=`, `>`, `<`, `<=` được dùng đúng như requirement.
- [ ] Expected result truy ngược được về requirement.
- [ ] Test chưa chạy không bị ghi là Pass/Fail.
