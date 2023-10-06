# 格式

Verilog区分大小写。格式自由，可以在一行内编写，也可以跨行编写。

每个语句以**分号**为结束符。

## 不换行（不推荐）

```Verilog
wire [1:0]  results ;assign results = (a == 1'b0) ? 2'b01 ： (b==1'b0) ? 2'b10 ： 2'b11 ;
```

## 换行

```Verilog
wire [1:0]  results ;
assign      results = (a == 1'b0) ? 2'b01 ：
            (b==1'b0) ? 2'b10 ：
                2'b11 ;
```
# 注释

Verilog有两种注释方式：

1. 用`//`进行单行注释

```Verilog
reg [3:0] counter ;  // A definition of counter register
```

2. 用`/*`与`*/`进行跨行注释

```Verilog
wire [11:0]  addr ;
/* 
Next are notes with multiple lines.
Codes here cannot be compiled.
*/
assign   addr = 12'b0 ;
```

# 标识符与关键字

标识符可以是任意一组字母、数字、`$` 符号和` _`符号的组合，但标识符的第一个字符必须是字母或者下划线，不能以数字或者美元符开始。

标识符区分大小写。

关键字是Verilog中预留的用于定义语言结构的特殊标识符。Verilog 中关键字全部为小写。

```Verilog
reg [3:0] counter ; //reg 为关键字， counter 为标识符
input clk; //input 为关键字，clk 为标识符
input CLK; //CLK 与 clk是 2 个不同的标识符
```

