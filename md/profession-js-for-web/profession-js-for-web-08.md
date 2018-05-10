- Function类型
    - 每个函数本质上都是Function类型的实例（即对象） => 函数本质是对象。
        - 引申问题：在js中，类型不也是对象吗？
    - 函数名实际上只是一个指向函数对象的指针（变量名） => 函数名本质是指针变量。因此函数名其实和其他包含对象指针的变量没有什么不同
        - 函数名和函数本身没有绑定 --> js没有重载
        - 所有引用类型值不都是指针吗？理解里最初C语言定义的指针就是保存地址的变量
    - 创建函数（函数定义）：
        - 函数声明
        - 函数表达式
        - 使用Function构造函数（不推荐）
    - 函数声明 vs 函数表达式
        - 解析器在向执行环境中加载数据时，会先读取函数声明，使其在执行任何代码之前可用。
        - 即在代码执行之前，，解析器会通过函数声明提升，function declaration hoisting，读取并将函数声明添加到执行环境中。
    - 作为值的函数
        - 函数名本身就是变量，所以函数也可以作为值来使用
            - 函数作为参数传递
            - 函数作为值返回
    - 函数**内部**属性（并不是函数的属性）
        - arguments：类数组对象，主要用于保存函数参数
            - arguments.callee：指向拥有这个arguments对象的函数 => 解除函数名与函数紧耦合
            - this：引用的是函数据以**执行**的**环境对象**
                - 在调用函数前（执行），this的值并不确定
                - 但是无论this的值是什么，调用的函数 因为函数名仅仅是一个变量而已，因此无论在哪个环境中执行，都是指向的同一个函数。
    - 函数对象属性
        - caller：调用当前函数 的 **函数**的引用（在全局作用域下值为null）
    - 函数的属性与方法
        - length：函数希望接收的命名参数的个数
        - prototype：
            - 对于ECMAScript引用类型而言，prototype是保存它们所有实例方法的真正所在。
            - toString()和valueOf()等方法，实际上都保存在prototype名下，只不过通过各自的对象实例访问。（函数其实都是同一个）
            - 在创建自定义引用类型和实现继承时，prototype属性的作用是**极其重要**的。
            - 在ECMAScript 5 中，prototype属性是**不可枚举**的，因此使用for-in无法发现。
        - 非继承而来的方法（函数类型才有的方法，Object类型没有）:
            - apply()和call()，作用都是**在特定的作用域中调用函数**，即相当于设置函数体内this对象的值。
            - 真正强大之处在于：**扩充函数赖以运行的作用域**。最大好处在于：**对象不需要与方法有任何耦合关系**。
            - 均接收两种参数：一个是在其中运行函数的作用域，即this，另一个是传递的参数。两者区别在于第二个参数传递的方式不同，前者是参数数组（也可以是arguments对象），后者是参数的逐一传入
        - bind()：会创建一个函数的实例，其中this值会被绑定到传给bind()函数的参数值
    - 继承方法
        - toString()、toLocaleString()、valueOf()返回函数代码，表现各异