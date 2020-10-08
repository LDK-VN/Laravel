# Intro

## Public Directory:

Chứa file **index.php** -> cổng -> cho phép tất cả request vào project. Ngoài ra còn chứa một số tài nguyên như ảnh, Javascript và CSS.

## Configurations Files

Tất cả file cấu hình được lưu trong thư mục **config**

## Directory permissions (Quyền thư mục)

Sau khi cài laravel, cần phải configure một số quyền. Cac thư mục **storage** và **bootstrap/cache** phải được ghi bời web server

## Application key

Tạo key cho application (trong file .env)

```bash
php artisan key:generate
```
Nhằm bảo mật cho phiên người dùng và các dữ liệu được mã khoá 

## Additional Configuration (Cấu hình bổ sung)

Có thể thêm một số file cấu hình cần thiết như:
* Cache
* Database
* Session

# Web server configuration

## Directory Configuration

Laravel phải luông được cung cấp từ thư mục root (web directory) được định cấu hình cho máy chủ web.
Không nên cố thay đổi -> Nó sẽ làm lộ các tệp nhạy cảm.

## Pretty URLs (URL đẹp)

### Apache

Sử dụng `public/.htaccess` -> Cung cấp URL không có controller phía trước path

 Tập tin dùng để cấu hình máy chủ web apache. Cho phép điều hướng và enable các tính năng linh hoạt hoặc bảo vệ một phần nào đó của website

### Nginx

