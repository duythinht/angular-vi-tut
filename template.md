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

## Views & Route
Đôi khi trong một trang, nhiều khi chúng ta chỉ muốn hiển thị một phần HTML ứng với mỗi chức năng cụ thể mà ta không cần chuyển đổi trang, Angular là một full-stack framework hiệu quả giúp chúng ta có thể làm được việc này nhanh chóng và dễ dàng. Để làm việc này thì bạn cần gọi và sử dụng một extends module của angular là [ngRoute](angular-route.min.js)

index.html
	
	<!doctype html>
	<html ng-app="ExampleModule">
	<head>
	    <script src="http://code.angularjs.org/1.2.12/angular.min.js"></script>
	    <script src="http://code.angularjs.org/1.2.12/angular-route.min.js"></script>
	    <script src="script.js"></script>
	</head>
	<body>
	    <div ng-view></div>

	    <script type="text/ng-template" id="message.html">
	    	<input type="text" ng-model="name">
			<h3>Hello, {{ name }}!</h3>
		</script>
		<script type="text/ng-template" id="another.html">
			<input type="text" ng-model="name">
			<h3>Chào, {{ name }}</h3>
		</script>
	</body>
	</html>

script.js

	var app = angular.module('ExampleModule', ['ngRoute']);

	app.config(function($routeProvider, $locationProvider) {
		$routeProvider.when('/message', {
			templateUrl: 'message.html',
			controller: 'MessageCtrl'
		});

		$routeProvider.when('/another', {
			templateUrl: 'another.html',
			controller: 'AnotherCtrl'
		});

		$routeProvider.otherwise({
	        redirectTo: '/message'
	    });
	});


	app.controller('MessageCtrl', function($scope) {
		$scope.name = 'World';
	});

	app.controller('AnotherCtrl', function($scope) {
		$scope.name = 'Sky';
	});

* ng-view đánh dấu vị trí view, nơi sẽ thể hiện template trọng document
* ngRoute là module hỗ trợ routing url cho angular
* app.config là method cho phép khai báo các Controller, View tương ứng với url
* $routeProvider.otherwise xử lý cho route mặc định