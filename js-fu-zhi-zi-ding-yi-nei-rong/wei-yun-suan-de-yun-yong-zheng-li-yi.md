---
description: 最近看到一位巨佬整理的关于位运算的总结，这里根据我的理解来记录整理
---

# 位运算的运用整理

###  **什么是位运算？**

    ****程序中的所有数在计算机内存中都是以二进制的形式储存的。位运算说穿了，就是直接对整数在内存中的二进制位进行操作。比如，and（&）运算本来是一个逻辑运算符，但整数与整数之间也可以进行and（&）运算。举个例子，6的二进制是110，11的二进制是1011，那么6 and 11的结果就是2，它是二进制对应位进行逻辑运算的结果（0表示False，1表示True，空位都当0处理）：

```cpp
          110
AND（&）  1011
———————————————————
          0010  –>  2
```

当然有人会说，这个快了有什么用，计算6 and 11没有什么实际意义啊。这一系列的文章就将告诉你，位运算到底可以干什么，有些什么经典应用，以及如何用位运算优化你的程序。



### **各种位运算的使用**

![&#x6765;&#x6E90;&#xFF1A;&#x767E;&#x5EA6;&#x767E;&#x79D1;&#xFF08;&#x6574;&#x4E2A;&#x767E;&#x79D1;&#x4E0A;&#x5B8C;&#x5168;&#x662F;Matrix67&#x5927;&#x795E;&#x7684;&#x535A;&#x5BA2;&#x5185;&#x5BB9;&#x590D;&#x5236;&#xFF09;](../.gitbook/assets/image%20%2828%29.png)

####   **** === 1. and（&）与 ===

   and（&）运算通常用于二进制取位操作，例如一个数 and 1的结果就是取二进制的最末位。**这可以用来判断一个整数的奇偶**，二进制的最末位为0表示该数为偶数，最末位为1表示该数为奇数



####    === 2. or（\|）或 ===

   or（\|）运算通常用于二进制特定位上的无条件赋值，例如**一个数or 1的结果就是把二进制最末位强行变成1**。如果需要把二进制最末位变成0，对这个数or 1之后再减一就可以了，其实际意义就是把这个数强行变成最接近的偶数。



####    === 3. xor（^）异或 === 

xor（^）运算通常用于对二进制的特定一位进行取反操作，因为异或可以这样定义：**0和1异或0都不变，异或1则取反**。或者更直白点，**异或判断其实是对每一位二进制数问：是不是相等**  
  
**xor（^）运算的逆运算是它本身**，也就是说两次异或同一个数最后结果不变，即\(a ^ b\) ^ b = a。  
  
xor（^）运算可以用于简单的加密，比如我想对我MM说1314520，但怕别人知道，于是双方约定拿我的生日19951211作为密钥。  
1314520 ^ 19951211= 19161267  
我就把20665500告诉MM。MM再次计算19161267^ 19951211的值  
19161267 ^ 19951211= 1314520  
得到1314520，于是她就明白了我的企图。

刚才不是说xor（^）的逆运算是它本身吗？于是我们就有了以下的使用方法：

```typescript
function swap(a:number,b:number){
    a = a ^ b
    b = a ^ b
    a = a ^ b
    return [a,b];
}
```

![](../.gitbook/assets/image%20%2826%29.png)

看起来很诡异但是实际使用起来非常巧妙，有兴趣的同学可以自己去试试看



####    === 4. not（~）非 ===

not（~）运算的定义是把内存中的0和1全部取反。



####    === 5. shl（&lt;&lt;）左移 ===

a &lt;&lt; b的值实际上就是**a乘以2的b次方**，因为在二进制数后添一个0就相当于该数乘以2



####    === 6. shr（&gt;&gt;）右移 ===

同理，a &gt;&gt; b的值实际上就是**a除以2的b次方并取整**

### 

### **位运算的简单应用**

![&#x6765;&#x6E90;&#xFF1A;&#x767E;&#x5EA6;&#x767E;&#x79D1;&#xFF08;&#x56FE;&#x5012;&#x662F;&#x767E;&#x5EA6;&#x767E;&#x79D1;&#x81EA;&#x5DF1;&#x6574;&#x7684;&#xFF09;](../.gitbook/assets/image%20%2827%29.png)



