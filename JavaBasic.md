# Java基础
## 1 基础
### 1.1 输入输出
    System.out.println("Hello World!");
    Scanner in = new Scanner(System.in);
    System.out.println("echo: " + in.nextLine());
### 1.2 变量常量
    int prince = 0;
    double amount;
    price = in.nextInt()

    final int amount = 100;
### 1.3 类型转换
    (int)(12.5*13.7)
## 2 流程控制
### 2.1 if语句
    if (condition) {
        ...
    }
### 2.2 switch-case语句
>case可以是整数，也可以是String

		switch (x) {
		case 1:
			System.out.println("1");
		case 2:
			System.out.println("2");
			break;
		case 3:
			System.out.println("3");
		default:
			System.out.println("4");
			break;
		}
### 2.3 while循环 和 do-while循环
    while (condition) {
        
    }

    do {

    }while (condition)
### 2.4 for循环
    for (int i=0; i<100; i++) {

    }
## 3 数组

>数据类型相同，一旦创建不能变大小，定义的时候可以用变量表示大小。

    int x = 10;
    int[] numbers = new int[x];
## 4 字符串
### 4.1 字符
    char c = 'x'
### 4.2 包裹类型
>int的包裹类型是Ingeter，它首先可以代替int来定义变量。它还可以表示整数的最大最小值

    Integer.MAX_VALUE
    Character.isDigit('1')
### 4.3 字符串
>字符串不可变，方法可能有结果，但不会有副作用。

    String s1 = new String("a string");
    String s2 = "This is s2";
    System.out.println(s1+s2);

    s1 == s2;           // 比较是不是同一个字符串
    s1.equals(s2);      // 比较内容是不是相同

    s1.compareTo(s2);   // 1大 -1小 0一样
    s1.length();        // 长度
    s1.charAt(2);       // 下标
    s1.indexOf('a', loc+1);     // -1表示没找到
## 5 函数
	public static void sum(int a, int b) {
		System.out.println(a+b);
	}

	public static void main(String[] args) {
		sum(1,5);
	}

**注意:**
- Java全部都是值传递，这样，基本数据类型肯定不能改变，但是对于对象这种引用变量而言，拷贝的对象变量依然指向该对象，所以可以对对象进行操作。
## 6 类和对象
### 6.1 定义类
    package vendingMachine;

    public class VendingMachine {
        int price = 80;
        int balance;
        int total;
        
        void showPrompt() {
            System.out.println("Welcome!");
        }
        
        void insertMoney(int amount) {
            balance = balance + amount;
        }
        
        void showBalance() {
            System.out.println(balance);
        }
        
        void getFood() {
            if (balance >= price) {
                System.out.println("Here you are!");
                balance -= price;
                total += price;
            }
        }
        
        public static void main(String[] args) {
            VendingMachine vm = new VendingMachine();
            vm.showPrompt();
            vm.showBalance();
            vm.insertMoney(100);
            vm.getFood();
            vm.showBalance();
        }

    }
**注意：**
- 不要编写返回值是引用可变对象的访问器方法（所谓访问器方法就比如getDate()），例如返回了Date对象并赋值给了d，现在d和this.date指向同一个对象，d调用setTime()方法将改变this.date，可以改为return date.clone()
- 上面的vm并不是一个对象，而是对一个对象的引用（可以叫做对象变量），真正的对象是new VendingMachine()语句new出来的对象，这类似于C++的对象指针。
### 6.2 成员函数和成员变量
>在类的内部调用成员函数和成员变量时，不需要this.var或this.func，在类的外部则需要vm.var或vm.func. 成员变量的生存期是对象的生存期，作用域是类内部的成员函数。
### 6.3 对象初始化
>如果有一个成员函数的名字和类的名字完全相同，则在创建这个类的每一个对象的时候会自动调用这个函数，这个函数就叫构造函数。

    package vendingMachine;

    public class VendingMachine {
        int price = 80;
        int balance;
        int total;
        
        VendingMachine() {
            balance = 80;
        }
        VendingMachine(int price) {
            this.balance = price;
        }

        void showBalance() {
            System.out.println(balance);
        }
        
        public static void main(String[] args) {
            VendingMachine vm1 = new VendingMachine();
            VendingMachine vm2 = new VendingMachine(70);
            vm1.showBalance();
            vm2.showBalance();
        }

    }

- 构造函数不能有返回类型
- 构造函数可以不止一个，参数个数可以不同即可（重载）
### 6.4 对象的交互
    package clock;

    class Display {
        
        private int value = 0;
        private int limit = 0;
        
        public Display(int limit) {
            this.limit = limit;
        }
        
        public void increase() {
            value++;
            if (value == limit) {
                value = 0;
            }
        }
        
        public int getValue() {
            return value;
        }
    }

    public class Clock {
        
        private Display hour = new Display(24);
        private Display minute = new Display(60);
        
        public void start() {
            int x = 0;
            while (x++ < 1000) {
                minute.increase();
                if (minute.getValue() == 0) {
                    hour.increase();
                }
                System.out.printf("%02d:%02d\n", hour.getValue(), minute.getValue());
            }
            
        }
        
        public static void main(String[] args) {
            // TODO Auto-generated method stub
            Clock clock = new Clock();
            clock.start();
        }

    }
### 6.5 private
>只有这个类内部可以访问，即成员函数中可以访问，这个限制是对类的而非对对象的，因为成员函数中可以包涵对同类的其他对象的操作。

### 6.6 public
>一个编译单元(.java文件)只能有一个public类，且类名与文件名相同。还有一种情况，既没有private也没有public关键字，那么它是friendly的，可以被同一个包中的其他类访问。

### 6.7 类变量（静态变量）
>当成员变量之前有static关键字的时候，该成员变量成为类变量，不再为某一对象独自拥有，而是被该类全体所有，某一对象的类变量改变，其余对象的该类变量随之改变。可以用Class.var访问，也可以用c.var访问。但其实静态常量更常用。

### 6.8 类函数（静态方法）
>当函数之前带有static时，成员函数变为类函数，它只能对类变量进行操作，同样地，它能被类访问，也能被对象访问。但是建议使用类来访问，如Math.pow(x,a)，因为静态方法只能对类变量进行操作，所以用对象访问静态方法时，实际上与该对象完全无关，这看起来很奇怪。

### 6.9 toString函数
>当类中有public String toString() 函数时，在打印该类的某一个对象时，可以成功显示有意义的字符串

    package notebook;

    public class NoteBook {
        private int x = 10;
        
        public String toString() {
            return "" + x;
        }
        
        public static void main(String[] args) {
            // TODO Auto-generated method stub
            NoteBook nb = new NoteBook();
            System.out.println(nb);
        }
    }


## 7 容器
### 7.1 容器类
    private ArrayList<String> notes = new ArrayList<String>();

- ArrayList是容器的类型
- String是元素的类型

### 7.2 ArrayList
    package notebook;

    import java.util.ArrayList;

    public class NoteBook {
        private ArrayList<String> notes = new ArrayList<String>();
        public void add(String s) {
            notes.add(s);
        }

        public void add(String s, int location) {
            notes.add(location, s);
        }

        public int getSize() {
            return notes.size();
        }

        public String getNote(int index) {
            return notes.get(index);
        }

        public boolean removeNote(int index) {
            return true;
        }

        public String[] list() {
            String[] a = new String[notes.size()];
            notes.toArray(a);
            return a;
        }
            
        public static void main(String[] args) {
            // TODO Auto-generated method stub
            NoteBook nb = new NoteBook();
            nb.add("first");
            nb.add("second");
            nb.add("third",1);
            String[] a = nb.list();
            for (String s : a) {
                System.out.println(s);
            }
        }
    }

- .add()
- .get()
- .toArray()

### 7.3 HashSet
    HashSet<String> s = new HashSet<String>()
- .add()

### 7.4 HashMap
    HashMap<Integer, String> hm = new HashMap<Integer, String>();
    hm.put(key, value);
    hm.get(key);
    hm.containsKey();
    hm.KeySet().size();
    for (Integer k : hm.KeySet()) {
        String s = hm.get(k);
        System.out.println(s);
    }

- <>里面不能填int，必须是Integer，因为要填入对象，而非基本数据类型。

## 8 继承
### 8.1 概念
item.java:

    package database;

    public class Item {
        private String title;
        private int playingTime;
        private boolean gotIt = false;
        private String comment;
        
        public Item() {
            
        }
        
        
        
        public Item(String title, int playingTime, boolean gotIt, String comment) {
            super();
            this.title = title;
            this.playingTime = playingTime;
            this.gotIt = gotIt;
            this.comment = comment;
        }



        public static void main(String[] args) {
            // TODO Auto-generated method stub

        }



        public void print() {
            // TODO Auto-generated method stub
            System.out.println(title);
        }
    }
CD.java:

    package database;

    public class CD extends Item {
        private String artist;
        private int numofTracks;

        public CD(String title, int playingTime, String comment, String artist, int numofTracks) {
            super(title, playingTime, false, comment);
            this.numofTracks = numofTracks;
            this.artist = artist;
        }
        
        public void print() {
            System.out.println(artist);
            super.print();
        }

        public static void main(String[] args) {
            // TODO Auto-generated method stub
            CD cd = new CD("CD1",2,"...","CDA1",2);
            cd.print();
        }
    }

- 子类的super会调用父类的构造函数，父类函数可能存在重构，子类的super会根据参数表选择父类匹配的构造函数，如果没有super，则调用父类没有参数的那个构造函数。
- 子类调用父类的函数，需加super，如super.print()
- 子类不能直接访问父类的private域

### 8.2 多态变量
- 子类的对象可以当做父类的对象来使用
- 可以赋值给父类的变量
- 可以传递给需要父类对象的函数
- 可以放进存放父类对象的容器里

**当把子类的对象赋值给父类的变量的时候，就发生了向上造型。** 
**父类对象赋值给子类变量会报错，除非造型，CD cd = (CD)item;**

### 8.3 代码优化
>封装可以减少类之间的耦合，容器的使用可以提升代码的可扩展性（不要硬编码）。

### 8.4 其他
>final类是不可派生子类的类，方法之前也可以加final，这样它就不能被子类覆写，final类中的方法自动成为final方法。
## 9 抽象
### 9.1 例子
    package shape;

    import java.awt.Graphics;

    public abstract class Shape {

        public abstract void draw(Graphics g);

    }

- 只要有一个抽象的成员函数，该类就是抽象的。
- 抽象类不能创建对象。
- 抽象类可以定义变量，任何继承了这个抽象类的非抽象类的对象都可以赋值给这个变量。
- 继承自抽象类的子类必须覆盖父类中的抽象函数，否则自己就成了抽象类。

### 9.2 接口interface
- 接口是一个纯抽象类，所有的成员函数都是抽象函数，所有成员变量都是public static final
- 其他类可以实现很多接口。implements cell

## 10 异常
### 10.1 try
    package exception;

    import java.util.Scanner;

    public class ArrayIndex {

        public static void main(String[] args) {
            // TODO Auto-generated method stub
            int[] a = new int[10];
            int idx;
            Scanner in = new Scanner(System.in);
            idx = in.nextInt();
            try {
                a[idx] = 10;
                System.out.println("hello");
            } catch (ArrayIndexOutOfBoundsException e) {
                System.out.println("Caught");
            } catch (){
                ...;
            } catch (){
                ...;
            }
        }

    }
### 10.2 e的方法
System.out.println(e.getMessage());
System.out.println(e);
e.printStackTrace();
throw e;异常再次抛出
### 10.3 异常的规范写法
>不要一堆的if- else，异常机制的最大好处是清晰地分开了正常的业务逻辑代码和遇到情况时的处理代码。

    try {
        open the file;
        determine its size;
        allocate that much memory;
        read the file into memory;
        close the file;
    } catch (fileOpenFailed) {
        doSomething;
    } catch (sizeDeterminationFailed) {
        doSomething;
    } catch (memoryAllocationFailed) {
        doSomething;
    } catch (readFailed) {
        doSomething;
    } catch (fileCloseFailed) {
        doSomething;
    }
### 10.4 throw
    package exception;

    import java.util.Scanner;

    class OpenException extends Throwable{
        
    }

    public class ArrayIndex {
        public static int open() {
            return -1;
        }

        public static void readFile() throws OpenException {
            if (open() == -1) {
                throw new OpenException();
            }
        }
        
        public static void main(String[] args) {
            // TODO Auto-generated method stub
            try {
                readFile();
            } catch (OpenException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
        }

    }
### 10.5 异常的继承
>异常exception继承自throwable，其他异常也可以有继承关系，同样地，子异常也可以被父异常的catch捕捉到，catch一旦捕捉，不会再执行下面的catch，因此，如果上面的catch里是父异常，写在下面catch的子异常是不可能起作用的，这就是它会报错的原因。

    catch (Exception e){
        // 可以捕捉任何异常
    }
### 10.6 异常与父子类
>父类有一个声明抛出A异常的成员函数，子类覆盖该函数时，该函数只能不抛异常或者也抛A异常，不能增加B,C异常。

>相反，子类的构造函数必须声明父类可能抛的全部异常。（总结：被调用者不能比调用者更多）