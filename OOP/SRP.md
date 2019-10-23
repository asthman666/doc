# Single responsibility principle

1.  each software module should have one and only one reason to change

    一个改变的原因是怎么定义的？

    一些人想要弄明白修复bug是不是一个改变的原因。另外一些人想弄明白重构是不是改变的原因。这个问题可以由"reason to change"和"responsibility"之间的耦合来回答。

    当然，代码的职责并不是修复bug和重构。那么代码的指责是什么呢？进一步说，**谁必须为代码的设计做出相应？**

    想象一个简单的商业结构。一个CEO在最顶端，CFO，COO和CTO需要想CEO汇报。CFO负责财务，COO负责运营，CTO负责技术。

    加入我们又一个类：

        public class Employee {
            public Money calculatePay();
            public void save();
            public String reportHours();
        }

    * calculatePay实现了一个employee应该发多少工资
    * save把employee的数据存储到数据库中
    * reportHours返回一个字符串，这个字符串会添加到报告中，审计员会检查这个字符串，确保员工的工作时长

    现在，如果员工的工资发错了，CFO会有责任；如果审计报告有问题，COO会有责任；如果数据不能存储到数据库，CTO会有责任

    因此，calculatePay这个算法改动的原因将会来自于CFO的组织，reportHours改动的原因来自COO的组织，save改动的原因来自CTO的组织

    这就是Single responsibility principle的症结所在，原则是关于人的。

    当你写一个软件模块，你想要确认当一个改变被请求，这个改变仅仅源于一个人，或者一组紧密耦合的人，代表一个狭义的商业功能。
    
    为什么呢？因为你不想当CTO请求改变时，COO被影响。

    想象一下，如果你的车窗坏了，你去修理厂修理。第二天，修理厂打电话给你说车修好了，当你拿到你的车，发现车窗修好了，但是车不能启动了。

2. Gather together the things that change for the same reasons. Separate those things that change for different reasons.

如果你思考上面这句话，你将会认识到，这仅仅是另外一种定义聚合和耦合的方法。对于有相同原因的修改请求，增加聚合；对于有不同原因修改请求，减少耦合。