---
title: JS数组字符串方法整理
tags: 
- JS
categories:
- JS
---
# 回顾数组字符串方法
## 数组对象方法
#### 转换数组(将数组转换成一些其他形式): 
1. `valueOf()` 返回数组对象本身,和直接输出数组对象是一样的

2. `toString()` 把数组以逗号相连转为字符串
```
var arr = [1, 2, 3, 4, 5];
console.log(arr.toString());
```

3. `join()` 用指定分隔符连接数组元素转为字符串
```
var arr = [1, 2, 3, 4, 5];
console.log(arr.join());
console.log(arr.join("-"));
console.log(arr.join(""));
```

> 注: 不传入参数即表示默认用逗号连接转为字符串

#### 数组检测: 用于判断是否是数组类型
1. `instanceof 关键字` 注意它不是方法没有(),并且也适用于其他判断
```
var arr = [1,2,3,4,5];
console.log(arr instanceof Array); //true
console.log("a" instanceof Array); //false
```

2. `Array.isArray()`
```
var arr = [1,2,3,4,5];
console.log(Array.isArray(arr));//true
console.log(Array.isArray("a"));//false
```

#### 增删方法:
1. `push()` 从后面添加元素,返回新数组的长度
```
var arr = [11,22,33,44,55];
console.log(arr.push(99));
```

2. `pop()` 从后面删除元素,返回被删除的元素
```
var arr = [11,22,33,44,55];
console.log(arr.pop());
```

3. `shift()` 从前面删除元素,返回被删除的元素
```
var arr = [11,22,33,44,55];
console.log(arr.shift());
```

4. `unshift()` 从前面添加元素,返回新数组的长度
```
var arr = [11,22,33,44,55];
console.log(arr.unshift(0));
```

#### 迭代方法:
1. `filter` 需要传入一个回调函数,该回调函数需具有三个参数,这个回调函数由js内部调用,filter方法会遍历数组,每次遍历到一个元素就会执行回调函数一次,第一个参数为当前元素,第二个参数为当前元素的索引,第三个参数为当前数组
```
var arr = [1500, 1200, 2000, 2100, 1800];
var newArr = arr.filter(function (element, index, array) {
 if (element > 2000) {
  return false;
 }
 return true;
});
console.log(newArr);
// 回调函数返回值为true则表示当前需要保留当前元素,返回false则表示不保留当前元素,如果没写返回值默认为undefined也就是false 
// 当数组迭代完成时,会返回一个新数组,这个新数组中的元素取决于在回调函数中,有多少个元素返回了true得以保留
```

2. `forEach`方式进行迭代(ES5的新方法)
和filter()方法一样传入一个回调函数,有JS内部调用进行数组遍历,循环遍历数组时,每循环到一个元素就会调用一次,回调函数同样有3个参数,参数1: 遍历到的元素,参数2: 便利到的元素索引,参数3: 原数组
```
var arr = [4, 6, 7, 8, 3, 46, 8];
arr.forEach(function(e){
    console.log(e);
}

var arr = [4, 6, 7, 8, 3, 46, 8];
arr.forEach(function(element, index, arr){
    console.log(element);
    console.log(index);
    console.log(arr);
});
```

#### 位置方法:
1. `indexOf()` 返回找到数组中第一个a出现的位置
```
var arr = ["c", "a", "z", "a", "x", "a"];
console.log(arr.indexOf("a"));//1
// 注:搜索""结果是0,搜不到的结果是-1,搜索"ca"结果也是0
```

2. `lastIndexOf()` 返回从后往前找到数组中第一个a出现的位置
```
var arr = ["c", "a", "z", "a", "x", "a"];
console.log(arr.lastIndexOf("a"));//5
// indexOf的第二个参数:从哪个索引开始找,包含该索引
// 找不到返回-1!
```

3. 实例：寻找每个a出现的位置
```
var arr = ["c", "a", "z", "a", "x", "a"];
var index = -1;
do {
    index = arr.indexOf("a", index+1);
    console.log(index);
} while (index !== -1);
```

4. 实例：统计元素的出现次数
要统计每个元素出现的次数,可以使用键值对(对象)的形式来存储数据,元素作为键(对象的属性),出现的次数作为值,元素每出现一次,就让键对应的值自增一即可
```
var arr = ["c", "a", "z", "a", "x", "a"];
var count = {};
for (var i = 0; i < arr.length; i++) {
    var item = arr[i];
    if (count[item]) { //循环过程中判断,如果这个元素在对象中有键,那取出值进行自增
        count[item]++;
    } else { //如果这个元素在对象中没有键,那就加一个键进去,初始值为1,表示出现了一次
        count[item] = 1;
    }
}
console.log(count);
```

#### 其他方法:
1. slice截取数组,不会改变原数组,返回一个新数组
```
var arr = [4, 6, 7, 8, 3, 46, 8];
console.log(arr.slice(0, 2));//结果是[4, 6]
// 注:开始能取到,结束取不到 !
```

2. splice删除数组中的元素,会对原数组进行修改,返回删掉的数组
```
var arr = [4, 6, 7, 8, 3, 46, 8];
console.log(arr.splice(0, 2));
// 从一个索引开始,删除多少个元素
// 第三个参数可以往删除的地方添加元素,可以添加多个,使用逗号隔开即可
```

3. 清空数组:
```
var array = [1,2,3,4,5,6];
//方式1
array.splice(0,array.length); //删除数组中所有项目 
//方式2
array.length = 0; //length属性可以赋值
//方式3
array = [];  //推荐
```

## 字符串对象方法
#### 截取方法
1. `slice()` 从start位置开始，截取到end位置，end取不到
2. `substring()` 从start位置开始，截取到end位置，end取不到
3. `substr()` 从start位置开始，截取length个字符

#### 位置方法 `indexOf()`

#### 替换方法 `replace()`

#### 字符方法 `charAt()`

#### 其他方法
1. `split()`
2. `trim()`
3. `charCodeAt()`  //获取指定位置处字符的ASCII码
4. `str[0]`   //ES5，IE8+支持 和charAt()等效

# 归纳整理数组字符串常用方法
## 字符串方法

```
var a="i love you!";
```

1. `toUpperCase()` 将小写转换成大写

2. `toLowerCase()` 将大写转换成小写

3. `charAt()` 返回指定位置的字符
```
document.write(a.charAt(4));//结果是v
// 注：字符是从0开始到length-1结束
```

4. `indexOf()` 返回指定字符的位置
```
document.write(a.charAt(v));//结果是4
```

5. `lastIndexOf()`

6. `split()` 返回被分割的字符串数组
```
document.write(a,split("v",2));//结果是["i lo","e you!"]
// 注:前面指定分割的位置,不填则分割成一个个字符;后面指定分割组数,可不填
```

7. `substring()` 提取字符串
```
document.write(a.substring(2,5));//结果是love
document.write(a.substring(7));//结果是you!
// 注:前面指定开始提取的位置;后面指定结束提取的位置,不填则默认到字符串最后
```

8. `subsrt()` 提取指定数目字符串
```
document.write(a.substr(2,4));//结果是love
document.write(a.substr(-4));//结果是you!
// 注:前面指定开始提取的位置;后面指定提取的长度,不填则默认到字符串最后;若出现-,则表示倒着数
```

## 数组方法

1. `concat()` 连接数组,不改变原数组,返回一个新数组
```
var a=["1","2"];
var b=["3","4"];
document.write(a.concat(b));
//结果是["1","2","3","4"]
```

2. `join()` 用指定分隔符连接数组元素,返回string
```
var a=["I","love","you"];
document.write(a.join("."));//结果是I.love.you
// 注:若不指定,默认","
```

3. `reverse()` 颠倒数组元素顺序,会改变原数组
```
var a=["1","2"];
document.write(a.reverse());//结果是["2","1"]
```

4. `slice()` 选定元素,不改变原数组,返回一个子数组
```
var a=["1","2","3","4"];
document.write(a.slice(2,4));//结果是["3","4"];
// 注:前面指定开始选定的位置,注意不包括这个位置;后面指定结束选定的位置,不填则默认到字符串最后;若出现-,则表示倒着数
```

5. `sort()` 数组排序
```
function a(x,y){return x-y;}
//升序,若降序,return y-x;
var b=["1","7","5","3"];
document.write(b.sort(a));
//结果是["1","3","5","7"]
```

6. `slice(start,end)` 截取指定索引之间的字符串(包括start,不包括end),返回新的字符串
```
var str = "abcdaefga";
console.log(str.slice(1,5)); // "cda"
```

7. `subString(start,stop)` 截取指定索引之间的字符串(包括start,不包括stop),返回新的字符串
```
var str = "abcdaefga";
console.log(str.slice(1,5)); // "cda"
```

8. `charAt(index)` 返回指定位置的字符
```
var str = "abcde";
console.log(str.charAt(3)); // d
```

9. `concat(str)` 连接字符串,生成一个新的字符串,原字符串不会被改变
```
var str1 = "abc";
var str2 = "def";
console.log(str1.concat(str2)); // “abcdef”
```

10. `trim()`去掉字符串的首尾的空格,返回新的字符串
```
var str = "  abcd  ";
console.log(str.trim()); // "abcd"
```

