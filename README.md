
#### 数组解构



```
const arr = ["1","2","3"]

let a,b,c

// 解构赋值
//将数组的第一个元素赋值给第一个变量，第二个元素赋值给第二个变量，依次类推

[a,b,c] = arr
console.log(a,b,c) // 1 2 3

```


```
// 声明变量同时解构
let [a,b,c] = ["1","2","3"]
console.log(a,b,c) // 1 2 3

```


```
// 如果变量数大于元素数量，则超出的变量部分赋值为undefined
const arr = ["1","2","3"]
let [a,b,c,d] = arr
console.log(a,b,c,d) // 1 2 3 undefined

```


```
// 默认值，如果变量声明了默认值，解构为undefined的时候，则会使用默认值，否则使用对应元素
const arr = ["1","2","3"]
let [a,b,c=10,d=11] = arr
console.log(a,b,c,d) // 1 2 3 11

```


```
// 解构数组时可以使用...获取剩余的元素

const arr = ["1","2","3","4","5"]
// 第一个元素赋值给a，第二个元素赋值给b，其余元素赋值给c
let [a,b, ...c] = arr
console.log(a) // 1
console.log(b) // 2
console.log(c) // ['3','4','4']

```


```
// 解构多维数组
const arr = [[1,2,3],[4,5,6]]
let [[a,b,c],obj] = arr

console.log(a,b,c) // 1 2  3
console.log(obj) // [4,5,6]

```

#### 对象解构



```
const user = {"name":"q",age:18}
// 声明变量同时解构对象
let {name,age} = user

console.log(name,age) // q  18

```


```
// 先声明变量，再解构对象
const user = {"name":"q",age:18}

let name,age

({name,age} = user)  // {} 在js中是代码块，所以需要在外面使用()
console.log(name,age) // q 18

```


```
const user = {"name":"q",age:18}

// 如果变量名与属性名不匹配，则解构为undefined
let {a,b} = user
console.log(a,b) // undefined undefined

// 可以给变量起别名再解构
// 可以给变量既起别名，又设置默认值
let {name:c,age:d=20} = user

console.log(c,d) // q  18


```

#### 对象的序列化


JS中的对象使用时都是存在于计算机的内存中的,序列化指将对象转换为一个可以存储的格式,在JS中对象的序列化通常是将一个对象转换为字符串（JSON字符串）



```
const user = {name:"l",age:18}

// 将一个对象转换为json字符串
const strUser = JSON.stringify(user)
console.log(strUser)

// 将一个json字符串转换为js对象
const objUser = JSON.parse(strUser)
console.log(objUser)

```


> 编写JSON的注意事项：
> 
> 
> 1. JSON字符串有两种类型：
> 
> 
> 	* JSON对象 {}
> 	* JSON数组 \[]
> 2. JSON字符串的属性名必须使用双引号引起来
> 3. JSON中可以使用的属性值（元素）
> 
> 
> 	* 数字（Number）
> 	* 字符串（String） 必须使用双引号
> 	* 布尔值（Boolean）
> 	* 空值（Null）
> 	* 对象（Object {}）
> 	* 数组（Array \[]）



```
// 利用json完成深复制，将对象转换成字符串，再将字符串转换成一个新对象
const strUser = JSON.stringify(user)
const objUser = JSON.parse(strUser)

```

#### Map



> Map用来存储键值对结构的数据（key\-value）
> 
> 
> Object中存储的数据就可以认为是一种键值对结构



> Map和Object的主要区别：
> 
> 
> * Object中的属性名只能是字符串或符号，如果传递了一个其他类型的属性名，JS解释器会自动将其转换为字符串
> * Map中任何类型都可以称为数据的key


##### map的使用



```
const info = new Map()

// 设置键值对
info.set("name","l")
info.set({},"a")
info.set(NaN,"b")

console.log(info)  // Map(3) { 'name' => 'l', {} => 'a', NaN => 'b' }

// 当前map大小
console.log(info.size) // 3


// 获取map的所有的key
console.log(info.keys())  // [Map Iterator] { 'name', {}, NaN }


// 获取map所有的value
console.log(info.values()) // [Map Iterator] { 'l', 'a', 'b' }


// 检查map是否包含指定key，包含true否则false
console.log(info.has(NaN)) // true

// 通过key获取指定元素
console.log(info.get("name"))  // l

// 删除元素
info.delete("name")
console.log(info)  // Map(2) { {} => 'a', NaN => 'b' }

// 清空map
info.clear()
console.log(info)  // Map(0) {}



```

##### map的转换



```
const info = new Map()

info.set("name","l")
info.set({},"a")
info.set(NaN,"b")

// 使用Array.from将 map转换为数组
const arr = Array.from(info)
console.log(arr)  // [ [ 'name', 'l' ], [ {}, 'a' ], [ NaN, 'b' ] ]


```


```
const arr = [["name",1],["age",2]]

// 将二维数组转换为map
const map = new Map(arr)
console.log(map) // Map(2) { 'name' => 1, 'age' => 2 }


```

##### 遍历map



```

const info = new Map()

info.set("a",1)
info.set("b",2)


// 方式一
for (const entry of info){
    const [key,value] = entry
    console.log(key,value)
}

for (const [key,value] of info){
    console.log(key,value)
}

// 方式二

info.forEach((key,value)=>{
    console.log(key,value)
})

```

#### Set


* Set用来创建一个集合
* 它的功能和数组类似，不同点在于Set中不能存储重复的数据



```

// 创建集合
const set = new Set()


// 添加数据,如果集合中已经存在要添加的元素，则不会添加
set.add("a")
set.add("b")


// 获取集合的大小
console.log(set.size) // 2

// 检查集合中是否包含指定元素，包含true否则false
console.log(set.has("a")) // true


// 读取指定元素-需要将set转换成数组，然后通过下标读取
const arr = [...set]
console.log(arr[0]) // a

// 删除元素
set.delete("b")

//  遍历集合
for (const v of set){
    console.log(v)
}


```


```
// 通过数组创建集合，基于集合元素的唯一性，会对数组进行去重

const arr = [1,2,3,4,4,1,1,5]

const set =  new Set(arr)
console.log(set) // Set(5) { 1, 2, 3, 4, 5 }


```

#### Math


Math是一个工具类，提供了数学运算的一些常量和方法


[用法大全](https://github.com)



```

// 常量 圆周率
console.log(Math.PI)  // 3.141592653589793

// 求一个数的绝对值
console.log(Math.abs(-123))  // 123

// 求多个值中的最小值
console.log(Math.min(1, 2, 3))  // 1

// 求多个值中的最大值
console.log(Math.max(1,2,3))  // 3

// 求指定数值的幂次方
console.log(Math.pow(2,3)) // 8

// 求一个数的平方根
console.log(Math.sqrt(4)) // 2

// 向下取整
console.log(Math.floor(1.5)) // 1

// 向上取整
console.log(Math.ceil(1.5)) // 2

// 四舍五入取整
console.log(Math.round(3.5)) // 4

// 去除小数位
console.log(Math.trunc(3.5)) // 3

// 生成0~1之间的随机浮点数，不包含0和1
console.log(Math.random()) // 0.11258771607929718

// 生成 0~5之间的随机整数
// Math.random范围 是0~1，*5将范围扩大5倍 0~5 默认不包含0和5，然后四舍五入，根据四舍五入包含0和5
console.log(Math.round(Math.random() * 5))

// 生成 x ~ y 任意范围的随机数
/*
1~6之间的随机数
范围扩大5倍，是0~5，然后+1是1~6，得出随机小数后四舍五入，包含1和6
*/
console.log(Math.round(Math.random() * 5 + 1))


// 11~20之间的整数
// [0,1] -> [0,9] -> [0+11,9+11]
// 先写+号后面的部分，11，,20-11=9
console.log(Math.round(Math.random() * 9 + 11))


// 根据 四舍五入、取证等方法的规则，来决定左右数值是否包含


```

#### Date


在JS中所有的和时间相关的数据都由Date对象来表示


[用法大全](https://github.com):[樱花宇宙官网](https://yzygzn.com)


##### Date使用



```

// 创建当前的时间的对象
let date = new Date()
console.log(date) // 2024-10-30T10:48:29.454Z

// 创建指定时间对象-年,月(从下标0开始),日,时,分,秒,毫秒
date = new Date(2024,9,30,13,13,13,13)
console.log(date) // 2020-01-01T05:13:13.000Z

// 创建指定时间的对象-通过时间字符串-年-月-日 时:分:秒
date = new Date("2024-10-30 12:00:00")
console.log(date) // 2024-10-30T04:00:00.000Z

// 创建指定时间的对象-通过时间戳
date = new Date(1730265193013)
console.log(date) // 2024-10-30T05:13:13.013Z




// 获取时间对象的年份
console.log(date.getFullYear())
// 获取时间对象的月份-返回的是月份的索引，索引从0开始
console.log(date.getMonth())
// 获取时间对象的日
console.log(date.getDate())
// 获取日期对象是周几（0-6） 0表示周日
console.log(date.getDay())
// 返回当前日期对象的时间戳
console.log(date.getTime())

// 返回当前时间的时间戳
console.log(Date.now())

```

##### Date格式化



```
let date = new Date()


// 将日期转换为本地时间格式字符串
let time = date.toLocaleDateString()
console.log(time)  // 10/31/2024

// 将时间转换为本地时间格式字符串
time = date.toLocaleTimeString()
console.log(time) // 10:32:05 AM

// 日期时间转换为本地时间格式字符串
time = date.toLocaleString()
console.log(time) // 10/31/2024, 10:32:50 AM

// 日期时间转换为指定地区、格式字符串-指定国家时间
time = date.toLocaleString(
    "en-US", // 指定语言和国家
    {dateStyle: "full", timeStyle: "full"}
    //                             dateStyle 日期的风格
    //                             timeStyle 时间的风格
    //                                 full
    //                                 long
    //                                 medium
    //                                 short
    //                             hour12 是否采用12小时值
    //                                 true
    //                                 false
    //                             weekday 星期的显示方式
    //                                 long
    //                                 short
    //                                 narrow
    //
    //                             year
    //                                 numeric
    //                                 2-digit


)
console.log(time)

```

#### 包装类


在JS中，除了直接创建原始值外，也可以创建原始值的对象



```
//         通过 new String() 可以创建String类型的对象
//         通过 new Number() 可以创建Number类型的对象
//         通过 new Boolean() 可以创建Boolean类型的对象

//         注意:千万不要这么做,通过该方式创建的是对象，无法与原始值做比较

let str = new String("hello world")
let num = new Number(10)
let bool = new Boolean(true)
num.max = 100 // 给num对象设置属性

console.log(str) // [String: 'hello world']
console.log(num) // [Number: 10]
console.log(num.max) // 100 
console.log(bool) // [Boolean: true]

console.log(num === 10) // false

```

包装类：



> * JS中一共有5个包装类
> * String \-\-\> 字符串包装为String对象
> * Number \-\-\> 数值包装为Number对象
> * Boolean \-\-\> 布尔值包装为Boolean对象
> * BigInt \-\-\> 大整数包装为BigInt对象
> * Symbol \-\-\> 符号包装为Symbol对象



> 通过包装类可以将一个原始值包装为一个对象
> 
> 
> 当我们对一个原始值调用方法或属性时，JS解释器会临时将原始值包装为对应的对象,然后调用这个对象的属性或方法



```

// 原始值
let str = "hello world"

// 给原始值添加属性，会将原始值转换为一次性临时的原始值对象
str.name = "11111"
// 赋值和读取两次调用str.name,是两次临时的原始值对象，无法通过该方法读取
console.log(str.name) // undefined



let num = 100
// 原始值number是没有方法的，当调用方法时，将num临时的转为number对象，调用number对象的toString方法
num = num.toString()

```

由于原始值会被临时转换为对应的对象，这就意味着原始值对象中的方法都可以直接通过原始值来调用



```
// 字符串的本质是一个字符数组, hello-->["h","e","l","l","0"]

let str = "hello"

// 可以通过操作数组的一些方法去操作字符串

// 索引读取字符-不可以负索引
console.log(str[0]) // h
// 遍历字符串
for (let char of str){
    console.log(char)
}
// 获取字符串长度
console.log(str.length) // 5

// 根据索引获取字符串，可以接受负数索引
console.log(str.at(-1)) // o

// 索引读取字符-不可以负索引
console.log(str.charAt(0)) // h

// 用来连接两个或者多个字符串,返回一个新字符串
console.log(str.concat(" world"," !")) // hello world !


// 检查字符串中是否包含某个内容，返回true或者false
console.log(str.includes("ll")) //检测全部字符串 true
console.log(str.includes("h",2)) // 从下标2开始检测  false

// 检查指定字符第一次出的位置
console.log(str.indexOf("l")) // 2

// 检查指定字符最后一次出现的位置
console.log(str.lastIndexOf("l")) // 3

// 检查字符串是否以指定内容开头
console.log(str.startsWith("he")) // true

// 检查字符串是否以指定内容结尾
console.log(str.endsWith("o")) // true

// 给字符串补位 如果字符串长度不够指定长度，从开头开始补，返回一个新字符串,不指定补位字符，则默认是空
console.log(str.padStart(7,"0")) // 00hello
// 给字符串补位 如果字符串长度不够指定长度，从结尾开始补0，返回一个新字符串
console.log(str.padEnd(8,"0")) // hello000

// 使用一个新字符串替换字符串中的一个指定内容，返回一个新字符串
console.log(str.replace("l","a")) // healo


// 使用一个新字符串替换所有指定内容，返回一个新字符串
console.log(str.replaceAll("l","a")) // heaao

// 对字符串进行切片,左闭右开
console.log(str.slice(1,3)) // el

// 截取字符串，左闭右开
console.log(str.substring(1,3)) // el

// 将一个字符串拆分为一个数组,参数指定以什么字符间隔拆分
console.log(str.split("")) // [ 'h', 'e', 'l', 'l', 'o' ]

// 将字符串转换为小写
console.log(str.toLowerCase()) // hello

// 将字符串转换为大写
console.log(str.toLocaleUpperCase()) // HELLO

// 去除首尾空格
console.log(str.trim())

// 去除开始空格
console.log(str.trimStart())

// 去除结束空格
console.log(str.trimEnd())


```

#### 正则表达式



> * 正则表达式用来定义一个规则
> * 通过这个规则计算机可以检查一个字符串是否符合规则或者将字符串中符合规则的内容提取出来
> * 正则表达式也是JS中的一个对象，所以要使用正则表达式，需要先创建正则表达式的对象


##### 创建正则表达式对象



```
// 通过构造函数创建正则表达式对象，RegExp() 接收两个字符串参数 1.正则表达式 2.匹配模式
// 字符串转义原因，表达式编写注意转义
let regObj = new RegExp("\\w","i")


// 使用字面量创建一个正则表达式对象, /正在表达式/匹配模式
// 字面量创建不用考虑转义问题
let reg = /\w/i


let reg2 = new RegExp("a")
// test方法:get定的字符串str中测试是否存在与正则表达式re匹配的部分
console.log(reg2.test("abc")) // 字符串str 表达式a  str中包含a   返回true

```

##### 正则表达式语法



```

// 在正则表达式中大部分字符都可以直接写
// | 在正则表达式中表示或

// 字符串是否有abc或者bcd
let re = /abc|bcd/



// [] 表示字符集

// 字符串是否包含字符集里面的任意字母，等同于 a | b | c
re = /[abc]/

// 任意的小写字母
re = /[a-z]/

// 任意的大写字母
re = /[A-Z]/

// 任意的大小写字母
re = /[a-zA-Z]/

// 任意的数字
re = /[0-9]/


// [^]表示排除

// 除了a以外的任意字符
re = /[^a]/

// .表示除了换行以外的任意字符 ,如果想匹配. 需要转义 /\./
re = /./

// 其他字符集

// 任意的单词字符 [A-Za-z0-9_]
re = /\w/

// 排除单词字符  [^A-Za-z0-9_]
re = /\W/

// 任意数字 [0-9]
re = /\d/

// 排除数字 [^0-9]
re = /\D/

// 空格
re = /\s/

// 排除空格
re = /\S/

// 单词边界
re = /\b/

// 排除单词边界
re = /\B/

// 开头和结尾,^表示字符串的开头，$表示字符串的结尾

// 匹配开始位置的a
re = /^a/

// 匹配结束位置的a
re = /a$/

// 匹配字幕a，完全匹配，字符串和正则完全一致
re = /^a$/

```

##### 量词



```


// 3个a
let re = /a{3}/

// 至少3个a
re = /a{3,}/

// 3~6个a
re = /a{3,6/

// 多字符匹配:两次匹配只对量词前面的一个字符生效，比如 /ab{3}/,只会检测b，不会检测ab，如果要检测ab，需要使用()
re = /(ab){3}/


//  开头任何个小写字母
re = /^[a-z]{3}/


// + 表示一个以上，等同于{1,}
re = /a+/

// *表示任意数量
re = /a*/

// ?表示0-1次  等同于{0,1}
re = /a?/



```

##### 正咋表达式匹配模式


1. 默认（贪婪模式）
	* 在 JavaScript 正则表达式中，默认情况下量词（如`*`、`+`、`?`）是贪婪的。这意味着它们会尽可能多地匹配字符。
	* 例如，对于正则表达式`/a.*b/`和字符串`"aabbbc"`，它会匹配从第一个`a`到最后一个`b`的整个字符串，即`"aabbbc"`。因为`.*`会尽可能多地匹配中间的字符，直到遇到最后一个`b`。
2. 非贪婪模式（懒模式）
	* 通过在量词后面添加`?`可以将其转换为非贪婪模式。在非贪婪模式下，量词会尽可能少地匹配字符。
	* 例如，对于正则表达式`/a.*?b/`和字符串`"aabbbc"`，它会匹配`"aab"`。因为`.*?`会在遇到第一个`b`时就停止匹配，只匹配最少的字符来满足表达式。
3. 全局匹配模式（`g`）
	* 当在正则表达式末尾添加`g`标志（如`/pattern/g`）时，它会进行全局匹配。这意味着会在整个字符串中查找所有匹配的部分，而不是只找到第一个匹配就停止。
	* 例如，对于正则表达式`/a/g`和字符串`"aaab"`，它会匹配所有的`a`，返回一个包含三个`a`的数组（在使用`match`方法时）。如果没有`g`标志，只会返回第一个`a`。
4. 不区分大小写匹配模式（`i`）
	* 在正则表达式末尾添加`i`标志（如`/pattern/i`）会使匹配不区分大小写。
	* 例如，对于正则表达式`/a/i`和字符串`"Aa"`，它会匹配`A`，因为不区分大小写。
5. 多行匹配模式（`m`）
	* 当添加`m`标志（如`/pattern/m`）时，`^`和`$`的匹配行为会发生改变。`^`不仅可以匹配字符串开头，还可以匹配每一行的开头；`$`不仅可以匹配字符串结尾，还可以匹配每一行的结尾。
	* 例如，对于正则表达式`/^a/m`和字符串`"a\nb"`，它会匹配第一行开头的`a`，如果没有`m`标志，它只会匹配整个字符串开头的`a`，对于这个例子就不会匹配


##### 正则表达式提取


exec()用于获取字符串中符合正则表达式的内容



```
let str = "abc123bcc456cbdd"


let re = /\d+/ig


// '123'是本次匹配到的结果，index是匹配到的字符串在原始输入字符串中的起始索引位置是 3，input是原始字符串，group是组
console.log(re.exec(str)) // [ '123', index: 3, input: 'abc123bcc456cbdd', groups: undefined ]
console.log(re.exec(str)) // [ '456', index: 9, input: 'abc123bcc456cbdd', groups: undefined ]
// 每调用一次只会匹配一次，调用多次会依次向后匹配，为null说明匹配结束没有了
console.log(re.exec(str)) // null



// 使用()可以进行分组

str = "abcadcacc"

// 匹配a*c，使用()把中间的字符分组
re = /a([a-z])c/

// abc是本次匹配到的内容，b是分组内的内容
console.log(re.exec(str)) // [ 'abc', 'b', index: 0, input: 'abcadcacc', groups: undefined ]


```

##### 字符串的正则方法



```
let str = "llaacqqabcccaccdd"
// 可以根据正则表达式来对一个字符串进行拆分

console.log(str.split(/a[a-z]c/)) // [ 'll', 'qq', 'cc', 'dd' ]

// 根据正则表达式替换字符串中的指定内容
console.log(str.replace(/a[a-z]c/g,"@")) // ll@qq@cc@dd


// 可以去搜索符合正则表达式的内容第一次在字符串中出现的位置
console.log(str.search(/a[a-z]c/)) // 2

// 根据正则表达式去匹配字符串中所有符合要求的内容
console.log(str.match(/a/g)) // [ 'a', 'a', 'a', 'a' ]


// 根据正则表达式去匹配字符串中符合要求的内容(必须设置g 全局匹配),返回的是一个迭代器
console.log(str.matchAll(/a/g)) // Object [RegExp String Iterator] {}



```

#### 垃圾回收机制



> * 如果一个对象没有任何的变量对其进行引用，那么这个对象就是一个垃圾对象
> * 垃圾对象的存在，会严重的影响程序的性能
> * 在JS中有自动的垃圾回收机制，这些垃圾对象会被解释器自动回收，我们无需手动处理
> * 对于垃圾回收来说，我们唯一能做的事情就是将不再使用的变量设置为null



```
let obj = { value: 1 };
let anotherObj = obj;  // obj的引用次数增加到2
obj = null;            // obj的引用次数减少到1
anotherObj = null;     // obj的引用次数减少到0，可被垃圾收集器回收


```

