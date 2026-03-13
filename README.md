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
**1.** Ở đường dẫn ```http://localhost:8000/?page=orders``` ta có Queue hiện tại là 2 người nhưng theo logic code thì chỉ có 1 người tên "Minh Vo" có trạng thái là 'pending'.

Ở file ```orders.php``` line 6 có đoạn code
```
if ($order['status'] === 'completed')
```
Cần sửa 'completed' -> 'pending'
```
if ($order['status'] === 'pending')
```
**2.** Ở đường dẫn ```http://localhost:8000/?page=customers``` ta có số lượng members là 2 người.
Ở file ```customers.php``` có đoạn code
```
    [
        'name' => 'Minh Vo',
        'email' => 'minh@student.example.com',
        'tier' => 'student',
        'active' => false,
    ],
```
Cần sửa 'false' -> 'true' để có thể hiện đầy đủ số members
```
    [
        'name' => 'Minh Vo',
        'email' => 'minh@student.example.com',
        'tier' => 'student',
        'active' => true,
    ],
```
**3.** Ở file ```customers.php``` có đoạn code
```
    [
        'name' => 'Linh Pham',
        'email' => 'linh@student.example.com',
        'tier' => 'falcuty',
        'active' => true,
    ],
```
Cần sửa 'falcuty' -> 'student' để có thể tính đúng số liệu
```
    [
        'name' => 'Linh Pham',
        'email' => 'linh@student.example.com',
        'tier' => 'student',
        'active' => true,
    ],
```

**4.** Ở file `dashboard.php`, đoạn 
```
foreach ($products as $sku => $product) {
    if ($product['stock'] < 1) {
        $lowStockItems[] = $sku . ' - ' . $product['name'];
    }
}
```
Đang đếm số lượng hàng còn tồn kho thấp, tuy nhiên trong code đang tính là số lượng hàng đã hết (nhỏ hơn 1)

Cần sửa thành 
```
foreach ($products as $sku => $product) {
    if ($product['stock'] < 5) {
        $lowStockItems[] = $sku . ' - ' . $product['name'];
    }
}
```
để đếm thành số lượng còn tồn kho dưới 5 (tồn kho ít)

**5.** Ở file `checkout.php` có đoạn

```
foreach ($cart as $item) {
    $subtotal = $products[$item['sku']]['price'] * $item['qty'];
}
```
Logic đang thực hiện đếm tổng tiền nhưng sau mỗi vòng foreach, `$subtotal` lại được gán mới và `$subtotal` chỉ nhận giá trị của vòng foreach cuối cùng.
Cần sửa thành 
```
foreach ($cart as $item) {
    $subtotal += $products[$item['sku']]['price'] * $item['qty'];
}
```
để thực hiện cộng đúng tổng tiền
