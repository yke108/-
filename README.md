工厂方法模式
===============

### 简介
工厂方法模式是一种常用的类创建型设计模式,此模式的核心精神是封装类中变化的部分，提取其中个性化善变的部分为独立类，通过依赖注入以达到解耦、复用和方便后期维护拓展的目的。它的核心结构有四个角色，分别是抽象工厂、具体工厂、抽象产品、具体产品。

### 角色结构

抽象工厂：
> 是工厂方法模式的核心，与应用程序无关。任何在模式中创建的对象的工厂类必须实现这个接口。

具体工厂：
> 这是实现抽象工厂接口的具体工厂类，包含与应用程序密切相关的逻辑，并且受到应用程序调用以创建产品对象。

抽象产品：
> 工厂方法模式所创建的对象的超类型，也就是产品对象的共同父类或共同拥有的接口。

具体产品：
> 这个角色实现了抽象产品角色所定义的接口。某具体产品有专门的具体工厂创建，它们之间往往一一对应。

### 代码实例

```php
/**
 * 抽象工厂类接口
 */
interface FactoryInterface
{
    public function productMethod();
}

/**
 * 具体的工厂A类，继承抽象工厂
 */
class FactoryA implements FactoryInterface
{
    public function productMethod()
    {
        return new ProductA();
    }
}

/**
 * 具体的工厂B类，继承抽象工厂
 */
class FactoryB implements FactoryInterface
{
    public function productMethod()
    {
        return new ProductB();
    }
}

/**
 * 抽象产品类接口
 */
interface ProductInterface
{
    public function doAction();
}

/**
 * 具体的产品A类，继承抽象产品
 */
class ProductA implements ProductInterface
{
    public function doAction()
    {
        echo "生产产品A";
    }
}

/**
 * 具体的产品B类，继承抽象产品
 */
class ProductB implements ProductInterface
{
    public function doAction()
    {
        echo "生产产品B";
    }
}

//使用工厂子类获取产品类
$factory = new FactoryA();
$mode = $factory->productMethod();

//执行产品类方法
$mode->doAction();
```

### 总结

*   优点：添加新的产品对象时，仅仅需要添加一个具体对象以及一个具体工厂对象，扩展性很好，不需要修改原有代码，很好的符合了”开放－封闭”原则
*   缺点：引进一个新的产品类，就不得不创建一个工厂子类