# 注解
## 1 注解定义
>注解不是程序本身，它可以对程序作出解释。它可以被其他程序（比如编译器）读取。
- 注解以@注释名在代码中存在，还可以添加参数值，如：

        @SuppressWarnings(value="unchecked")
- 注解在package, class, method, field上面使用，相当于给它们添加了额外的辅助信息，我们可以通过反射机制编程实现对这些元数据的访问。
## 2 举例
- @Override: 重写
- @Deprecated: 不推荐使用的，废弃的方法
- @SuppressWarnings("all"): 镇压警告，原警告不报