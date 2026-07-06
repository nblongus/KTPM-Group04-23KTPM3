---
name: use-case-testing
description: Thiết kế Use-Case Testing dựa trên đặc tả README của EShop, qua các cổng review bắt buộc, hợp nhất test case vào một file và ghi nhận phân tích, bug cùng kết quả trong một report. Dùng khi cần đề xuất feature có luồng người dùng đầu-cuối, phân tích actor/precondition/basic flow/extensions/scenarios, sinh test case theo scenario, ghi nhận lỗi sau khi thực thi test case, hoặc lập test report mà không bịa requirement hay kết quả thực thi.
---

# Use-Case Testing cho EShop

Áp dụng Use-Case Testing (UCT) cho các luồng nghiệp vụ của EShop. Làm đúng thứ tự ba phase thiết kế, dừng ở hai review gate, ghi nhận kết quả thực thi và kết thúc bằng báo cáo kiểm thử tổng hợp. Chỉ tạo bug report khi người dùng cung cấp kết quả thực thi failed; chỉ hoàn tất test report khi mọi test case trong scope có trạng thái được xác nhận.

## Quy tắc không được vi phạm

- Dùng `README.md` EShop do người dùng chỉ định làm nguồn requirement chính. Nếu chưa chỉ định file, tìm `README.md` ở root workspace và công bố file đã dùng.
- Đọc đủ các requirement và tham chiếu chéo liên quan đến feature; không chỉ đọc riêng một FR nếu flow phụ thuộc FR khác.
- Không đọc implementation để lấp khoảng trống của đặc tả, trừ khi người dùng đổi rõ nguồn sự thật.
- Không bịa actor, hành vi, điều hướng, thông báo, dữ liệu, API response, post-condition hoặc requirement ngoài README.
- Phân loại nội dung là `Explicit requirement`, `Assumption`, hoặc `Missing information`. Không biến assumption thành expected result bắt buộc.
- Nếu ảnh bài giảng và slide mâu thuẫn về **cấu trúc artifact**, ưu tiên ảnh bài giảng. Không dùng ảnh hoặc slide để ghi đè hành vi nghiệp vụ trong README nếu người dùng chưa cho phép.
- Tập trung vào hành trình actor–system và nhánh nghiệp vụ. Không biến UCT thành Equivalence Partitioning, Boundary Value Analysis hoặc Decision Table.
- Chỉ chọn feature có flow người dùng rõ từ đầu đến cuối. Ưu tiên feature có actor, precondition, main flow và alternative/error flow. Không chọn feature chỉ có validation input đơn giản mà thiếu luồng nghiệp vụ.
- Yêu cầu xác nhận rõ ràng sau Phase 1 và Phase 2. Việc người dùng yêu cầu chạy skill hoặc đã nêu tên feature không thay thế xác nhận tại gate.
- Hoàn thành artifact của phase hiện tại, nêu file đã tạo và câu hỏi còn thiếu, yêu cầu review, rồi kết thúc lượt. Không bắt đầu phase kế tiếp trong cùng lượt.
- Giữ output ngắn gọn, rõ ràng và dùng Markdown. Bảo toàn file của người dùng; chỉ cập nhật artifact thuộc UCT và feature đang làm.

## Cấu trúc output

Giữ đúng ba file Markdown trong thư mục phương pháp; giữ nguyên requirement ID và test-case ID ổn định trong nội dung.

```text
use-case-testing/
├── SKILL.md
├── report.md
└── test-cases.md
```

Dùng `report.md` cho danh sách ứng viên, analysis đã duyệt, bug và báo cáo cuối. Dùng `test-cases.md` cho test case chi tiết, mỗi test case là một mục H2. Không tạo thư mục artifact lồng nhau hoặc file Markdown bổ sung. Chuẩn hóa `FEATURE_ID` từ requirement ID bằng cách bỏ dấu gạch ngang, ví dụ `FR-08` thành `FR08`; dùng `S01`, `S02`, ... cho scenario.

## Phase 1 — Đọc đặc tả và đề xuất feature

1. Xác định và đọc README EShop, gồm các requirement được tham chiếu chéo.
2. Tìm feature có actor và flow nghiệp vụ đầu-cuối quan sát được.
3. Đánh giá mức phù hợp:
   - `High`: có actor, precondition, success flow và ít nhất một alternative/error flow rõ.
   - `Medium`: có flow nghiệp vụ nhưng một số precondition, nhánh hoặc kết quả còn thiếu.
   - `Low`: chủ yếu là validation đơn lẻ, hiển thị tĩnh hoặc quy tắc không tạo thành hành trình người dùng.
4. Tạo hoặc cập nhật phần feature candidates trong `use-case-testing/report.md` với bảng:

   | Feature ID | Feature | Actor | End-to-end flow | Alternative/error flows | Suitability | Evidence | Missing information |
   |---|---|---|---|---|---|---|---|

5. Chỉ đề xuất các feature `High` hoặc `Medium`; giải thích ngắn vì sao phù hợp. Nếu người dùng đã nêu feature, vẫn đánh giá feature đó.
6. Liệt kê feature không phù hợp đáng chú ý và lý do, nhất là validation đơn lẻ dễ bị nhầm với UCT.
7. Yêu cầu người dùng review và confirm chính xác feature hoặc tập feature cần phân tích.
8. Dừng. Không tạo Use Case Overview, flow, scenario hay test case.

## Phase 2 — Phân tích use case đã được xác nhận

Chỉ bắt đầu sau khi người dùng xác nhận Phase 1. Với mỗi feature được chọn, thêm phần use-case analysis vào `use-case-testing/report.md`, gồm các phần sau.

### 1. Scope và nguồn requirement

- Ghi feature ID, tên feature, file nguồn và các requirement ID liên quan.
- Tách rõ `Explicit requirements`, `Assumptions`, và `Missing information`.

### 2. Use Case Overview

Dùng đúng bảng hai cột:

| Field | Value |
|---|---|
| Use Case Title | ... |
| Primary Actor | ... |
| Level | ... |
| Preconditions | ... |
| Minimal Guarantees | ... |
| Success Guarantees | ... |

Chỉ điền điều được README hỗ trợ. Nếu `Level`, guarantee hoặc thông tin khác không được nêu hay suy ra chắc chắn, ghi `Missing information` hoặc assumption có nhãn.

### 3. Main Success Scenario / Basic Flow

- Đánh số `1`, `2`, `3`, ...
- Mỗi bước bắt đầu bằng actor rõ ràng, ví dụ `Người dùng ...` hoặc `Hệ thống ...`.
- Mô tả một luồng thành công từ trigger đến success guarantee.
- Không thêm màn hình, nút, xác nhận, thông báo hoặc xử lý backend không có trong README.

### 4. Extensions / Alternative Flows

Gắn mỗi extension vào đúng bước Basic Flow bằng ID `1a`, `2a`, `2b`, `3a`, ... Với mỗi extension, ghi đủ:

| Extension ID | Base step | Condition | System behavior | Continuation |
|---|---|---|---|---|

Trong `Continuation`, ghi rõ một trong các dạng: `Tiếp tục tại bước N`, `Quay lại bước N`, hoặc `Dừng use case`. Nếu README không quy định, ghi `Missing information`; không tự quyết định.

### 5. Scenarios

Tạo scenario từ Basic Flow, Basic Flow + một Alternative Flow, và tổ hợp Alternative Flows khi tổ hợp đó khả thi, có ý nghĩa nghiệp vụ và được đặc tả hỗ trợ.

| Scenario ID | Scenario name | Flow path | Test objective | Requirement coverage | Readiness |
|---|---|---|---|---|---|

- Dùng flow path dạng `1-2-3-4` hoặc `1-2-2a-3-4`.
- Dùng `Ready`, `Partial`, hoặc `Blocked` cho readiness; nêu lý do nếu không `Ready`.
- Không tạo tổ hợp vô lý, không thể đạt, hoặc chỉ nhằm vét tổ hợp.
- Đảm bảo mỗi extension khả thi xuất hiện trong ít nhất một scenario, hoặc nêu lý do chưa thể cover.

### 6. Traceability và review

- Lập mapping `Requirement ID → Basic/Extension step → Scenario ID → Planned TC ID`.
- Dùng planned TC ID theo mục dự kiến trong `test-cases.md` và giữ ID ổn định qua các lần sửa.
- Kiểm tra mọi flow và expected outcome đều truy vết được về README.
- Trình bày analysis, assumption, missing information và scenario bị block.
- Yêu cầu người dùng review và confirm analysis.
- Dừng. Không tạo file test case chi tiết.

## Phase 3 — Sinh test case từ analysis đã xác nhận

Chỉ bắt đầu sau khi người dùng xác nhận Phase 2.

1. Tạo ít nhất một test case cho mỗi scenario đã duyệt. Nếu scenario bị block do thiếu expected behavior, chỉ tạo khi người dùng chấp nhận assumption rõ ràng; nếu không, giữ trong danh sách blocked.
2. Tạo mỗi test case thành một mục H2 riêng trong `use-case-testing/test-cases.md`.
3. Đặt ID `TC_<FEATURE_ID>_<SCENARIO_ID>_<SHORT_NAME>`, ví dụ `TC_FR08_S01_CheckoutSuccess`. Dùng short name ngắn, PascalCase, chỉ gồm chữ và số.
4. Trong mỗi mục test case, ghi mỗi trường đúng một lần:

```markdown
# <TC ID> — <Short title>

| Field | Value |
|---|---|
| TC ID | ... |
| Feature ID | ... |
| Use Case Title | ... |
| Technique | Use-Case Testing |
| Scenario covered | ... |
| Preconditions | ... |
| Test data | ... |
| Expected result | ... |
| Post-condition | ... |
| Requirement coverage | ... |
| Status | Not Run |

## Test steps

| Step | Actor | Action | Expected result |
|---|---|---|---|
| 1 | ... | ... | ... |
```

5. Làm precondition có thể thiết lập và quan sát được. Đặt giá trị cụ thể ở `Test data`; không giấu dữ liệu quan trọng trong mô tả chung.
6. Giữ test steps nguyên tử, theo đúng flow path của scenario và ghi actor ở từng bước.
7. Chỉ dùng expected result và post-condition được README hỗ trợ. Gắn assumption đã được duyệt ngay tại trường liên quan.
8. Ghi requirement coverage bằng ID và bước use case, ví dụ `FR-08; Basic Flow 1–5`.
9. Audit: mỗi scenario đã duyệt có ít nhất một TC; mọi extension khả thi có coverage; TC ID, scenario ID, tiêu đề mục và traceability khớp nhau; tất cả status là `Not Run`.
10. Báo danh sách mục TC đã tạo, coverage gap và test case bị block. Không khẳng định test đã chạy.

## Ghi bug report sau khi thực thi

Khi người dùng báo test case failed:

1. Xác định TC ID và đọc test case tương ứng cùng requirement nguồn.
2. Dùng thông tin thực thi do người dùng cung cấp; không tự dựng actual result hoặc evidence.
3. Nếu thiếu dữ liệu tối thiểu để mô tả lỗi tái hiện được, yêu cầu bổ sung đúng phần thiếu. Có thể tạo draft và ghi `Missing information` nếu người dùng muốn.
4. Tạo mỗi lỗi thành một mục riêng trong phần defect của `use-case-testing/report.md`, dùng ID `BUG_<FEATURE_ID>_<NNN>_<SHORT_NAME>`; không ghi đè bug khác và giữ Bug ID ổn định.
5. Ghi đủ các trường:

```markdown
# <Bug ID> — <Short title>

| Field | Value |
|---|---|
| Bug ID | ... |
| Related TC ID | ... |
| Feature ID | ... |
| Requirement violated | ... |
| Expected result | ... |
| Actual result | ... |
| Severity | ... |
| Evidence | ... |
| Suggested fix | ... |
| Status | New |

## Steps to reproduce

1. ...
```

6. Suy ra severity từ tác động quan sát được và ghi ngắn lý do; nếu chưa đủ dữ liệu, ghi `TBD` thay vì đoán.
7. Ghi `Suggested fix` ở mức hướng điều tra hoặc hành vi cần khôi phục. Không khẳng định root cause nếu chưa có bằng chứng.
8. Liên kết requirement violated tới ID trong README và bảo đảm steps/expected result nhất quán với test case.

## Bước cuối — Viết báo cáo kiểm thử hoàn chỉnh

Chỉ bắt đầu sau khi người dùng cung cấp kết quả hoặc trạng thái thực thi của test case trong scope. Hoàn thiện `use-case-testing/report.md`. Report chỉ là `Complete` khi mọi test case trong scope có trạng thái được xác nhận, kể cả `Blocked` hoặc `Not Run`; nếu còn test case chưa có trạng thái, có thể tạo draft nhưng phải ghi rõ `Incomplete` và liệt kê dữ liệu còn thiếu. Không suy đoán trạng thái, actual result, evidence hoặc defect.

1. Đọc lại requirement nguồn, use-case analysis, toàn bộ test case trong scope, kết quả thực thi được cung cấp và các bug report liên quan.
2. Đối chiếu TC ID, scenario ID, requirement coverage, trạng thái thực thi và Bug ID. Mọi số liệu tổng hợp phải tính được từ artifact hoặc dữ liệu thực thi thực tế.
3. Tạo report gồm đúng các phần sau:

```markdown
# Use-Case Testing Report — <Feature ID>: <Feature name>

## 1. Report information

| Field | Value |
|---|---|
| Feature ID | ... |
| Technique | Use-Case Testing |
| Requirement source | ... |
| Test scope | ... |
| Execution period | ... |
| Test environment | ... |
| Report status | Complete / Incomplete |

## 2. Executive summary

...

## 3. Requirement and scenario coverage

| Requirement ID | Scenario IDs | TC IDs | Execution status | Bug IDs | Coverage note |
|---|---|---|---|---|---|

## 4. Test execution results

| TC ID | Scenario | Status | Actual result | Evidence | Related bug |
|---|---|---|---|---|---|

## 5. Defect summary

| Bug ID | Related TC ID | Severity | Status | Summary |
|---|---|---|---|---|

## 6. Coverage gaps, blocked tests, and limitations

...

## 7. Conclusion and recommendation

...
```

4. Trong `Executive summary`, nêu tổng số test case trong scope và số lượng theo từng trạng thái thực tế như `Passed`, `Failed`, `Blocked`, `Not Run`; không quy đổi `Not Run` thành `Passed` hoặc bỏ khỏi tổng số.
5. Trong `Requirement and scenario coverage`, thể hiện cả requirement/scenario chưa được thực thi hoặc chưa cover và nêu nguyên nhân. Không tuyên bố coverage đầy đủ nếu còn gap, scenario blocked hoặc traceability chưa khớp.
6. Trong `Test execution results`, chỉ ghi actual result và evidence do người dùng cung cấp. Nếu thiếu, ghi `Missing information`.
7. Trong `Defect summary`, chỉ liệt kê bug report đã tồn tại. Một test failed chưa có đủ dữ liệu tạo bug phải được nêu là defect gap, không tự sinh nội dung lỗi.
8. Trong `Conclusion and recommendation`, kết luận dựa trên kết quả và mức coverage quan sát được. Chỉ dùng kết luận `Ready`, `Ready with known limitations`, hoặc `Not ready` khi tiêu chí tương ứng đã được người dùng/requirement xác định; nếu chưa có tiêu chí, ghi rõ đây là đánh giá có điều kiện và nêu cơ sở.
9. Audit report: tổng số theo trạng thái khớp danh sách TC; mọi TC failed liên kết đúng Bug ID hoặc defect gap; mọi Bug ID trỏ về TC; bảng coverage khớp analysis; các liên kết mục tồn tại; report không chứa dữ liệu tự dựng.
10. Báo `report.md` đã cập nhật, trạng thái `Complete` hoặc `Incomplete`, và các thông tin còn thiếu. Đây là artifact cuối của quy trình UCT.

## Checklist kết thúc

- Chỉ dùng đúng ba file trong thư mục `use-case-testing/` và đúng phase.
- Không có requirement ngoài README hoặc nội dung không gắn nhãn.
- Basic Flow có actor ở từng bước; extension có condition, system behavior và continuation.
- Scenario có ID, name, flow path và test objective.
- Khi vừa sinh ở Phase 3, mỗi TC là một mục H2 trong `test-cases.md`, đủ trường, đúng ID và có `Status: Not Run`.
- Mỗi bug là một mục trong `report.md`, có related TC và evidence thực tế hoặc `Missing information`.
- Test report tổng hợp đúng scope, số liệu thực thi, coverage, defect và limitation; mọi kết luận đều có căn cứ.
- Đã dừng đúng review gate và chưa sinh artifact của phase sau.
