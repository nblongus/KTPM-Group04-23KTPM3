# State Transition Testing — Test Cases

---

<a id="stt-password-reset-i-001"></a>

## `STT-PASSWORD-RESET-I-001` — Attempt reset without an obtained token

### TC ID

`STT-PASSWORD-RESET-I-001`

### Feature

`1.3 / 1.4 — Password-reset lifecycle`

### Technique

`State Transition Testing — Invalid Transition`

### Precondition

The API is available at `http://localhost:3000`. Start a new, isolated API-client execution record and do not call `POST /api/forgot-password` or import a previously returned token for `test@domain.com`; this observably establishes S0 without asserting that the server stores no token.

### Steps

1. Prepare a `POST /api/reset-password` request using the specified token, which was not returned by §1.3 in this execution.
2. Send the request with the specified email, token, and new password.
3. Record the HTTP status and response without asserting undocumented rejection behavior.

### Test Data

| Field | Value |
|---|---|
| Base URL | `http://localhost:3000` |
| Email | `test@domain.com` |
| Token not obtained through §1.3 | `000000` |
| New password | `NewPassword123!` |
| Request body | `{"email":"test@domain.com","resetToken":"000000","newPassword":"NewPassword123!"}` |

### Expected Result

**Blocked pending specification clarification.** §§1.3–1.4 do not state whether `000000` must be rejected, which HTTP status or body would indicate rejection, whether the password changes, or which state follows the request. Therefore the destination remains `Unspecified`, and this case must not be treated as pass/fail until a requirement-backed expected result is supplied.

### Covered Transition

`T03: S0 --submit reset request with a token not obtained through §1.3--> Unspecified`

---

<a id="stt-password-reset-v-001"></a>

## `STT-PASSWORD-RESET-V-001` — Request and receive a reset token

### TC ID

`STT-PASSWORD-RESET-V-001`

### Feature

`1.3 / 1.4 — Password-reset lifecycle`

### Technique

`State Transition Testing — Valid Transition`

### Precondition

The API is available at `http://localhost:3000`. Start a new, isolated API-client execution record in which no `POST /api/forgot-password` response or reset token has been captured for `test@domain.com`; this observably establishes S0 without assuming hidden server data.

### Steps

1. Send `POST /api/forgot-password` with the specified JSON body.
2. Record the HTTP status and JSON response.
3. Read the `message` and `resetToken` fields from the response.

### Test Data

| Field | Value |
|---|---|
| Base URL | `http://localhost:3000` |
| Email | `test@domain.com` |
| Request body | `{"email":"test@domain.com"}` |
| Documented reset token | `123456` |

### Expected Result

Per §1.3, the response is `200 OK` and contains the documented message indicating that a password-reset code was created plus `resetToken: "123456"`. The observed workflow reaches S1 because a concrete reset token has been returned.

### Covered Transition

`T01: S0 --request reset token and receive the documented successful response--> S1`

---

<a id="stt-password-reset-v-002"></a>

## `STT-PASSWORD-RESET-V-002` — Execute the token-to-reset flow

### TC ID

`STT-PASSWORD-RESET-V-002`

### Feature

`1.3 / 1.4 — Password-reset lifecycle`

### Technique

`State Transition Testing — Valid Transition`

### Precondition

The API is available at `http://localhost:3000`. Start a new, isolated API-client execution record in which no `POST /api/forgot-password` response or reset token has been captured for `test@domain.com`; this observably establishes S0 without assuming hidden server data.

### Steps

1. Send `POST /api/forgot-password` with the specified email.
2. Record the HTTP status and JSON response.
3. Capture the returned `resetToken` and establish S1.
4. Send `POST /api/reset-password` with the same email, the captured token, and the specified new password.
5. Record the HTTP status and response without asserting undocumented values.

### Test Data

| Field | Value |
|---|---|
| Base URL | `http://localhost:3000` |
| Email | `test@domain.com` |
| Forgot-password body | `{"email":"test@domain.com"}` |
| Documented returned token | `123456` |
| New password | `NewPassword123!` |
| Reset-password body | `{"email":"test@domain.com","resetToken":"123456","newPassword":"NewPassword123!"}` |

### Expected Result

Partially executable: per §1.3, the first request returns `200 OK`, the documented creation message, and `resetToken: "123456"`, covering T01 and reaching S1. **Blocked for T02:** §1.4 specifies the request fields but no success status, response body, or observable method for proving that S2 was reached. No expected reset response, login effect, or session effect may be asserted until the specification is clarified.

### Covered Transition

`T01: S0 --request reset token and receive the documented successful response--> S1; T02: S1 --submit returned token and new password--> S2 (blocked: S2 is not observably specified)`
