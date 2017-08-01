# 简单工厂模式

#### 

#### 简介

简单工厂模式属于创新型模式，又称静态工厂方法模式。

简单工厂模式中包含的角色及其相应的职责如下：

* 工厂角色：它是简单工厂模式的核心，由它负责创建所有类的内部逻辑。同时，工厂类必须能被外界调用，创建所需要的产品对象。
* 抽象产品角色：简单工厂模式所创建的所有对象的父类，这里的父类可以是接口或者抽象对象类，它负责描述所有实例所共有的公共接口
* 具体产品角色：简单工厂所创建的具体实例对象。这些产品具有共同的父类。

通过简单工厂模式，咱们做一个运算器。

首先画出运算器的UML图：

![](/assets/未命名文件.png)

Android运算器代码：

工厂类:

```java
/**
 * Created by huangdaju on 17/8/1.
 */

public class OperationFactory {

    public static Operation createOperation(String operate) {
        Operation op = null;
        if ("+".equals(operate)) {
            op = new OperationAdd();
        } else if ("-".equals(operate)) {
            op = new OperationSub();
        } else if ("*".equals(operate)) {
            op = new OperationMul();
        } else if ("/".equals(operate)) {
            op = new OperationDiv();
        }
        return op;
    }
}
```

运算类：

```java
/**
 * Created by huangdaju on 17/8/1.
 */

public abstract class Operation {

    private double numberA;
    private double numberB;

    public double getNumberA() {
        return numberA;
    }

    public void setNumberA(double numberA) {
        this.numberA = numberA;
    }

    public double getNumberB() {
        return numberB;
    }

    public void setNumberB(double numberB) {
        this.numberB = numberB;
    }

    public abstract double getResult();
}
```

运算加类:

```java
/**
 * Created by huangdaju on 17/8/1.
 */

public class OperationAdd extends Operation {
    @Override
    public double getResult() {
        return getNumberA() + getNumberB();
    }
}

```

运算减类:

```java
/**
 * Created by huangdaju on 17/8/1.
 */

public class OperationSub extends Operation {
    @Override
    public double getResult() {
        double result = 0;
        result = getNumberA() - getNumberB();
        return result;
    }
}

```

运算乘类：

```java
/**
 * Created by huangdaju on 17/8/1.
 */

public class OperationMul extends Operation {

    @Override
    public double getResult() {
        double result = 0;
        result = getNumberA() * getNumberB();
        return result;
    }
}

```

运算除类：

```java
/**
 * Created by huangdaju on 17/8/1.
 */

public class OperationDiv extends Operation {

    @Override
    public double getResult() {
        double result = 0;
        try {
            result = getNumberA() / getNumberB();
        } catch (Exception e) {
            e.printStackTrace();
        }

        return result;
    }
}

```





简单工厂模式的优缺点：

优点：工厂类是整个工厂模式的核心。它包含必要的判断逻辑，能够根据外界给定的信息，决定该创建哪个具体的类的对象。用户在使用时直接根据工厂类创建的实例c操作，而无需了解这些对象是怎么创建的，以及如何组织。有利于程序整体的优化。

缺点：

