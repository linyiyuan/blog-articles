浅谈架构方式
------

```
    什么是架构，为什么要使用架构，我认为架构就相当于人的一个骨骼 机器的整体框架一样，他决定了之后的所有操作都是以什么样的方式进行展开的，就像是乐高积木一样
        例子:最简单的机器人就是由某个模块之间互相焊接组成的，将四肢焊接到躯干的电路板上 ，这样就会产生一个问题，当某一个部位发生故障后，就需要将相应的部位替换，但是由于所有连接点都是焊死的，所以在后期维护相当麻烦，落是我们初期设计就讲各个连接点设计成即插即用的接口，那么当有零件模块损坏时，只需要将损坏的零件拔下，用新的零件直接替换就好了，这样的设计无疑是更加科学合理的

    在软甲开发过程一样，架构就相当于上个例子中的不同焊接方式，不同的架构可以使我们有着不同的组织软件的方式，并不一定说哪一个最好，而是根据其使用的场景来选择最为合适的架构方式，选用合适的架构可以助于我们实现软件的合理分层，降低耦合度，便于后期的维护和拓展
```

MVC（Model View Control）
-----------------------

```
较为传统和成熟的一种架构模式，最核心就是通过control层来进行调控，
所有的调度都是由Control来进行处理的，其核心的策略如下
```

![](https://i.imgur.com/w4KWjhv.png)

可以看到control处于中间核心地位，同时三者之前都是两两有联系的control请求model层操作，model处理数据返回给view

优点：对于混乱的软件住址方式有了一个明确的组织方式，通过control来掌控全局，同时将view的展示和model的变化分离开

缺点:view 和 model之间是直接进行交互的，也就是说view和model之间是可以相互产生影响的，这样在代码中就必然会导致view和model之间的耦合性，在后期的维护也就比较困难

MVP(Model View Presenter)
-------------------------

`MVC架构模式的变种，使用presenter来代替control，而且改变了数据的流向view model之间不再进行交互而是全部通过presenter来进行`![](https://i.imgur.com/ZdPBlXi.png)

presenter同时持有view model同时view model中也有对于presenter的作用，当view中的视图改变需要更新数据时，通过presenter来通知model进行数据更新，然后反向

优点：可以使整个软件分层清晰，降低耦合度

缺点：需要加入presenter来作为桥梁协调view model 同时也会使presenter变得臃肿

mvvm（model view viewModel）
--------------------------

`MVVM其实是对MVP的一种改进，他将Presenter替换成了ViewModel，并通过双向的数据绑定来实现视图和数据的交互。也就是说只需要将数据和视图绑定一次之后，那么之后当数据发生改变时就会自动的在UI上刷新而不需要我们自己进行手动刷新。在MVVM中，他尽可能的会简化数据流的走向，使其变得更加简洁明了。`优点：可以使得数据流的走向更加清晰明了，同时也简化了开发，数据和视图只需要进行一次绑定即可 缺点：目前这种架构模式的实现方式比较不完善规范，常见的就是DataBinding框架

![](https://i.imgur.com/pbmPQLE.png)

更加详细内容请查看http://www.ruanyifeng.com/blog/2015/02/mvcmvp\_mvvm.html