# AngularJS bằng tiếng Việt - phần 3
## Module
Trong các ứng dụng thực tế, việc phân chia ứng dụng thành các thành phần khác nhau là điều cần thiết. Dưới đây là lợi ích của việc chia nhỏ ứng dụng:
* Dễ dàng hơn cho việc quản lý và khai báo ứng dụng cũng như kiểm tra lại sau này
* Khả năng tái sử dụng cũng như tận dụng các 3rd modules
* Nạp từng phần ứng dụng sẽ nhanh hơn là buộc phải nạp toàn bộ ứng dụng vào rồi mới chạy.

Trong AngularJS, module được hỗ trợ trong khai báo ng-app bên cạnh khai báo nó trong mã nguồn script của bạn, dưới đây là một template chuẩn của angular sử dụng modules

	<!doctype html>
	<html ng-app="ExampleModule">
	<head>
	    <script src="http://code.angularjs.org/1.2.12/angular.min.js"></script>
	    <script src="script.js"></script>
	</head>
	<body>
	    <div>
	        Hello, Angular's Module!
	    </div>
	</body>
	</html>

script.js

	var app = angular.module('ExampleModule', []);

* ng-app="ExampleModule": Khai báo một angular app là module, sử dụng ExampleModule được khai báo trong script
* Trong script, angular.module() là hàm khai báo cho module.
* cặp dấu ngoặc [] chính là mảng các module sẽ được nạp chung vào để chạy chung với ứng dụng (module chính được khai báo trong ng-app) ví dụ:

	var app = angular.module('ExampleModule', ['ngRoute', 'ngBootstrap']);

## Controller trong module.
Trong ví dụ trên chúng ta đã thấy việc khai báo module như thế nào, vậy controller khi ứng dụng sẽ được khai báo như thế nào. Hãy xem ví dụ duới đây

index.html

	<!doctype html>
	<html ng-app="ExampleModule">
	<head>
	    <script src="http://code.angularjs.org/1.2.12/angular.min.js"></script>
	    <script src="script.js"></script>
	</head>
	<body>
	    <div ng-controller="ExampleCtrl">
	        Hello, {{ name }}!
	    </div>
	</body>
	</html>

script.js
	
	var app = angular.module('ExampleModule', []);

	app.controller('ExampleController', function($scope) {
		$scope.name = 'World';
	});

* Method .controller của module sẽ đóng vai trò khai báo thêm một controller cho module.
* Function đại diện cho controller được khai báo bình thường giống như controller khai báo bên ngoài module

## Tổ chức của một ứng dụng thực tế
Thông thường thì tổ chức một ứng dụng thực tế sẽ được khởi tạo như sau

	├── index.html
	├── css
	│   └── style.css
	└── scripts
	    ├── module_1.js
	    ├── module_2.js
	    ├── module_3.js
	    └── main.js

* index.html chính là html documents
* style.css chính là mã nguồn css cho document
* main.js chính là mã nguồn cho module chính
* các files js khác là các modules được module chính sử dụng, như vậy template của chúng ta sẽ được khai báo lại như sau

index.html

	<!doctype html>
	<html ng-app="ExampleModule">
	<head>
		<link rel="stylesheet" href="css/style.css">
	    <script src="http://code.angularjs.org/1.2.12/angular.min.js"></script>
	    <script src="scripts/module_01.js"></script>
	    <script src="scripts/module_02.js"></script>
	    <script src="scripts/module_03.js"></script>
	    <script src="main.js"></script>
	</head>
	<body>
	    <div ng-controller="ExampleCtrl">
	        Hello, Angular's Module!
	    </div>
	</body>
	</html>

main.js
	
	var app = angular.module('ExampleModule', ['Module1', 'Module2', 'Module3']);

	app.controller('ExampleController', function($scope) {
		$scope.name = 'World';
	});

Tiếp theo: [Views, Template & Routing](http://google.com)