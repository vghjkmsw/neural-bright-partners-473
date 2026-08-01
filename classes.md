# JavaScript：类与面向对象



## 说明

ES6 class 语法，继承、getter/setter、静态方法、私有字段。



## 代码

```html

<!DOCTYPE html>

<html lang="zh">

<head><meta charset="UTF-8"><title>JS 类</title></head>

<body>

<h2>🏗 JavaScript 类与面向对象</h2>

<pre id="out" style="background:#f5f5f5;padding:15px;font-family:monospace"></pre>

<script>

const out = document.getElementById("out");

function log(msg) { out.textContent += msg + "\n"; }



// ====== 基类 ======

class Animal {

    constructor(name) {

        this.name = name;

    }



    speak() {

        return `${this.name} 发出声音`;

    }



    // getter

    get description() {

        return `动物: ${this.name}`;

    }



    // 静态方法

    static isAnimal(obj) {

        return obj instanceof Animal;

    }

}



// ====== 继承 ======

class Dog extends Animal {

    constructor(name, breed) {

        super(name);  // 必须先调用 super()

        this.breed = breed;

    }



    speak() {

        return `${super.speak()}，汪汪！`;  // 调用父类方法

    }



    fetch() {

        return `${this.name} 去捡球了`;

    }

}



// ====== 使用私有字段 (ES2022+) ======

class BankAccount {

    #balance = 0;  // 私有字段



    constructor(owner, initialDeposit) {

        this.owner = owner;

        this.#balance = initialDeposit;

    }



    deposit(amount) {

        if (amount <= 0) throw new Error("金额必须为正");

        this.#balance += amount;

        return this.#balance;

    }



    withdraw(amount) {

        if (amount > this.#balance) throw new Error("余额不足");

        this.#balance -= amount;

        return this.#balance;

    }



    get balance() {

        return this.#balance;  // 只读访问

    }

}



// ====== Mixin 模式（多继承模拟） ======

const FlyingMixin = Base => class extends Base {

    fly() {

        return `${this.name} 在飞！`;

    }

};



class Bird extends FlyingMixin(Animal) {

    speak() { return `${this.name} 啾啾！`; }

}



// ====== 测试 ======

const dog = new Dog("旺财", "金毛");

log(dog.speak());

log(dog.fetch());

log(dog.description);

log(`是动物吗: ${Animal.isAnimal(dog)}`);



const bird = new Bird("小鸟");

log(bird.fly());

log(bird.speak());



const account = new BankAccount("小明", 1000);

log(`余额: ${account.balance}`);

account.deposit(500);

log(`存入 500 后: ${account.balance}`);

try {

    account.withdraw(2000);

} catch (e) {

    log(`❌ 取款失败: ${e.message}`);

}

// log(account.#balance);  // ❌ 访问私有字段报错

</script>

</body>

</html>

```



## 教学重点

- `class` 本质是原型链的语法糖

- `extends` 继承，`super()` 调用父类构造器

- getter `get` 让方法像属性访问，setter `set` 校验赋值

- `static` 方法属于类本身不属于实例

- `#name` (Hash Names) 是真正的私有字段



## 常见错误

- 子类构造器忘记 `super()` 调用

- 私有字段名不匹配（`#a` ≠ `#A`）

- 把方法当属性赋值覆盖 getter/setter

- `this` 指向问题：在回调中 `this` 可能变成 `undefined`

