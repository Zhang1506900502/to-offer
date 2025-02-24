### 替换空格

> 题目:请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

示例 1：

```js
//输入：s = "We are happy."
//输出："We%20are%20happy."
```

> 限制：0 <= s 的长度 <= 10000

### 思路分析

- 方法一：正则表达式解法

这也是最简单的办法，利用正则结合字符串的replace方法即可。代码如下:

```js
var replaceSpace = function (s) {
    return s.replace(/\s/g,"%20");
};
```

由于程序只执行一次，所以这个算法的时间复杂度为 O(1),每次都会访问1次字符串，所以空间复杂度为 O(1)。

- 方法二:字符数组

由于字符串是从1个字符替换到3个字符，因此可以创建一个长度为该字符串3倍的字符数组。然后创建一个索引如index为0，index表示遍历完成后的替换字符串的长度，遍历字符串，然后获取字符串的当前字符，判断如果当前字符是空格，则数组的第index为"%",第index + 1为"2",第index + 2为"0",并且将index加3，否则数组的第index项为该字符，并且将index加1，遍历结束后，最后得到的index则为新字符串的长度，从数组的前index个字符中创建新字符串即可。代码如下:

```js
var replaceSpace = function (s) {
    let len = s.length,index = 0,array = new Array(len * 3);
    for(let i = 0;i < len;i++){
        if(s[i] === " "){
            array[index] = "%";
            array[index + 1] = "2";
            array[index + 2] = "0";
            index += 3;
        }else{
            array[index] = s[i];
            index += 1;
        }
    }
    // 从0开始截取到index索引的字符数组即为替换后的字符串，然后调用join方法转成字符串，注意这里的参数必须是空字符串。
    return array.slice(0,index).join("");
};
```

由于用到了一个循环，所以时间复杂度为O(n),而且用了一个数组来存储，所以空间复杂度也为O(n)。

