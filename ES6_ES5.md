---
title: ES5方法回顾
tags: 
- ES5
- ES6
categories:
- ES6
---
### ES5数组方法

- `forEach`:遍历数组
	- 语法:`数组.forEach(fn)`

			var arr = [{name:'zs'},{name:'ls'},{name:'ww'}];
			
			arr.forEach(function(v,i){
				console.log('值' + v.name + ',索引' + i);
			});


- `map`:映射(利用数组通过函数中的算法生成一个数组)
	- 语法:`数组.map(fn)`,返回一个数组,数组中的每一个元素就是map函数中fn的返回值

			var arr = [1,2,3,4];
			
			var newArr = arr.map(function(v,i){
				return v * v;
			});
			
			console.log(newArr);


- `filter`:过滤筛选
	- 语法:`数组.filter(fn)`,返回一个数组,筛选出满足条件的数据(满足条件返回true,不满足返回false)

			// 筛选出奇数
			var arr = [ 1, 2, 3, 4, 5, 6 ];
			var a = arr.filter( function ( v ) { 
				return v % 2 === 1;
			});
			console.log(a);
			

- `some`:判断数组中至少有一个数据符合要求,返回true,否则返回false
	- 语法:`数组.some(fn)`
		
			var arr = [ '123', {}, function () {}, '123' ];
			// 判断数组中至少有一个数字 则返回true
			var isTrue = arr.some( function ( v ) { 
				return typeof v === 'number';
			} );
			
			console.log(isTrue);
			


- `every`:必须满足所有元素都符合要求才会返回 true
	- 语法:`数组.every(fn)`
	
			var arr = [ 1, 2, 3, 4, 5, '6' ];
			var isTrue = arr.every( function ( v ) { 
				// 如果都是数字则返回true
				return typeof v === 'number';
			} );
			
			console.log(isTrue);


- `indexOf`:从数组中查找某个数据的索引(从左向右查找)
	- 语法:`数组.indexOf(元素,从哪个位置开始查找)`

			var arr = [ 1, 2, 3, 4, 5 ];
			// 不传第二个参数,默认是0
			var res = arr.indexOf( 4 );
			console.log( res );
		
			var arr = [ 1, 2, 3, 4, 5, 4, 5, 6 ];
			// 从索引4开始查找元素4
			var res = arr.indexOf( 4, 4 );
			console.log( res );


- `lastIndexOf`:从数组中查找某个数据的索引(从右向左查找)
	- 语法:`数组.lastIndexOf(元素,从哪个位置开始查找)`

			var arr = [ 1, 2, 3, 4, 5 ];
			// 不传第二个参数,默认是0
			var res = arr.lastIndexOf( 4 );
			console.log( res );
		
			var arr = [ 1, 2, 3, 4, 5, 4, 5, 6 ];
			// 从索引4开始查找元素4
			var res = arr.lastIndexOf( 4, 4 );
			console.log( res );

