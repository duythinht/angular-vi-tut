# AngularJS bằng tiếng Việt - phần 4
## Template
Đôi lúc trong quá trình xây dựng hệ thống, file HTML trở nên phức tạp để giải quyết vấn đề này ta cần chia thành nhiều phần khác nhau, AngularJS cung cấp cho chúng ta một giải pháp hữu ích đó là template. Trong Angular, chúng ta có 2 cách để tạo một template.

### Dùng file ngoài:
Chúng ta có thể dùng thêm một file html bên ngoài để làm template cho file chính, ví dụ:

message.html
	
	<h3>Hello, {{name}}!</h3>

### Dùng script
Chúng ta có thể tích hợp thẳng template vào file hiện hành thông qua thẻ script với type là text/ng-template
	
	<script type="text/ng-template" id="message.html">
		<h3>Hello, {{name}}!</h3>
	</script>

	