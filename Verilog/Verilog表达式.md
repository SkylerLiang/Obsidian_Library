# 表达式

表达式由操作符和操作数构成，其目的是根据操作符的意义得到一个计算结果。表达式可以在出现数值的任何地方使用。例如：

```Verilog
a^b ;          //a与b进行异或操作
address[9:0] + 10'b1 ;  //地址累加
flag1 && flag2 ;  //逻辑与操作
```

# 操作数

操作数可以是任意的数据类型，只是某些特定的语法结构要求使用特定类型的操作数。

操作数可以为常数，整数，实数，线网，寄存器，时间，位选，域选，存储器及函数调用等。

```Verilog
module test;

//实数
real a, b, c;
c = a + b ;

//寄存器
reg  [3:0]       cprmu_1, cprmu_2 ;
always @(posedge clk) begin
        cprmu_2 = cprmu_1 ^ cprmu_2 ;
end
         
//函数
reg  flag1 ;
flag = calculate_result(A, B);
 
//非法操作数
reg [3:0]         res;
wire [3:0]        temp;
always@ （*）begin
    res    = cprmu_2 – cprmu_1 ;
    //temp = cprmu_2 – cprmu_1 ; //不合法，always块里赋值对象不能是wire型
end

endmodule
```

# 操作符

Verilog 中提供了大约 9 种操作符，分别是算术、关系、等价、逻辑、按位、归约、移位、拼接、条件操作符。

大部分操作符与 C 语言中类似。同类型操作符之间，除条件操作符从右往左关联，其余操作符都是自左向右关联。圆括号内表达式优先执行。例如下面每组的 2 种写法都是等价的。

```Verilog
//自右向左关联，两种写法等价
A+B-C ;
(A+B）-C ;

//自右向左关联，两种写法等价，结果为 B、D 或 F
A ? B : C ? D : F ;
A ? B : (C ? D : F) ;

//自右向左关联，两种写法不等价
(A ? B : C) ? D : F ;  //结果 D 或 F
A ? B : C ? D : F ; //结果为 B、D 或 F
```

不同操作符之间，优先级是不同的。为了避免由操作符优先级导致的计算混乱，在不确定优先级时，建议用圆括号将表达式区分开来。

# 算数操作符

算术操作符包括单目操作符和双目操作符。

双目操作符对 2 个操作数进行算术运算，包括乘（\*）、除（/）、加（+）、减（-）、求幂（\*\*）、取模（%）。

```Verilog
reg [3:0]  a, b;
reg [4:0]  c ;
a = 4'b0010 ;
b = 4'b1001 ;
c = a+b;        //结果为c=b'b1011
c = a/b;          //结果为c=4，取整
```

如果操作数某一位为 X，则计算结果也会***全部***出现 X。例如：

```Verilog
b = 4'b100x ;
c = a+b ;       //结果为c=4'bxxxx
```

对变量进行声明时，要根据变量的操作符对变量的位宽进行合理声明，不要让结果溢出。上述例子中，相加的 2 个变量位宽为 4bit，那么结果寄存器变量位宽最少为***5bit***。否则，高位将被截断，导致结果高位丢失。

> 无符号数乘法时，结果变量位宽应该为 2 个操作数位宽之和。

