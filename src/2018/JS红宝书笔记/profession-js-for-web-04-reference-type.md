## 引用类型
- 引用类型
    - 引用类型是一种数据结构，用于将数据和功能组织在一起。
    - 引用类型也常被称为“类”，但是并不妥当，因为 ECMAScript 不具备传统面向对象语言所支持的类和接口等基本结构。
    - 引用类型也常被称为“对象定义”，因为描述的是一类对象所具有的属性和方法。
- 引用的值（即**对象**）是引用类型的实例。
    - 使用`new`操作符后跟一个**构造函数**来创建。
    - 构造函数本身就是一个函数，只不过该函数是`出于创建新对象的目的而定义的函数`。

- Object 类型
    - 创建 Object 实例的方法
        - 使用`new`操作符后跟 Object 构造函数
        - **对象字面量**
            - **不会调用 Object 构造函数**
            - 属性名可以使用字符串（属性名可包含会导致语法错误的字符，或者关键字和保留字）
            - 一般函数通常使用对象字面量来封装多个可选参数，对必需值直接使用命名参数
    - 访问对象属性
        - 点表示法
        - 方括号
            - 属性需要使用字符串访问
            - 可以通过变量访问属性

- Array 类型
    - 创建数组实例的方法
        - 使用 Array 构造函数
        - 数组字面量表示法
            - 不会调用 Array 构造函数
    - 数组大小
        - 可**动态调整**
        - 可**写**
            - arr[arr.length] = xxx; // 往数组末尾新添项
    - 数组检测
        - arr instanceof Array; // 当有多个全局环境时存在不同版本的 Array 构造函数
        - Array.isArray(arr)
    - 转换方法
        - valueOf() -> 数组本身
        - toString() -> 数组的字符串表示（每个值的字符串表示拼接成了一个字符串，中间用逗号分隔）（此方法一般隐式调用居多）
        - toLocaleString() -> 一般同 toString()
        - join() -> 可以使用不同的分隔符来构建字符串（默认（=>不传或传入undefined）情况会用逗号分隔，传入空字符串才无分隔）
        - **类型转换有一种情况是某些函数接受特定类型的参数，会将参数转换为对应类型**
    - 栈方法（LIFO）
        - push()：可以接收任意数量的参数，逐个添加到数组末尾，并返回修改后的长度
        - pop()：从数组末尾移除最后一项，同时减少数组的 length 值，并返回移除的项
    - 队列方法（FIFO）
        - shift()：移除数组的第一项，并返回该项，同时数组长度减1
        - unshift()：在数组前端添加任意个项并返回新数组的长度
    - 重排序方法
        - reverse()：逆置，返回排序后的数组（影响原始数组）
        - sort()：按升序排列数组的项。会调用每个数组项的 toString() 方法再排序（即使是数值项），返回排序后的数组（影响原始数组）
            - 默认排序方式并不理想：可以理解为默认的sort()传入了一个比较函数，会将相邻项先做toString处理，再通过字符串比较的方法升序排列
            - 可接收一个比较函数作为参数
                - (a, b)
                    - <0，a比b“小”：a在b前（此时位置不变）
                    - =0，a和b“相等”：位置不变
                    - >0，a比b“大”：b在a前（换位置）
                - a和b传入到比较函数，根据“升序”排列
                - 对于数值类型/valueOf()方法会返回数值类型的对象类型，可以直接减法
            - sort()本质上是使用了什么排序算法？类似“冒泡”？https://segmentfault.com/q/1010000008506262
    - 操作方法
        - concat()：会先创建当前数组的一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。（不影响原始数组）
            - 不传递参数：返回当前数组的一个副本
            - 传递多个数组参数：每个数组的数组项逐一添加
            - 传递的不是数值：直接将其作为一项添加到数组末尾
        - slice()：基于当前数组中的一项或多项创建一个新数组。（不影响原始数组）由参数决定：
            - 传入一个参数：从该位置开始到当前数组末尾的所有项
            - 传入两个参数：从第一个参数位置（包含）开始到第二个参数位置（不包含）的项
                - 如果两个参数相同，则返回空数组（亲测）
            - 参数可为负数：位置 = 数组长度 + 负的参数
        - splice()：强大的数组方法，可最多传入2+x个参数，分别是：起始位置（1）, 要删除的项数（1）, 要插入的项<逐一传入>（n），根据不同传入情况可实现（影响原始数组）：
            - 删除：可以删除从任意位置开始任意项，只传入前两个参数
            - 插入：可以在任意位置插入任意项，参数均传，其中第二个参数为0（删除项数为0）
            - 替换：可以从任意位置替换任意几项为任意项，参数均传，其中第二个参数不为0
            ```javascript
                var colors = [“red”, “green”, “blue”];
                var removed = colors.splice(0,1); //remove the first item
                alert(colors); //green,blue
                alert(removed); //red - one item array
                removed = colors.splice(1, 0, “yellow”, “orange”); //insert two items at position 1
                alert(colors); //green,yellow,orange,blue
                alert(removed); //empty array
                removed = colors.splice(1, 1, “red”, “purple”); //insert two values, remove one
                alert(colors); //green,red,purple,orange,blue
                alert(removed); //yellow - one item array
            ```
    - 位置方法
        - 两个位置方法，均接收两个参数：要查找的项、查找起始位置（可选，可为负数）
            - indexOf()：从前往后
            - lastIndexOf()：从后往前
        - 返回要查找的项在数组中的位置，没有为-1
        - 比较方式为“全等比较===”
    - 迭代方法
        - 五个迭代方法，均接收两个参数：要在每一项上运行的函数、运行该函数的作用域对象（可选）。对数组中的每一项运行给定函数：
            - every()：如果该函数对每一项都返回true，则返回true
            - filter()：返回该函数会返回true的项组成的数组
            - forEach()：没有返回值
            - map()：返回每次函数调用的结果组成的数组
            - some()：如果该函数对任一项返回true，则返回true
            ```javascript
            var numbers = [1,2,3,4,5,4,3,2,1];
            var everyResult = numbers.every(function(item, index, array){
                return (item > 2);
            });
            alert(everyResult); //false

            var someResult = numbers.some(function(item, index, array){
                return (item > 2);
            });
            alert(someResult); //true

            var numbers = [1,2,3,4,5,4,3,2,1];
            var filterResult = numbers.filter(function(item, index, array){
                return (item > 2);
            });
            alert(filterResult); //[3,4,5,4,3]

            var numbers = [1,2,3,4,5,4,3,2,1];
            var mapResult = numbers.map(function(item, index, array){
                return item * 2;
            });
            alert(mapResult); //[2,4,6,8,10,8,6,4,2]

            var numbers = [1,2,3,4,5,4,3,2,1];
            numbers.forEach(function(item, index, array){
                //do something here
            });
            ```
            
    - 归并方法
        - 两个归并方法，都会迭代数组的所有项，然后构建一个最终返回的值。均接收两个参数：在每一项上调用的函数、作为归并基础的初始值（可选）
            - reduce()：从前往后
            - reduceRight()：从后往前
        - 第一个参数函数接收4个参数：前一个值、当前值、项的索引、数组对象。函数返回的任何值都会作为第一个参数自动传给下一项
        ```javascript
        var values = [1,2,3,4,5];
        var sum = values.reduce(function(prev, cur, index, array){
            return prev + cur;
        });
        alert(sum); //15

        var values = [1,2,3,4,5];
        var sum = values.reduceRight(function(prev, cur, index, array){
            return prev + cur;
        });
        alert(sum); //15
        ```

- Date类型
    - 创建一个日期对象：使用Date构造函数
        - 不传入参数 => 自动获得当前日期和时间
        - 传入该日期的毫秒数（从UTC时间1970年1月1日零时开始经过的毫秒数）,毫秒数获取方法
            - Date.parse()：接收一个**表示日期的字符串参数**（ECMA-262并没有定义应该支持哪些日期格式，因此会因实现而异，通常表现为因地区而异），然后尝试根据这个字符串返回相应日期的毫秒数。否则返回NaN。通常此过程在构造函数中可自动转化
            - Date.UTC()
    - Date.now()：返回调用这个方法时的日期和时间的毫秒数。**使用+操作符把Date对象转换为字符串**
    - 继承的方法
        - toLocaleString()
        - toString()
        - valueOf()：返回日期的毫秒表示 => 可以直接使用比较操作符来比较日期值
    - 日期格式化方法和日期/时间组件方法(复杂)
        - moment库：http://momentjs.cn/

- RegExp类型
    - 图形化正则表达式工具：https://regexper.com/
    - 创建正则表达式
        - 字面量
        - 构造函数
    - RegExp实例属性
        - global
        - ignoreCase
        - lastIndex
        - multiline
        - source
    - RegExp实例方法
        - exec()
        - test()
        - 继承的toString()和toString()会返回正则表达式的字面量
    - RegExp构造函数属性
        - “静态属性”
    
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

- 基本包装类型
    - 为了能（更方便）操作基本类型值，ECMAScript还提供了3个特殊的引用类型：Boolean、Number、String
    - 实际上，**每当读取一个基本类型值时，后台就会创建一个对应的基本包装类型的对象，从而能够调用一些方法来操作这些数据**，见下面代码演示：
    ```javascript
    // 对于这段代码
    var s1 = 'test';
    var s2 = s1.substring(2);

    // 其中第2句在执行过程中，对应可以细分为：
    var sTemp = new String('test'); // 创建String类型的一个实例
    var s2 = sTemp.substring(2);    // 在实例上调用指定的方法
    sTemp = null;   // 销毁这个实例
    ```
    - 引用类型与基本包装类型的主要区别就是：**对象的生存期**。
        - **使用new操作符创建**的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中。
        - **自动创建**的基本包装类型的对象，则只存在那行代码的执行瞬间，然后立即销毁。 => 不能在运行时为基本包装类型值添加属性和方法。
    - Object构造方法也会像**工厂方法**一样，根据传入值的类型返回相应基本包装类型的实例。例：`new Object('test')`，传入null和undefined会返回空对象
    - **使用new调用基本包装类型的构造函数**（返回相应的实例对象，理论上不支持这种方式，因为容易混淆处理的是基本类型值还是引用类型值，导致出现bug） 与 **直接调用同名的转型函数（返回基本类型值）** 是不一样的。
    - Boolean类型
        - 重写了valueOf()（返回true/false）
        - 重写了toString()和toLocaleString()（返回"true"/"false"）
    - Number类型
        - 重写了valueOf()、toString()和toLocaleString()
        - toFixed()
        - toExponential()
        - toPrecision()
    - String类型
        - 写了valueOf()、toString()和toLocaleString()
        - length属性
        - 字符方法
            - charAt()
            - charCodeAt()
            - 使用方括号加数值索引来访问字符串中的特定字符
        - 字符串方法
            - concat()：可接收多个参数，不影响原始字符串值。 => **拼接字符串**，在实际中更多使用**\+号**
            - 基于子字符串创建新字符串，不影响原始字符串值
                - slice()
                - substr()
                - substring()
            - 字符串位置方法
                - indexOf()
                - lastIndexOf()
            - trim()方法，不影响原始字符串值
                - trim()
                - trimLeft()
                - trimRight()
            - 字符串大小写转换方法
                - toLowerCase()、toLocalLowerCase()
                - toUpperCase()、toLocalUpperCase()
            - 字符串的模式匹配方法，等同于RegExp中的exec()方法
                - match()
                - search()
                - replace()
                - htmlEscape()
                - split()
            - localCompare()
            - 静态方法fromCharCode()
            - HTML方法（现在基本不用）
- 单体内置对象
    - 什么是内置对象？
        - 由ECMAScript实现提供的、不依赖于宿主环境的对象，这些对象在ECMAScript程序执行之前就已经存在了，例如Object、Array、String等
        - 不必实例化内置对象，因为它们已经实例化了
    - 两个单体内置对象：Global和Math
        - Global（全局）对象，理论上不属于任何其他对象的属性/方法最终都是Global的属性/方法，例如isNaN()、isFinite()、parseInt()、parseFloat()等
            - 还有：
                - URL编码方法
                    - encodeURI()、encodeURIComponent()
                    - decodeURI()、decodeURIComponent()
                - eval()：“代码注入”风险
            - Global对象的属性
                - 特殊的值：undefined、NaN、Infinity
                - 所有原声引用类型的构造函数
            - window：ECMAScript没有指出如何**直接访问**Global对象，但Window浏览器将这个全局对象作为window对象的**部分**实现。
        - Math对象
            - 属性：Math.E等常量
            - min()和max()方法
                - 接收任意多个数值参数
                - 如果是数组，可借助apply()方法，`Math.max.apply(Math, array)`，这样就可以找到数组的最大/小值
            - 舍入方法
                - ceil()：向上舍入为最接近的整数
                - floor()：向下舍入为最接近的整数
                - round()：四舍五入
            - random() => \[0, 1)
                - \[lowerValue, upperValue)
                - 第一个可能的值：lowerValue
                - 可能值的总数：upperValue - lowerValue + 1
                - 可能值是**连续**的
                - Math.floor(Math.random() * 可能值的总数 + 第一个可能的值
                - Math.floor(Math.random() * (upperValue - lowerValue + 1) + lowerValue)
            - 其他方法：Math.abs()等

- 引用类型小结
    - **对象**在JavaScript中被称为**引用类型的值**。
    - 引用类型与传统OOP中的类相似，但实现不同。（JavaScript能直接访问引用类型/类吗？是用对象来模拟的类？只是名称第一个大写？）
    - Object是一个基础类型，其他所有引用类型都从Object继承了基本的行为。（但使用Object.create(null)创建的对象未继承！是一个空白的对象。这里指的是对象，继承发生在类之间）
    - 基本类型值可以被作为对象来访问（Boolean、Number、String）
    - 每个包装类型都映射到同名的基本类型
    - 在读取模式下访问基本类型值，就会创建对应的基本包装类型的一个对象，从而方便了数据操作。
    - 操作基本类型值的语句一经执行完毕，就会立即销毁新创建的包装对象。
    - 在所有代码执行之前，作用域中就已经存在两个内置对象：Global和Math。（其他内置对象不存在？）