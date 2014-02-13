# AngularJS bằng tiếng Việt - phần 2
## HTTP & AJAX
AJAX là một kỹ thuật rất quan trọng trong nền điện toán hiện đại, cũng như mọi Javascript framework khác AngularJS cung cấp cho người dùng công cụ để làm việc với AJAX thông qua một injector là $http. Dưới đây là một ví dụ về xử lý ajax

index.html
	
	<!DOCTYPE html>
	<html ng-app>
	<head>
		<title>Hello World</title>
		<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.2.12/angular.min.js"></script>
		<script src="script.js"></script>
	</head>
	<body>
		<div ng-controller="ExampleCtrl">
			<table border="1" cellspacing="0">
				<thead>
					<tr>
						<th>ID</th>
						<th>Name</th>
						<th>Amount</th>
						<th>Tool</th>
					</tr>
				</thead>
				<tbody>
					<tr ng-repeat="item in list">
						<td>{{ item.id }}</td>
						<td>{{ item.name }}</td>
						<td><input type="text" ng-model="item.amount"></td>
						<td>
							<button ng-click="doEdit(item)">Edit</button>
							<button ng-click="doDelete(item)">Delete</button>
						</td>
					</tr>
				</tbody>
			</table>
			<!-- Show the list data as Json, To debug -->
			<pre>{{ list |json }}</pre>
		</div>

	</body>
	</html>

script.js
	
	ExampleCtrl = function($scope, $http) {
		$http.get('/get.json').success(function(data) {
			$scope.list = data;
		});

		$scope.doEdit = function(item) {
			var notice = "Item #" + item.id + " has been edited with amount: " + item.amount;

			$http.put('/update', item).success(function(data) {
				alert(notice);
			});
		}

		$scope.doDelete = function(item) {
			var notice = "Item #" + item.id + " has been deleted";

			//Remove item in list
			$scope.list.splice($scope.list.indexOf(item),1);

			//Delete at /delete/:id
			$http.delete('/delete/' + item.id).success(function(data) {
				alert(notice)
			});
		}
	}

get.json (JSON for get data)

	[
		{"id": 1, "name": "iPhone 5s", "amount": 10},
	    {"id": 2, "name": "Nexus 5", "amount": 12},
	    {"id": 3, "name": "Xperia Z1", "amount": 13},
	    {"id": 4, "name": "Motorola X", "amount": 8},
	    {"id": 5, "name": "Galaxy S4", "amount": 21}
	]

* $scope list sẽ được lấy từ ajax get request, sau đó bind vào html thông qua ng-repeat.
* Khi người dùng cập nhật dữ liệu, model sẽ được tự động thay đổi (xem ở json debug bên dưói html)
* Khi thực hiện sự kiện click chuột thì $http sẽ được gọi và thực hiện các thao tác request tương ứng (PUT/DELETE)
* Quá trình ví dụ trên chỉ mới implements ở bên phía front-end, bạn cần viết thêm các mã nguồn cho backend (/update | /delete/:id)
* Tương tự, Angular cũng cung cấp $http.post để thực hiện xử lý ajax cho method POST
* Xem thêm chi tiết về $http tại: http://docs.angularjs.org/api/ng.$http

## Filter
Trong ví dụ ở phía trên, trong phần document bạn có thể thấy chúng ta có cú pháp đề định dạng dữ liệu dạng JSON

	{{ list | json}}

AngularJS cung cấp sẵn cho chúng ta một số các filter hữu ích, dùng để định dạng cũng như lọc dữ liệu, ví dụ về định dạng tiền tệ:

index.html

	<!doctype html>
	<html ng-app>
	<head>
	    <script src="http://code.angularjs.org/1.2.12/angular.min.js"></script>
	    <script src="script.js"></script>
	</head>
	<body>
	    <div ng-controller="Ctrl">
	        <input type="number" ng-model="amount"><br>
	        default currency symbol ($):<span id="currency-default">{{amount | currency}}</span>
	        custom currency identifier (USD$): <span>{{amount | currency:"USD$"}}</span>
	    </div>
	</body>
	</html>

script.js

	Ctrl = function($scope) {
		$scope.amount = 1234.56;
	}

Kết quả sau khi định dạng của filter sẽ như sau:
	
	default currency symbol ($): $1,244.00
	custom currency identifier (USD$): USD$1,244.00

Tiếp theo: [Module & Realtime application](https://github.com/duythinht/angular-vi-tut/blob/master/module.md)