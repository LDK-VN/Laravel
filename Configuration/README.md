# Configuration

## Enviroment Configuration (Cấu hình biến môi trường)

Các thao tác về cấu hình môi trường -> file **.env** và các file ở thư mục config.

## Retrieving Enviroment Configuration (Truy xuất cấu hình môi trường)

Tất cả các biến sẽ được loaded vào $_ENV PHP super-global khi ứng dụng nhận được yêu cầu

Sử dụng **env** method -> truy xuất giá trị từ các biến trong file configuration.

```php
'debug' => env('APP_DEBUG', false),
```

* Tham số đầu tiến: tên cấu hình environment
* THam số thứ 2: giá trị mặc định 

## Determining The Current Enviroment (Xác định môi trường hiện tại)

Sử dụng **environment** method từ **App** facade:

```php
$enviroment = App:enviroment();
```

Kiểm tra môi trường hiện tại

```php
if (App:environment('local')) {
    // This is local enviroment
}

if (App:enviroment(['local', 'staging'])) {
    // The environment is either local OR staging ...
}
```

## Hiding Environment Variables From Debug Pages (Ẩn cac biến môi trường từ trang debug)

Khi có ngoại lệ chưa bị bắt và **APP_DEBUG** là true -> page hiển thị all biến môi trường và nội dung của chúng

Để ẩn đi một số biến nhất định -> sử dụng **debug_hide** trong file config/app.php

Một số biến có sẵn trong environment và request data -> cần ẩn $_ENV và $_SERVER

```php
return [

    // ...

    'debug_hide' => [
        '_ENV' => [
            'APP_KEY',
            'DB_PASSWORD',
        ],

        '_SERVER' => [
            'APP_KEY',
            'DB_PASSWORD',
        ],

        '_POST' => [
            'password',
        ],
    ],
];
```

## Accessing Configuration Values (Truy cập giá trị cấu hình)

Thông qua hàm **config()**

```php
$value = config('app.timezone'); // Lấy giá trị cấu hình timezone

// Truy xuất giá trị mặc định nếu giá trị cấu hình không tồn tại
$value = config('app.timezone', 'Asia/Seoul'); // 
```

Thay đổi giá trị cấu hình

```php
config(['app.timezone' => 'Asia/Ho_Chi_Minh']);
```

Chú thích : `app.timezone` là tham số trỏ đến config **timezone** ở file **config/app.php**

## Configuration Caching

Cho phép cache những cấu hình đã thiết lập lại

```bash
php artisan config:cache
```

Khi thực hiện lệnh này -> thay đổi file **.env** -> cấu hình vẫn giữ nguyên. Dùng khi chuẩn bị deploy dự án

Nếu muốn thay đổi

```bash
php artisan cache:clear
```

## Maintenance mode (Chế độ bảo trì)

Đôi khi hệ thống cũng cần được bảo trì -> run sẽ trả về page 503
```bash
php artisan down
```

Thêm thông báo và thời gian quay trờ lại hệ thống
```bash
php artisan down --message"Maintenancing..." --retry=3600
```

Trong lúc bảo trì có thể cho phép một số địa chỉ IP cụ thể truy cập được vào hệ thống
```bash
php artisan down --allow=127.0.0.1 --allow=192.168.0.0/1
```

Sử dụng **secret** để truy cập vào hệ thống đang bảo trì
```bash
php artisan down --secret="1630542a-246b-4b66-afa1-dd72a4c43515"
```
Tiếp theo điều hướng tối URL khới với mã thông báo -> đưa ra cookie bỏ qua chế độ bảo trì cho trình duyệt
```
https://example.com/1630542a-246b-4b66-afa1-dd72a4c43515
```

Chuyển hướng khi bảo trì
```bash
php artisan down --redirect=/
```

Bảo trì hoàn tất
```bash
php artisan up
```




