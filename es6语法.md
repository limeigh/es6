#vue中常用的es6语法总结
##1.0 利用import ... from ...替代require()
	第一种方式: 导入一个css文件,不接收对象
	es5写法: require('site.css')
	es6写法: import 'site.css'

	第二种方式: 导入一个js模块并且要接收一个对象
	es5写法: var calc=require('calc.js')
	es6写法: import calc from 'calc.js'

	第三种方式: 只获取所暴露出的对象的某个方法(add方法)(按需获取)
	es6写法: import {add} from 'calc.js'

##2.0 导出对象变量的写法
	例:function add(){};function substrict(){}

	--第一种方式--
	es5的写法
	module.exports.add=add
	module.exports.substrict=substrict
	es6的写法
	export function add(){}
	export function substrict(){}
	//注意:export可以导出任何东西，例如导出一个常量export const PI=3.14
	//以上三种导入的话可以使用 import {add,substrict,PI}这种方式导入
	--第二种方式--
	es5的写法:
	module.exports={
		add:add,
		substrict:substrict
	}

	es6的写法:
	module.exports={
		add,
		substrict
	}
	或者
	export default{
		add,substrict
	}//注:这种方式导出的不支持 import {add} from './calc.js'导入

	注意点,这种写法必须是属性名和属性值变量是同一个,否则要分开写:
	module.exports={
		addFn:add,
		substrict
	}

##3.0 导出对象方法的写法
	es5的写法:
	module.exports={
		addFun:function(x,y){
			return x + y
		}
	}

	es6的写法:
	module.exports={
		addFun(x,y){
			return x+y
		}
	}


## 用export 和import 的写法注意点
	```
	1、如果模块中是使用 export default {} 方式导出的对象
	    只能通过  import 对象名称 from '模块路径'
	    不能通过  import {对象名称} from '模块路径'


	2、如果就想要import {对象名称} from '模块路径'通过这种方式来按需导入对象中的某个属性
	那么应该使用 export 跟着要导出的对象或者方法名称
	    export function add(){}
	    export function substrct(){}

	    那么就可以使用：
	    import {add,substrct} from '模块路径'
	    只需要直接使用 add()方法即可
	    注意这里不能直接使用：  import cacl from '模块路径' 这种方式导入，会报错
