final Map可以修改内容，final 常量不能修改

对比集合：

final Map map =new HashMap();

final List list =new ArrayList();



map和list 对应的是栈中存储的地址，final表示地址不能修改，但是地址对应的内存区域的值是可以修改的；



对比常量：

final String name=”Joke”;

final int age=10;



name和age对应的是栈中存储的地址，同样final表示地址不能修改，但是地址的存储跟常量的值有关，给他重新赋值会指向另外一个对象，地址就改变了