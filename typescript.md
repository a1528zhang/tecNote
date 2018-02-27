# **typescrip笔记**

-----
**基本类型**：
- boolean
- number
- string
-  [  ]  （数组）
- tuple 元组：表示一个已知长度和类型的数组，数组的类型可以不同
- enum 枚举
- any 任意类型：编译的时候不会检查类型
- void 空值：void类型的变量只能赋undefined和null
- undefined
- null ： undefined和null是所有类型的子类，即任何类型都能赋值
- never ：是任何类型的子类型，表示的是那些永不存在的值的类型。返回为never的函数永远不会执行完毕，never end
- 断言 <string>someValue / someValue as string：类似于强制转换两种写法

**接口**：
    接口定义了方法参数的结构，也可以在接口中定义一个方法，然后用类实现，接口描述了类的公共部分。
- color?: string;  问号证明此属性可选
- readonly x:number : 只读属性，x在赋值后就不能修改了
- (source: string, subString: string): boolean; 函数类型：可以定义接口中函数的输入输出和返回值类型，比如这里要求输入是两个string，输出是boolean
- [index: number]: string; 可索引类型，证明实现这个接口的变量有索引
- 类类型，与java中的作用基本相同，可定义变量和方法，然后实现

**类**：
- 构造方法使用constructor声明
- Ts类中的成员默认为public的
- private： 不能在声明的类的外部访问，包括new a.b （b是private的）
- protected ：成员在派生类中仍然可以访问（extends）
- readonly ：只读属性必须在声明时或构造函数里被初始化
- 参数属性： 构造函数的参数加上修饰字就可以定义并初始化一个成员，例如：constructor(private name: string) {} new 后就可以 obj.name
- get/set : 关键字，用于存取私有属性
- static :静态关键字，与java相同
- abstract : 抽象关键字，和java中一样，抽象类中可以有具体方法，但是抽象方法必须要在子类中实现
- 重载： 与java相同，不同参数的同名函数不是同一个

**namespace**：
在文件内的代码块，如果没有导出，namespace外部无法访问内部的成员

**集成过程**:
- 安装typescript ts-loader @type/react 等依赖
- 在webpack配置文件中加入ts文件解析配置
```
{
        test: /\.(ts|tsx)$/,
        exclude: /node_modules/,
        loader: "ts-loader",
}
```
- 添加tsconfig.json文件 [配置项信息](https://www.tslang.cn/docs/handbook/compiler-options.html)
```
{
    "compilerOptions": {
        "noImplicitAny": true,
        "removeComments": true,
        "preserveConstEnums": true,
        "outFile": "../../built/local/tsc.js",
        "sourceMap": true,
        "target": "es5",
        "jsx": "react",
    },
    "include": [
        "src/**/*"
    ],
    "exclude": [
        "node_modules",
        "**/*.spec.ts"
    ]
}
```

**遇到的问题**:
- Property 'find' does not exist on type 'number[]' 数组无法找到find方法，在tsconfig中的target加上es6，[解决方法](https://github.com/Microsoft/TypeScript/issues/6945)