# JavaBasic
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
### 6.2 成员函数和成员变量
>在类的内部调用成员函数和成员变量是时，不需要this.var或this.func，在类的外部则需要vm.var或vm.func. 成员变量的生存期是对象的生存期，作用域是类内部的成员函数。
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

public class Display {
	
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
	
	public static void main(String[] args) {
		Display d = new Display(24);
		for (int i=0; i<1000 ; i++) {
			d.increase();
			System.out.println(d.getValue());
		}
	}

}
