Math是 JavaScript 的原生对象，提供各种数学功能。Math对象是目前javaScript原生对象里唯一一个不是构造函数，不用实例化，所有的属性和方法都是直接在Math对象上调用。下面是本次分享的Math主要方法：

【一】Math.abs() 返回绝对值
【二】Math.ceil(),Math.floor() 向上取整和向下取整
【三】Math.max(),Math.min() 最大值和最小值
【四】Math.round() 四舍五入
【五】Math.random() 随机数
【六】Math.pow() 指数运算
【七】Math.sqrt() 平方根
【八】Math.log() 自然对数
【九】Math.exp() e的指数
【十】Math属性
【十一】Math三角函数


> Math.abs() 绝对值

Math.abs()方法，接收一个参数，返回这个参数的绝对值，通俗的讲就是把任何一个有效数字返回一个正数：
`
console.log(Math.abs(10))   // 输出 10
console.log(Math.abs(-10))  // 输出 10
复制代码
`

> Math.ceil(),Math.floor() 向上取整和向下取整

Math.ceil(),Math.floor()方法是获取整数的方法，接收一个参数，把小数点后面的数向上或者向下取一个整数。Math.ceil()是向上，Math.floor()是向下：
`
console.log(Math.ceil(10.01))   // 输出 11
console.log(Math.floor(10.01))  // 输出 10
复制代码
`

> Math.max(),Math.min() 最大值和最小值

Math.max(),Math.min()方法接收多个参数，并返回参数里数值最大或者最小的那个数，Math.max()是获取最大，Math.min()是获取最小：
`
console.log(Math.max(5, 1, 9, 3, 7))   // 输出 9
console.log(Math.min(5, 1, 9, 3, 7))  // 输出 1
复制代码
`
> Math.max(),Math.min()也可以用来获取数组里的最大数值和最小数值：
`
var arr = [5, 1, 9, 3, 7];
// 先看用循环实现方法,采用循环方式的核心思想就是假设法。
var max = 0, min = 1;
for (var num of arr) {
    if (max < num) {
		max = num
	}
	if (min > num) {
		min = num;
	}
}   // 输出 9, 1;
// 下面是采用apply改变this指向的方式直接获取最大值和最小值
console.log(Math.max.apply(null, arr))   // 输出 9
console.log(Math.min.apply(null, arr))  // 输出 1
复制代码
`

> Math.round() 四舍五入

Math.round()方法接收一个数字参数，对数字小数点后一位的数进行四舍五入处理
`
console.log(Math.round(3.87))   // 输出 4
console.log(Math.round(3.39))  // 输出 3
复制代码
`

> Math.random() 随机数

Math.random()方法返回一个0到1之间的随机数；
`
console.log(Math.random())   // 输出 0到1之间的随机数
复制代码
`
Math.random()是一个应用非常广泛的方法，下面看一个限定范围内的随机数：
`
function getRandom (min, max) {
	return	Math.round(Math.random()*(max - min))
}
console.log(getRandom(0, 100)); // 输出0到100的随机整数
复制代码
`
基于这个思想，可以做很多事情，比如随机取字符串里的值，随机取数组里的某个当前项等等。
`
var ary = ['red', 'orange', 'yellow', 'blue', 'green']
function getRandom (min, max) {
		 return	ary[Math.round(Math.random()*(max - min))]
	}
console.log(getRandom(0, ary.length-1)); // 输出数组里随机的一个当前项
复制代码
`

> Math.pow() 指数运算

Math.pow()方法返回以第一个参数为底数、第二个参数为幂的指数值。
`
console.log(Math.pow(2, 2)); // 输出4
// 等同于 2 ** 2
console.log(Math.pow(2, 3)); // 输出8
// 等同于 2 ** 3
复制代码
`

> Math.sqrt() 平方根

Math.sqrt()方法返回参数值的平方根。如果参数是一个负值，则返回NaN。
`
console.log(Math.sqrt(9)); // 输出3
console.log(Math.sqrt(-9)); // 输出NaN
复制代码
`

> Math.log()

Math.log方法返回以e为底的自然对数值。
`
console.log(Math.log(10)); // 输出 2.302585092994046
复制代码
`

Math.exp()

> Math.exp()方法返回常数e的参数次方。
`
console.log(Math.exp(1)); // 输出 2.7182818284590455
console.log(Math.exp(2)); // 输出 7.38905609893065
复制代码
`

Math属性


Math.E：常数e。
Math.LN2：2 的自然对数。
Math.LN10：10 的自然对数。
Math.LOG2E：以 2 为底的e的对数。
Math.LOG10E：以 10 为底的e的对数。
Math.PI：常数π。
Math.SQRT1_2：0.5 的平方根。
Math.SQRT2：2 的平方根

`
Math.E // 2.718281828459045
Math.LN2 // 0.6931471805599453
Math.LN10 // 2.302585092994046
Math.LOG2E // 1.4426950408889634
Math.LOG10E // 0.4342944819032518
Math.PI // 3.141592653589793
Math.SQRT1_2 // 0.7071067811865476
Math.SQRT2 // 1.4142135623730951
复制代码
`
注意Math的这些属性都是只读，不可以修改的。

Math三角函数


Math.sin()：返回参数的正弦（参数为弧度值）
Math.cos()：返回参数的余弦（参数为弧度值）
Math.tan()：返回参数的正切（参数为弧度值）
Math.asin()：返回参数的反正弦（返回值为弧度值）
Math.acos()：返回参数的反余弦（返回值为弧度值）
Math.atan()：返回参数的反正切（返回值为弧度值）

`
Math.sin(0) // 0
Math.cos(0) // 1
Math.tan(0) // 0
Math.sin(Math.PI / 2) // 1
Math.asin(1) // 1.5707963267948966
Math.acos(1) // 0
Math.atan(1) // 0.7853981633974483
复制代码
`

结语

Math对象本身是对js里的数字做数学处理的，里面有不少方法，相信肯定有不少同学看起来都蒙蔽，因为大家肯定和我一样把学的数学知识都还给老师了，^-^|,而且对于他的实际应用，也会觉得陌生，既然陌生，那么同学看来这篇文章后，就和我一起去复习初中的数学知识吧。提前预告下，下篇将分享一个实战案例，双色球。

