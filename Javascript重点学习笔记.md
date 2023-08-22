# Javascript重点学习笔记

## 1 函数的初体验

### 1-1 什么是函数

函数是 JavaScript 中的基本组件之一。一个函数是 JavaScript 过程一组执行任务或计算值的语句。要使用一个函数，你必须将其定义在你希望调用它的作用域内。

### 1-2 定义一个函数

```javascript
function fn1(param1){
  语句
  return 返回值
}

匿名函数,去掉函数名即可
(function (param1){
	语句
  return 返回值
})

箭头函数
let fn=(param1)=>{
	语句
  return 返回值
}

let f1=x=>x*x
let f2=(x,y)=>x+y
let f3=(x,y)=>({name:x,age:y}) //返回对象，需要用圆括号包裹

使用构造函数，这样写能让你知道函数是由谁构造的
let f=new Function('x','y','return x+y')
```

### 1-3 函数基本结构

```javascript
        function name(params) {
            
        }
```

params是入参，比如说把鸡蛋放锅里，鸡蛋就是入参。

```javascript
        function pot(params) {
            console.log('加热');
            return '熟鸡蛋'
        }
        // 锅里煎蛋
        const goodEgg = pot(egg)
        console.log(goodEgg);
```

### 1-4 匿名函数

```javascript
        (function (params) {
            // 函数执行语句
            console.log('加热');
            // 返回值 用return返回熟鸡蛋
            return '熟鸡蛋'
        })('鸡蛋')
```

### 1-5 箭头函数

es6当中的函数写法

```javascript
        const hotPot = (params) =>{
            console.log('煮');
            return "熟饭"
        }
```

### 1-6 相加的函数

```javascript
        const add01 = (a,b) =>{
            let sum = a + b
            return sum
        } 
        // 返回值简写 =>代表了返回
        const add02 = (a,b) =>a+b
```

### 1-7 函数两种写法

```javascript
        // 复杂写法
        const add03 =(a,b)=>{
            return {
                a,
                b
            }
        }

        // 简单写法，用圆括号包裹对象，可以直接返回
        const add04 = (a,b)=>({a,b})
```

## 2 函数作用域

### 2-1 局部变量

在作用域内声明的变量，我们称为局部变量。

```javascript
        function fn() {
        	let a=1
        	console.log(a);
        }
        fn()  //1
```

在作用域外部，无法访问到作用域内声明的变量。

### 2-2 全局变量

全局变量只有window。

问，下面的代码打印什么？

```javascript
        const fn=()=>{
            let a=1
            const fn1=()=>{
                let a=2
                console.log(a);
            }
            console.log(a); 
            a=3
            fn1( )
        }
        fn()
        // 1.执行fn a=1打印
        // 2.执行了fn1 a=2打印
        //1 2
```

下面的代码打印什么？

```javascript
        const fn1=()=>{
            let a=4
            const fn2=()=>{
                let a=5
                const fn3=()=>{
                    console.log(a);
                }
                console.log(a);
                a=24
                fn3() 
            }
            console.log(a);
            a=30
            fn2()
        }
        fn1()
        // 4 5 24
```

## 3 数组声明

使用const声明一个方括号。

```javascript
        const array = [1,2,4,5]
        const array2 = new Array(1,4,6,7)
        console.log(array); 
        console.log(array2);
```

### 3-1 从字符串转数组

```javascript
        let str = '1,2,3,4,5,a,g,v'
        let strArr = str.split(',')
        console.log(strArr);

        let str2 = '4545faf'
        // Array.from将字符串转为数组，每个字符都是一个项
        let strArr2 = Array.from(str2)
        console.log(strArr2);
```

### 3-2 从对象转数组

```javascript
        let obj = {
            '0':125,
            '1':false,
            '2':()=>{
                console.log('你好');
            },
            'length':3
        }
        let objArr = Array.from(obj)
        console.log(objArr);
```

对象转数组两点局限性，1.下标必须为数字类型的字符串2. 必须含有length属性。

### 3-3 数组的截取和拼接

使用slice截取。

```javascript
        let arr = [1,2,43,5,67]
		// slice 截取数组
        let subArr = arr.slice(0,3)
        console.log(subArr);
```

使用concat拼接。

```javascript
        let shortArr1 = [1,2,3]
        let shortArr2 = [4,5,6]
        // 扩展... 可以将数组展开 [4,5,6] ---->4,5,6
        // concat 可以填入多个参数，也可以直接填入一个数组
        let longArr = shortArr1.concat(...shortArr2)
        console.log(longArr);
        let longArr2 = [...shortArr1,...shortArr2]
        console.log(longArr2);
```

### 3-4 伪数组

伪数组的原型和真数组不一样，这是我们判断是否为伪数组的依据。

```javascript
        //真数组
		let arr = [1,2,3]
        console.log(arr);
		//forEach()方法对数组的每个元素执行一次
        arr.forEach(item=>{
            console.log(item);
        })
		//document.querySelectorAll 
		//返回与指定的选择器组匹配的文档中的元素列表 (使用深度优先的先序遍历文档的节点)。
        const divList = document.querySelectorAll('div')
        console.log(divList);
        divList.forEach(item=>{
            console.log(item);
        })
```

代码结果

真数组![image-20230819163637028](C:\Users\Dongdong\AppData\Roaming\Typora\typora-user-images\image-20230819163637028.png)

伪数组![image-20230819163656090](C:\Users\Dongdong\AppData\Roaming\Typora\typora-user-images\image-20230819163656090.png)

上面的divList中没有concat属性。

```javascript
        dixList.concat(1,2,3)
        function fn() {
            console.log(arguments);
            arguments.concat(1,2,3)
            // arguments伪数组中，没有forEach方法
            arguments.forEach(arguments=>{
                console.log(arguments);
            })
        }
        fn(1,2,3)
```

结果![image-20230819163830115](C:\Users\Dongdong\AppData\Roaming\Typora\typora-user-images\image-20230819163830115.png)

## 5 数组的增删改查

### 5-1 增加

push( )  从尾部添加。

特点：1.可以添加一个值，也可以添加多个

​      2.不能去拼接数组

```javascript
        let arr=[0,1,2,3]
        arr.push(4) 
        console.log(arr);
        arr.push(5,6)
        console.log(arr);
```

push不能去传入一个数组，需要将数组（用...来展开）展开，否则会将整个数组都放进去。

```javascript
        let arr=[0,1,2,3]
		arr.push(...[7,8])
        console.log(arr);
```

从头部添加unshift()

```javascript
        let arr2=['a','b','c']
        arr2.unshift('d')
        console.log(arr2);
        arr2.unshift('e','f')
        console.log(arr2);
        arr2.unshift(...['g','h'])
        console.log(arr2);
```

concat( )  连接两个数组  (不改变原数组的内容)

```javascript
var arr = [1,2,3];
var c = [4,5,6];
var b = arr.concat(c);

console.log(arr);  // [1,2,3]
console.log(b);    // [1,2,3,4,5,6]
```

splice(startIndex,0,元素...) 增加 ，splice 增删改集大成第一个参数,开始下标，第二个参数,需要从这个下标开始，删除的个数后面的参数，都是需要添加的元素

```javascript
        //添加余下的月份进去
		let subMonth = ['1月','5月','8月']
        subMonth.splice(1,0,'2月','3月','4月')
        console.log(subMonth);
        subMonth.splice(5,0,'6月','7月')
        console.log(subMonth);
        subMonth.splice(8,0,'9月','10月','11月','12月')
        console.log(subMonth);
```

### 5-2 删除

使用pop()来删除，跟push对应，pop从 尾巴删除一个元素。

```javascript
		let arr=[1,2,3]
        arr.pop()
        console. log(arr);

```

shift从头部删除，与unshift对应

```javascript
        let arr=[1,2,3]
		arr4.shift()
        console.log(arr);
```

splice(startIndex，长度） 定点删除。

```javascript
var arr = [1,2,3,4,5]
arr.splice(3,1)
console.log(arr);  // [1,2,3,5]
```



### 5-3 查询

| 获取值对应的下标                     | indexOf                    |
| ------------------------------------ | :------------------------- |
| 判断数组是否包含某个值,返回boolean值 | includes                   |
| 截取数组中的某一段                   | slice(startIndex,endIndex) |

arr[index] 查询对应下标的值

```javascript
        let array = ['a', 'b', 'c']
        let b = array[1] 
        console.log(b); //b
```

indexOf(value) 查询对应值的下标

```javascript
        const index = array.indexOf('c' ) 
        console.log(index); //返回2 
```

includes(value) 判断数组是否包含某个值 。

```javascript
        const isInArr = array.includes('b')
        console.log(isInArr); 
        const isInArr2 = array.includes('d')
        console.log(isInArr2);
        const isInArr3=array.indexOf('a') 
        const isInArr4=array.indexOf('d')  //返回-1
        if(isInArr3>=0){
            console.log('a在数组中');
        }

        if(isInArr4<0){
            console.log('d不在数组中');
        }
```

slice(start,end) 截取  (包含开始，不含结束)

```javascript
// slice(startIndex,endIndex) 截取 包含开始不含结束
// slice(startIndex) 截取从startIndex开始到后面的所有值
var arr = [1,2,3,4]
console.log(arr.slice(1,3));  // [2,3]
console.log(arr.slice(1)); // [2,3,4]
```

### 5-4 修改

`splice(startIndex，长度，元素...)` 修改 先删除后插入

```javascript
var a =[1,2,3,4,5]
a.splice(2,1,9)
console.log(a); // [1,2,9,4,5]
```

## 6 小练习1

输入一个值，生成一个列表，不重复生成。

![image-20230819171909311](C:\Users\Dongdong\AppData\Roaming\Typora\typora-user-images\image-20230819171909311.png)

实现代码

```javascript
			// 第一步，获取input当中输入文本的数据getElementById通过id获取界面中的元素对象
			const input = document.getElementById("input");
			console.log(input);
			const list = document.getElementById("list");
			const todos = [];
			// 监听input的按键事件onkeydown是按键事件，我们给input的按键事件赋予了执行函数
			input.onkeydown = (event) => {
				console.log(event);
				// 如果这个keyCode是13说明我们按下了回车键
				if (event.keyCode === 13) {
					console.log(event.target.value);
					if (todos.includes(event.target.value)) {
						alert("已经有这个值啦！");
					} else {
						todos.push(event.target.value);
						// 创建一个li标签createElement
						const li = document.createElement("li");
						// innerHTML就是li标签中的内容
						li.innerHTML = event.target.value;
						// appendChild就是将li标签放到ul标签中
						list.appendChild(li);
					}
				}
			};
```

## 7 数组遍历

### 7-1 古老方法

使用for循环

```javascript
        let arr = ['a', 'b','d','g'] 
        for(let i=0;i<arr. length;i++){
            console. log(arr[i]);
        }
```

### 7-2 forEach

forEach循环item和 index是forEach送给我们的参数，item是当前循环的项  index是当前下标

forEach循环， 对原数组没有影响，没有返回值

```javascript
        let arr = ['a', 'b','d','g'] 
        arr.forEach((item, index) => {
            console.log(`${item}-${index}`);
            item = 'c'
        })
        console.log(arr);
```

返回结果

![image-20230819172436709](C:\Users\Dongdong\AppData\Roaming\Typora\typora-user-images\image-20230819172436709.png)

### 7-3 map映射

​    map和forEach一样接受一个函数作为参数

​    map有返回值，会返回一个数组，返回数组中的值与接受的函数返回的值相关

​    map不会改变原来的数组

```javascript
        let arr2 = [1,2,3,4,5]
        // double将原数组的每一项，都变成两倍
        const double = (arr) => arr.map(item => {
            return item * 2
        })
        const newArr = double(arr2)
        console.log(newArr);
        console.log(arr2);
```

返回结果

![image-20230819172653073](C:\Users\Dongdong\AppData\Roaming\Typora\typora-user-images\image-20230819172653073.png)

### 7-4 some

some只要数组中有一项满足条件，就输出true:否则输出false

```javascript
        let arr3=[1, 2, 3, 4, 5] 
        const res=arr3.some(item=>{
            return item > 3
        })
        const res2=arr3.some(item=>{
            return item < 0
        })
        console.log(res);    //  true
        console.log(res2);  //  false 
```

### 7-5 every

every 数组中的每一项都满足条件，返回true, 否则返回false

```javascript
        let arr4 = [1, 2, 3, 4, 5]
        const res4 = arr4.every(item =>{
            return item > 0
        })
        const res5=arr4.every(item =>{
            return item > 3
        })
        console.log(res4);   //true
        console.log(res5);   //false 
```

### 7-6 findIndex

findIndex 找到符合条件的就返回下标，没有就返回-1

```javascript
        const arr5=[
            1,2,3,{
                name:'钱多多'
            }
        ]
        const index = arr5.findIndex(item=>{
            return item.name==='钱多多'
        })
        console.log(index); //3
```

### 7-7 find

find返回第一个匹配的元素， 如果没有找到，返回undefined

```javascript
        const arr5=[
            1,2,3,{
                name:'钱多多'
            }
        ]
		const target=arr5.find(item=>{
            return item.name ==='钱多多'
        })
        console.log(target);
```

返回结果

![image-20230819173212019](C:\Users\Dongdong\AppData\Roaming\Typora\typora-user-images\image-20230819173212019.png)

### 7-8 filter

filter过滤返回符合条件的数组，不会改变原数组。

```javascript
        const nums = [1,2,3,4,5,6]
        const numBig = nums.filter(num=>{
            return num > 3
        })
        console.log(numBig);
```

## 8 小练习2

写一个代码，实现输入相应的id删除list的所有元素。

![image-20230819173501964](C:\Users\Dongdong\AppData\Roaming\Typora\typora-user-images\image-20230819173501964.png)

```javascript
			const array = [
				{
					name: "张三",
					id: 1001,
				},
				{
					name: "李四",
					id: 1002,
				},
				{
					name: "王五",
					id: 1003,
				},
				{
					name: "狗蛋",
					id: 1004,
				},
			];
			// 获取到list对象
			const list = document.getElementById("list");
			// 获取到input对象
			const input = document.getElementById("input");

			// 删除list下面所有的元素
			const removeAllChild = () => {
				const lis = document.querySelectorAll("li");
				if (lis.length) {
					// 循环伪数组，删除list下面所有的元素
					for (let i = 0; i < lis.length; i++) {
						list.removeChild(lis[i]);
					}
				}
			};

			// 重新渲染ul list
			const renderList = (array) => {
				// 先清空list下面的元素
				removeAllChild();
				// 将array中的数据添加到列表中
				for (let i = 0; i < array.length; i++) {
					const item = array[i];
					console.log(item);
					const li = document.createElement("li");
                    //innerHTML获取 HTML 语法表示的元素的后代。
					li.innerHTML = item.name;
					list.appendChild(li);
				}
			};
			renderList(array);

			// 监听input按键事件，当按下回车键的时候,通过输入的id值，找到数组中对应的下标，
			// 然后调用splice方法，删除数组中对应的项目
			input.onkeydown = (e) => {
				if (e.keyCode === 13) {
					// input当中的数据
                    //target点击事件触发的DOM节点
					const value = Number(e.target.value);
					// 找到id为value的数据下标 findIndex暂时看不懂，没关系
                    //findIndex() 方法返回数组中满足提供的测试函数的第一个元素的索引。若没有找到对应元素则返回-1。
					const targetIndex = array.findIndex((item) => {
						return item.id === value;
					});
					if (targetIndex >= 0) {
						array.splice(targetIndex, 1);
						renderList(array);
					}
				}
			};
```

## 9 数组的其他用法

### 9-1 翻转数组

reverse翻转数组，会改变原来的数组，也会返回一个新数组，都是翻转之后的。

```javascript
        let arr=['a','b','c']   //['c','b','a']
        const reverseArr = arr.reverse()
        console.log(arr);
        console.log(reverseArr);
```



### 9-2 数组转字符串join

join可以将数组转为字符串

join传入参数，分隔符

```javascript
        let arr2 = ['html','css','js']  // 'html,css,js'
        const str = arr2.join(',')
        const str2 = arr2.join('/') // html/css/js
        console.log(str);
        console.log(str2);
```

### 9-3 数组排序sort

​    会改变原来的数组，也会返回一个新数组，都是排序之后的

​    接受一个函数作为参数，函数有返回值， 且有两个参数，返回第一个参数-第二个参数为升序，反之为降序

```javascript
        let arr3 = [5,3,7,545,86,32,5]
        arr3.sort((a, b)=>{
        //升序
            return a-b
        })
        console.log(arr3);
		//降序
        const res = arr3.sort((a,b)=>{
            return b-a
        })
```

### 9-4 求和reduce

reduce((*pre*,*cur*)

​    第一个参数是累加器

​    第二个参数是我们最后的返回的结果

​    5+3  pre=0 cur=arr3[0]

​    3+7 pre=5 cur=arr3[1]

```javascript
        let arr1 = [1,2,3,4,5]
        const sum1 = arr1.reduce((pre,cur)=>{
            return pre+cur
        },0)
        console.log(sum1);  //15
```

```javascript
        let arr2 = [1,2,3,4,5]
        const sum2 = arr2.reduce((prev,cur)=>{
            return prev+cur
        },10)
        console.log(sum2); //25
```



## 10 小练习3

根据年龄升序、降序。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button id="like">通过好评排序</button>
    <button id="price">通过价格排序</button>
    <ul id="list"></ul>
    <script>
        const sales=[
            {
                name:'张三',
                like:30,
                price:100
            },{
                name:'李四',
                like:60,
                price:66
            },{
                name:'王五',
                like:10,
                price:102
            }
        ]

        // 拿到list对象
        const list = document.getElementById('list')
        // 拿到button对象
        const like = document.getElementById('like')
        const price = document.getElementById('price')

        // 优化技巧 消除重复 事不过三
        // 定义一个删除元素，删除所有的li标签 将删除函数封装起来
        const removeLis = () =>{
            // 删除所有的li标签
            const lis = document.querySelectorAll('li')
            console.log(lis);
            lis.forEach(li => {
                list.removeChild(li)
            })
        }
 
        // 定义一个重新渲染的函数 将渲染函数封装起来
        const reRenderList = (array) => {
            removeLis()
            // 然后用新的数组去渲染列表
            array.forEach(sale =>{
                const li = document.createElement('li')
                li.innerHTML = `${sale.name}-----${sale.like}-----${sale.price}`
                list.appendChild(li)
            })            
        }
        const ordered = (array,attr)=>{
            return array.sort((a,b)=> {return a[attr] - b[attr]})
        }
        reRenderList(sales)

        // onclick事件，注册按钮点击
        like.onclick = () =>{
            // 对于对象排序，需要取出对象中的值来进行比较
            const result = ordered(sales,'like')
            // 然后用新的数组去渲染列表
            reRenderList(result)
        }

        price.onclick = () =>{
            // 对于对象排序，需要取出对象中的值来进行比较
            const result = ordered(sales,'price')
            // 然后用新的数组去渲染列表
            reRenderList(result)
        }
    </script>
</body>
</html>
```

## 11 class类

```javascript
        // class类
        class Doggie{
            constructor(name){
                this.name = name
            }
            legNumber = 4
            bar(){
                console.log('bar');
            }

            waving(){
                console.log('waving');
            }
        }
        // 使用new操作符，来构造一个对象
        let chaiQuan = new Doggie('柴犬')
        console.log(chaiQuan);
```

## 12 class计算器

```javascript
        class Calculator{
            constructor(a,b){
                this.a = a
                this.b = b
            }
            add(){
                return this.a + this.b
            }
            subtract(){
                return this.a - this.b
            }
            multiply(){
                return this.a * this.b
            }
            divide(){
                return this.a / this.b
            }
        }
        const calObj = new Calculator(50,6)
        const addNum = calObj.add()
        const subNum = calObj.subtract()
        const mulNum = calObj.multiply()
        const divNum = calObj.divide()
        console.log(addNum);
        console.log(subNum);
        console.log(mulNum);
        console.log(divNum);
```

