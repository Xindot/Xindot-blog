---
layout: post
title: 比较几种js数组求和的方法
tags: [js]
categories: [it]

---

### 1 执行代码
```
function sumRun(length) {
  // 创建数组
  var array = new Array();
  for (var i = 0; i < length; i++) {
    array.push(i * 2);
  }

  // 1 for循环 
  console.time('for');
  var sum1 = 0;
  for (var i = 0; i < array.length; i++) {
    sum1 += array[i];
  }
  console.timeEnd('for')

  // 2 forEach 
  console.time('forEach');
  var sum2 = 0;
  array.forEach(el => {
    sum2 += el;
  })
  console.timeEnd('forEach')

  // 3 归并方法reduce()和 reduceRight()
  console.time('reduce');
  var sum31 = array.reduce(function (prev, next, index, array) {
    return prev + next;
  })
  console.timeEnd('reduce')

  console.time('reduceRight');
  var sum32 = array.reduceRight(function (last, before, index, array) {
    return last + before;
  })
  console.timeEnd('reduceRight')

  // 4 eval()
  console.time('eval');
  var sum4 = eval(array.join("+"))
  console.timeEnd('eval');

  // 5 map
  console.time('map');
  var sum5 = 0;
  array.map(item => sum5 += item)
  console.timeEnd('map');

  // sum
  var sumArr = [sum1, sum2, [sum31, sum32], sum4, sum5]
  console.log(' ↓ sum1,sum2,[sum31,sum32],sum4,sum5 ↓ ')
  console.log(JSON.stringify(sumArr))
}
sumRun(10000)
```

### 2 执行结果

##### 十位
![10](http://img.6h5.cn/xindot-blog/paste/20191225172545.png)
> map < for < reduceRight < reduce < forEach < eval 

##### 百位
![100](http://img.6h5.cn/xindot-blog/paste/20191225172700.png)
> reduce < reduceRight < for < map < forEach < eval

##### 千位
![1000](http://img.6h5.cn/xindot-blog/paste/20191225172741.png)
> reduceRight < reduce < map < for < forEach < eval

##### 万位
![10000](http://img.6h5.cn/xindot-blog/paste/20191225172830.png)
> forEach < reduceRight < reduce < for < map < eval

##### 十万级
![100000](http://img.6h5.cn/xindot-blog/paste/20191225172920.png)
> reduceRight < reduce < forEach < for < map < eval

##### 百万级
![1000000](http://img.6h5.cn/xindot-blog/paste/20191225172941.png)
> reduceRight < reduce < map < forEach < for < eval

##### 千万级
![10000000](http://img.6h5.cn/xindot-blog/paste/20191225173032.png)
> reduce < reduceRight < forEach < for < map < eval

##### 亿级
![100000000](http://img.6h5.cn/xindot-blog/paste/20191225173333.png)
> reduceRight < reduce < for < forEach … 浏览器崩溃

#### 2.1 将函数中 eval 和 map 顺序调整一下重试
##### 亿级
![100000000](http://img.6h5.cn/xindot-blog/paste/20191225175431.png)
> reduceRight < reduce < for < forEach < map … 浏览器崩溃

### 3 小结
> 1 ```reduce```表现一直优秀、```eval```综合表现较差<br/>
2 在千万级时: ```map```表现不佳<br/>
3 在百万级时: <br/>
- ```map```约是```for```的6~7倍; <br/>
- ```forEach```约是```for```的4倍; <br/>
- ```reduce```约是```for```的1/10; <br/>
- ```eval```约是```map```的4倍<br/>

### 4 测试心得
> 对于js数组求和，我觉得有人对```for循环```有所偏解，经过我一下午的测试，```for循环```性能并不比其它的要差；在百万数量级以内```for```和```map```差别不大；反而是千万级时```map```显得有点弱鸡；网上说```eval```快根本不可信；反复测试发现```reduce```才是最快的。

### 5 接下来
得空搞个```曲线图表 📈 ```来对比显示各自的性能。