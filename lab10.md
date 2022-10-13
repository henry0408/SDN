# lab10

上周介绍了header和paser，这周介绍剩下的内容

In this lab, we will continue to study the P4 language, learn the other three components of the P4 language, and complete the ‘basic.p4’ file:
* Control
* Tables
* Actions

# 1. Control Block
P4 parsers are responsible for extracting bits from a packet into headers. These headers (and other metadata) can be manipulated and transformed within control blocks. \
P4解析器负责从一个数据包中提取比特到头文件中。这些头文件（和其他元数据）可以在控制块中进行操作和转换。

The body of a control block resembles a traditional imperative program. Within the body of a control block, match-action units can be invoked to perform 
data transformations. \
控制块的主体类似于传统的命令式程序。在控制块的主体中，可以调用匹配动作单元来执行数据转换。

Match-action units are represented in P4 by constructs called tables.\
来执行数据转换。匹配动作单元在P4中由被称为表的构造来表示

Syntactically, a control block is declared with a name, parameters, optional type parameters, and a sequence of declarations of constants, variables,
actions, tables, and other instantiations.\
从语法上讲，控制块由名称、参数、可选类型参数以及常量、变量、操作、表和其他实例化的一系列声明来声明。


In this lab, we need to declare parameters, tables, actions and call the ‘apply’ methodto invoke a ‘table’ \
在这个实验室中，我们需要声明参数、表、操作，并调用“apply”方法来调用一个“表”

(Calling an apply method on a table instance returns a value with a struct type with three fields. This structure is synthesized by the compiler automatically.)
(对表实例调用应用方法返回带有三个字段的结构类型的值。这个结构是由编译器自动合成的。)


![image](https://user-images.githubusercontent.com/58734009/195614195-848a7666-3b8c-49cf-bdf9-d30ee3fcb89d.png)









