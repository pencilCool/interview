# interview


## oc 中 weak 是怎么实现的

- 带有 __weak 的对象所引用的对象被废弃的时候，变量赋值nil
- __weak ，自动将对象添加到了 autoreleasepool里面

```
{
  id __weak obj1 = obj;
}

```
```
 id obj1;
 objc_initWeak(&obj1,obj);// 初始化  ===> obj1 = 0; objc_storeWeak(&obj1,obj);
 objc_destroyMemory(&obj1); // 变量作用域结束 ===> objc_storeWeak(&obj1,0);

```
objc_storeWeak 的作用：将第一个参数的地址 （&obj1） 注册到weak 表里面。
第二个对象的地址作为键值，第二个参数为0 ，把变量从weak 表中删除。
weak表和引用计数表一样，作为散列表被实现。



