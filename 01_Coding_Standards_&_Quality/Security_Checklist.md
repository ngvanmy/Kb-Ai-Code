1. Authentication & Authorization
    | ID      | Quy tắc Bắt buộc                           | Chi tiết Kỹ thuật                                                                                                                                                 |
    |----------|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | SEC001   | [Bắt buộc] Mọi Endpoint đều phải được bảo vệ. | Sử dụng các thuộc tính `[Authorize]` hoặc `[AllowAnonymous]` một cách rõ ràng trên tất cả các Action Method.                                                    |
    | SEC002   | [Bắt buộc] Kiểm tra quyền (Authorization). | Luôn kiểm tra quyền truy cập dựa trên vai trò (`[Authorize(Roles = "Admin, Manager")]`) hoặc chính sách (Policies) được định nghĩa.                             |
    | SEC003   | [Bắt buộc] Kiểm tra Quyền sở hữu Dữ liệu (IDOR). | Luôn xác minh rằng `User.Identity.Name` (hoặc Claims ID) của người dùng hiện tại khớp với ID sở hữu tài nguyên đang được truy cập.                              |
    | SEC004   | [Nghiêm cấm] Lưu trữ mật khẩu dưới dạng văn bản thuần. | Mật khẩu phải luôn được băm (Hash) bằng thuật toán hiện đại (**PBKDF2**, **Argon2** hoặc **Bcrypt**). Không sử dụng **MD5**, **SHA1**, **SHA256** để băm mật khẩu. |

2. Injection Prevention
    ID	Quy tắc Bắt buộc	Chi tiết Kỹ thuật
    SEC005	[Bắt buộc] Ngăn chặn SQL Injection.	Luôn sử dụng Tham số hóa truy vấn (Parameterized Queries). Nếu dùng Entity Framework Core, đảm bảo không sử dụng FromSqlRaw() hoặc ExecuteSqlRaw() với input từ người dùng.
    SEC006	[Bắt buộc] Ngăn chặn Command Injection.	Không sử dụng các hàm gọi shell (Process.Start, CMD) với dữ liệu đầu vào không được lọc (unvalidated input) từ người dùng.
    SEC007	[Bắt buộc] Ngăn chặn XSS.	Đối với mã nguồn Blazor/Razor, luôn sử dụng Output Encoding (Mã hóa đầu ra). Tránh sử dụng <text> hoặc MarkupString với dữ liệu từ người dùng.                                                                        |
3. Data Handling & Exceptions
    |ID	|Quy tắc Bắt buộc	|Chi tiết Kỹ thuật
    SEC008	[Bắt buộc] Xử lý ngoại lệ an toàn.	Tránh trả về các thông báo lỗi hoặc thông tin stack trace chi tiết ra phía Client (Client-facing). Luôn log lỗi chi tiết ở phía Server và trả về thông báo lỗi chung chung (500 Internal Server Error).
    SEC009	[Bắt buộc] Kiểm tra tính hợp lệ của Input.	Luôn sử dụng Data Annotations ([Required], [Range], [EmailAddress]) và kiểm tra ModelState.IsValid ở phía Server (Server-side validation) cho tất cả các request POST/PUT.
    SEC010	[Bắt buộc] Xử lý Session/Token.	Đảm bảo token JWT được cấu hình với thời gian hết hạn (Expiration Time) ngắn (ví dụ: 15-30 phút) và sử dụng Refresh Token để gia hạn.
4. Logging
    | ID      | Quy tắc Bắt buộc                           | Chi tiết Kỹ thuật                                                                                                                                                 |
    |----------|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | SEC005   | [Bắt buộc] Logging toàn diện.             | Luôn sử dụng logging để ghi lại tất cả các hoạt động quan trọng, bao gồm cả các lỗi nghiêm trọng.                                                               |
    | SEC006   | [Bắt buộc] Không ghi log mật khẩu.        | Không bao giờ ghi log mật khẩu hoặc thông tin xác thực khác.                                                                                                     |