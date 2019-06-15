调用一个对象上父对象的函数或方法

##### this关键词指向函数所在的当前对象

##### super指向的是当前对象的原型对象

```javascript
const person = {
	name:'jack'
}

const man = {
	sayName(){
		return super.name;
	}
}

Object.setPrototypeOf( man, person );

let n = man.sayName();

console.log( n )	//jack
```

