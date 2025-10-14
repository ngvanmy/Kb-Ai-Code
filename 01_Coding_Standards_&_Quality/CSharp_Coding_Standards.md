# Tiêu chuẩn Code C# cho Dự án

## 1. Quy ước Đặt tên (Naming)

| Thành phần | Quy tắc Bắt buộc | Ví dụ Đúng |
|---|---|---|
| Class, Method | PascalCase | OrderProcessor, CalculateTotal() |
| Private Field | _camelCase | private readonly ILogger _logger; |
| Tham số | camelCase | Process(int orderId) |
| Interface | Bắt đầu bằng 'I' (PascalCase) | IDataRepository |

## 2. Quy tắc Ngôn ngữ

-   **KHÔNG** sử dụng `string.Format()`. Luôn sử dụng **String Interpolation** (`$"{variable}"`).
-   **KHÔNG** sử dụng `catch (Exception)`. Phải bắt ngoại lệ cụ thể, ngoại trừ logging và re-throw.
-   **Tất cả** public members phải có **XML Doc Comments** (`///`).

## 3. Quy tắc Chất lượng (Maintainability)

-   Mỗi phương thức không được vượt quá **50 dòng** code.
-   Sử dụng **var** khi kiểu dữ liệu rõ ràng.