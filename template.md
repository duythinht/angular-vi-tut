# AngularJS bằng tiếng Việt - phần 4
## Template
Đôi lúc trong quá trình xây dựng hệ thống, file HTML trở nên phức tạp để giải quyết vấn đề này ta cần chia thành nhiều phần khác nhau, AngularJS cung cấp cho chúng ta một giải pháp hữu ích đó là template. Trong Angular, chúng ta có 2 cách để tạo một template.

#### Dùng file ngoài:
Chúng ta có thể dùng thêm một file html bên ngoài để làm template cho file chính, ví dụ:

message.html
	
	<h3>Hello, {{name}}!</h3>

#### Dùng script
Chúng ta có thể tích hợp thẳng template vào file hiện hành thông qua thẻ script với type là text/ng-template
	
	<script type="text/ng-template" id="message.html">
		<h3>Hello, {{name}}!</h3>
	</script>

#### Cách sử dụng template
Có nhiều cách để sử dụng template, tuy nhiên trong AngularJS có 2 cách thông dụng nhất để dùng template đó là ng-include và ngRoute (sẽ nói ở phần sau), ví dụ:

index.html

	<!doctype html>
	<html ng-app="ExampleModule">
	<head>
	    <script src="http://code.angularjs.org/1.2.12/angular.min.js"></script>
	    <script src="script.js"></script>
	</head>
	<body>
	    <div ng-controller="ExampleCtrl">
	    	<input type="text" ng-model="name">
	        <div ng-include src="template_name"></div>
	    </div>
	    <script type="text/ng-template" id="message.html">
			<h3>Hello, {{name}}!</h3>
		</script>
	</body>
	</html>

var app = angular.module('ExampleModule', []);

app.controller('ExampleCtrl', function($scope) {
	$scope.template_name = 'message.html';
	$scope.name = 'World';
});

