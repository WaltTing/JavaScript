# JS数组的增删改查
## 1.增
增在数组中其实就是插入若干元素。
### 1.1 从数组头部插入
	var arr = [1,2,3,4];
	arr.unshift(0,2,1);
	console.log(arr);  //[ 0, 2, 1, 1, 2, 3, 4 ]
### 1.2 从数组尾部插入
	var arr = [1,2,3,4];
	arr.push(5);
	console.log(arr);
### 1.3 任意位置插入
	var arr = [1,3,2,4,5,6]
	//splice用于插入操作有三个参数：插入的起始位置，要删除的元素，要插入的元素（不限个数）
	arr.splice(3,0,3,5);
	
	console.log(arr);  //[ 1, 3, 2, 3, 5, 4, 5, 6 ] 
也可以封装插入函数：

	Array.prototype.insert = function(index,item){
	    this.splice(index,0,item);
	};
	var nums = ["one","two","three"];
	nums.insert(2,"four");
	console.log(nums);  //[ 'one', 'two', 'four', 'three' ]
## 2.删
### 2.1 删除最后一项
	var arr = [1,2,3,4];
	var rec = arr.pop();
	console.log(rec);  //4
	console.log(arr); //[ 1, 2, 3 ]
### 2.2 删除第一项
	var arr = [1,2,3,4];
	var rec = arr.shift();
	console.log(rec); //1
	console.log(arr); //[ 2, 3, 4 ]
## 3.改
所谓的改就是替换数组中的元素。用splice()先将某一位置元素删除，然后再插入一元素。

	var arr = [1,2,3,4,5];
	//三个参数：起始位置，要删除的项数，插入的项
	arr.splice(2,1,5); //将3替换成5
	console.log(arr);  //[ 1, 2, 5, 4, 5 ]

## 4.查

查找某一元素对应的数组下标。

	var arr = [1,2,3,4,5];
	console.log(arr.indexOf(3));  //2