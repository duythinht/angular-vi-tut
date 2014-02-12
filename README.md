Hướng dẫn AngularJS bằng tiếng Việt
====================================

## Giới thiệu
AngularJS là một full-stack Javascript framework, được phát triển bởi Google. Ban đầu mục tiêu của Angular là để xây dựng các ứng dụng dựa trên tiêu chuẩn MVC (Model - View - Controller), sau đó Angular dần phát triển và tiến gần hơn về với MVVM và MVP. Sau đó Google đã định nghĩa nó lại là MVW (Model-View-Whatever) để ám chỉ Angular là một framework có tính chất "whatever works for you".

## 	Cài đặt
Việc cài đặt luôn là điều khởi đầu của việc học bất cứ framework nào. Bởi vì là Javascript, nên Angular cũng được sử dụng bằng cách "import" file js vào HTML document. Sau đây là một HTML Template chuẩn của Angular

	<!DOCTYPE html>
	<html ng-app>
	<head>
		<title>Hello World</title>
		<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.2.12/angular.min.js"></script>
		<script src="script.js"></script>
	</head>
	<body>
		<h1>Hello angular</h1>
	</body>
	</html>

Trong đó:
* angular.min.js là file thư viện của angular
* script.js là file javascript chứa mã nguồn do bạn tự viết
* Thuộc tính **ng-app** của thẻ HTML sẽ đánh dấu đây là một bắt đầu document của AngularJS

## Ví dụ đơn giản về Model và data binding
Một tính năng đơn giản và cực kỳ hữu ích của AngularJS chính là data-binding, Angular thược hiện điều này thông qua một thuộc tính ng-model trong html.
Data-binding của Angular thực sự mạnh mẽ, việc sử dụng data-binding sẽ giúp tối ưu hoá mã nguồn và giúp giảm số lượng dòng code mà bạn phải viết. Sau đây là ví dụ về cách sử dụng data-binding.
	
	<!DOCTYPE html>
	<html ng-app>
	<head>
		<title>Hello World</title>
		<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.2.12/angular.min.js"></script>
		<script src="script.js"></script>
	</head>
	<body>
		<input ng-model="name">
		<h3>Hello, {{ name }}! Welcome to Angular.</h3>
	</body>
	</html>

Trong ví dụ trên bạn thấy:
* Chúng ta có một ng-model và nó có tên là "name"
* Ở phía dưới, chúng ta có một câu chào, và model "name được" bind vào đó. Khi bạn thay đổi value của model "name" câu chào sẽ thay đổi.