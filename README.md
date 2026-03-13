# NT208
## Các lỗi syntax

**1.** Ở đường dẫn ```http://localhost:8000/?page=settings```, nhận được báo lỗi parse như sau: ```Parse error: syntax error, unexpected token ";", expecting "]" in C:\Users\UNEAN\Documents\GitHub\NT208\web-development--main\Variant\pages\settings.php on line 7 ```

Ở line 7 trong file ```Setting```, nhận thấy dòng code
```
$config = [
    'currency' => 'USD',
    'timezone' => 'Asia/Ho_Chi_Minh',
    'language' => 'en',
;
``` 
đang bị thiếu dấu đóng ngoặc `]`, thêm dấu đóng ngoặc thành
```
$config = [
    'currency' => 'USD',
    'timezone' => 'Asia/Ho_Chi_Minh',
    'language' => 'en',
];
``` 
thì đã hiển thị đúng




**2.** Ở đường dẫn ```http://localhost:8000/?page=reports``` báo lỗi ```Parse error: syntax error, unexpected variable "$totalsByCategory" in C:\Users\UNEAN\Documents\GitHub\NT208\web-development--main\Variant\pages\reports.php on line 4 ```

Ở dòng 3 và 4 thấy code 
```
$reportRows = []
$totalsByCategory = [];
```

Ở dòng 3 ta thấy thiếu dấu ```;``` nên thêm `;`
```
$reportRows = [];
$totalsByCategory = [];
```
thì lỗi này đã mất



**3.** Ở đường dẫn ```http://localhost:8000/?page=customers``` ta nhận thấy báo lỗi ```Parse error: Unclosed '[' does not match ')' in C:\Users\UNEAN\Documents\GitHub\NT208\web-development--main\Variant\pages\customers.php on line 6```

Ở file `customers.php` ta thấy code
```
if ($customer['active') {
```

Code này thiếu dấu đóng ngoặc, thêm dấu `]` được

```
    if ($customer['active']) {
```
thì đã chạy đúng


## Các lỗi logic