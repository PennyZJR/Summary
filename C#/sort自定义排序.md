# sort自定义排序

sort默认是升序排序，如果想要自定义排序，需记住

```c#
return -1//当前对象放在传入对象前面
return 0 //位置不变
return 1 //放在传入对象后面
```

如果想要自定义排序，实现方式有以下几种(均以**升序**为例)：

1. 自定义类实现`ICompareable<>`接口,并实现`CompareTo`方法
   ```c#
   public class People:ICompareable<People>
   {
       public string name;
       public int age;
       public People(string name,int age)
       {
           this.name=name;
           this.age=age;
       }
       public int CompareTo(People other)
       {
           if(age>other.age)
               return 1;
           else if(age==other.age)
               return 0;
           else
               return -1;
       }
   }
   ```

2. 自定义类实现`IComparer`接口，并实现`Compare`方法
   ```c#
   public class People:IComparer<People>
   {
       public string name;
       public int age;
       public People(string name,int age)
       {
           this.name=name;
           this.age=age;
       }
       public int Compare(People x,People y)
       {
           //y看做传入对象
           if(x.age>y.age)
               return 1;
           else if(x.age==y.age)
               return 0;
           else
               return -1;
       }
   }
   ```

3. 自定义类使用匿名函数或者委托排序：
   ```c#
   List<Person>list;
   list.Add(new Person("001","zhang"));
   list.Add(new Person("002","by1"));
   //使用委托
   list.Sort(delegate(Person x,Person y)
             {
                 //y看做传入对象
                 if(x.id>y.id)
                     return 1;
                 else if(x.id==y.id)
                     return 0;
                 else
                     return -1;
             });
   //使用匿名函数
   list.Sort((x,y)=>
             {
                 if(x.id>y.id)
                     return 1;
                 else if(x.id==y.id)
                     return 0;
                 else return -1;
             });
   ```

   