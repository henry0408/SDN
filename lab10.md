# lab10

上周介绍了header和paser，这周介绍剩下的内容

In this lab, we will continue to study the P4 language, learn the other three components of the P4 language, and complete the ‘basic.p4’ file:
* Control
* Tables
* Actions

# Control Block
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

## 1. P4 Programming-Tables

P4 tables contain the state used to forward packets. Tables are composed of lookup keys and a corresponding set of actions and their parameters. \
P4表包含用于转发数据包的状态。表由查找键和相应的动作及其参数组成

A trivial example might be to store a set of destination MAC addresses as the lookup keys, and the corresponding action could set the output port on the device, and/or increment a counter. \
一个简单的例子可能是将一组目标MAC地址存储为查找键，并且相应的操作可以设置设备上的输出端口，并/或增加一个计数器。

Tables and their associated actions are almost always chained together in sequence to realize the full packet forwarding logic, although in the abstract it is 
possible to build a single table that includes all the lookup key information and the full output action set\
表及其相关的操作几乎总是按顺序链接在一起，以实现完整的数据包转发逻辑，尽管在抽象中，可以构建一个包含所有查找键信息和完整的输出操作集的单一表




