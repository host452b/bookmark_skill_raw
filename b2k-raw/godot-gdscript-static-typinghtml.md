# 在GDScript中体验静态类型化编程

本文讲述的内容:

- **GDScript中如何使用类型系统**

- 静态类型化有助于避免bug

这项新特性的使用场景和使用方式，完全根据你自己的习惯和需要来决定：比如只在一些“敏感的”GDScript脚本中使用、或者全部使用、或者不用！

静态类型声明可作用于变量、常量、函数、参数及返回值类型。

备注:
```
Godot 从 3.1 版本开始支持类型化声明。

```

## 简介

使用类型化GDScript方式编写代码，Godot能检测出更多的潜在错误！在用Godot工作时，你和同事能得到更多信息，因为当你调用方法时，能看出各个参数的类型。

假设你在开发一套库存系统。 你编写了`Item`节点，然后`Inventory`节点。要将物品放到仓库，当调用你刚写的代码时，写法是要将一个`Item`传给`Inventory.add`方法。而利用类型声明，就能强化这一点：
```
    # In 'Item.gd'.
    class_name Item
    # In 'Inventory.gd'.
    class_name Inventory

    func add(reference: Item, amount: int = 1):
        var item = find_item(reference)
        if not item:
            item = _instance_item_from_db(reference)

        item.amount += amount

```

另一项显著优势是可以享受新的**警告机制**。从 Godot 3.1 版本开始，你编写代码时会被给出相关警告-引擎会识别出可能在运行时导致问题的代码位置，当然，你来决定是否进行处理。

静态类型化方式也能给到你更好的代码自动完成的选项。通过下面的代码，能看出`PlayerController`类那里，动态类型与静态类型两种方式下的自动完成选项的不同之处。

将节点存到变量中，输入“点号”字符，得不到自动完成的提示：

这种因为是动态类型的代码写法，Godot无法得知传给该函数的节点或值的类型。如果代码显式指定类型，你就会得到编辑器对该节点全部公共方法与属性的提示：

未来类型化GDScript编写方式还能让你收获到代码运行性能的提升：基于JIT方式的编译以及其它方面的编译器优化已经在规划中了。

总的来说，类型化编程能给到你更结构化的体验。它有助于预防错误、优化脚本的文档化表述(self-documenting)效果。这点在团队协作中或长期维护的项目中尤其有益：有研究表明，开发者花费的大多数时间都是用在阅读他人的代码、或是阅读他们自己过去编写的早已遗忘的脚本；而更清晰更结构化的代码，就更易于快速理解，项目进展也就更快。
## 用法

要定义变量或常量的类型，在变量名后面打上分号，跟着就声明它的类型。如`var health: int`。这样就强制让该变量的类型保持相同：
```

    var damage: float = 10.5
    const MOVE_SPEED: float = 50.0

```

如果你只打冒号但省略后面的类型声明，Godot也会尝试进行类型推导：
```

    var life_points := 4
    var damage := 10.5
    var motion := Vector2()

```

当前支持三种类型：

- [语言内置类型](https://docs.godotengine.org/en/stable/getting_started/scripting/gdscript/gdscript_basics.html#doc-gdscript-builtin-types)

- 引擎的核心类及节点(`Object`, `Node`, `Area2D`, `Camera2D`等)

- 自行编写的类

注：
```
其实你无需显式声明常量的类型，因为Godot会自动根据所赋的值进行设定。但是你还是可以通过显式声明以便清晰表述编码时的意图。

```

### 自定义变量类型

任何类包括自定义类均可作为类型进行声明。自定义类有两种写法。一种是预先加载你想使用的脚本，定义为常量，就可以作为一种类型：
```
    const Rifle = preload("res://player/weapons/Rifle.gd")
    var my_rifle: Rifle

```

另一种是在创建自定义类文件时，通过`class_name`关键字进行声明。 比如上面的例子，那个 Rifle.gd 文件里的写法像这样：
```
    extends Node2D
    class_name Rifle

```

用`class_name`的写法后，Godot就会自动注册Rifle这个全局类型，代码中随处可以使用，无需再像上面那样用常量预先加载了。
```
    var my_rifle: Rifle

```

### 变量类型转换

类型转换是静态类型语言中的一个关键概念，是指值从一种类型转换成另外一种类型。

假设游戏里有个 `Enemy（敌人）`，继承自 `Area2D`，它会与玩家发生碰撞，这时会用给一个 `KinematicBody2D` 节点附加一个 `PlayerController` 脚本的方式来实现。在 `on_body_entered` 信号中可以编写回调的代码进行检测碰撞，基于类型化的写法，要检测的物体就只是宽泛的`PhysicsBody2D`，而不是明确的`PlayerController`。

用`as`类型转换关键字来判断该`PhysicsBody2D`是否是玩家，用冒号`:`来强制变量为`PlayerController`类型。
```
    func _on_body_entered(body: PhysicsBody2D) -&gt; void:
        var player := body as PlayerController
        if not player:
            return

        player.damage()

```

在处理自定义类型的时候，如果`body`不是继承自`PlayerController`，代码中的`player`变量就会赋值为`null`，可以通过这一点来判断`body`是不是玩家。类型转换后，在编辑器中就可以得到完整的代码自动完成提示。

注：
```
若是针对内置类型进行转换，则失败时Godot会抛出错误。

```

### 安全行

安全行是 Godot 3.1 提供的一个新工具，可以告诉开发者哪些可能有语义歧义的代码行是类型安全的。类型转换就可用在确保这些安全行处。

由于代码可能存在同时出现类型化和动态化两种代码的情况，有时 Godot 就没有足够信息可以判断出某条指令在运行时是否引发错误。

这种情况在获取子节点对象时就会发生。一个计时器的例子：GDScript基于 [鸭子类型](https://stackoverflow.com/a/4205163/8125343)只关注对象行为，但是这样动态化写法，在运行时甚至无法得知传进来的对象是否具有所需调用的方法。用类型转换告诉 Godot 在获取节点对象时所预期的类型，如`($Timer as Timer)`, `($Player as KinematicBody2D)`，Godot就能凭此确定类型是否正常。

如果确定正常的话，脚本编辑器左侧会呈现绿色提示。

Unsafe line (line 7) vs Safe Lines (line 6 and 8)

注：
```
可以在编辑器设置界面关闭安全行机制或修改提示颜色。

```

### 定义函数的返回值类型 - 用 `-&gt;` 箭头写法

```
    func _process(delta: float) -&gt; void:
        pass

```

声明为`void`类型意味着该函数不返回任何结果。返回值可用的类型与变量相同：
```
    func hit(damage: float) -&gt; bool:
        health_points -= damage
        return health_points &lt;= 0

```

当然，也就可以使用自定义节点作为返回值类型：
```
    # Inventory.gd

    # Adds an item to the inventory and returns it.
    func add(reference: Item, amount: int) -&gt; Item:
        var item: Item = find_item(reference)
        if not item:
            item = ItemDatabase.get_instance(reference)

        item.amount += amount
        return item

```

## 静态还是动态？每次统一用一种

静态类型化GDScript可以与动态类型GDScript在同一个项目中共存。但是建议在整个团队及相应项目代码中任选一种统一的风格，这样相同的标准便于团队成员间协作，阅读和理解他人代码时也会更快速。

静态类型化的写法多多一点代码，但是如上所述能因此受益。这里给出两种空骨架代码。

动态类型写法：
```
    extends Node

    func _ready():
        pass

    func _process(delta):
        pass

```

静态类型写法：
```
    extends Node

    func _ready() -&gt; void:
        pass

    func _process(delta: float) -&gt; void:
        pass

```

可以看到，针对引擎的这些虚拟方法，也可以使用类型声明。同样，节点的信号回调函数，跟所有方法一样，也能使用类型声明。比如一个`body_entered`信号的动态类型写法：
```

    func _on_Area2D_body_entered(body):
        pass

```

对应的类型提示写法：
```
    func _on_area_entered(area: CollisionObject2D) -&gt; void:
        pass

```

另外，像下面的例子，可以将参数`bullet`原本约定的`CollisionObject2D`类型任意替换成你自定义的类型，引擎会自动进行类型转换：
```
    func _on_area_entered(bullet: Bullet) -&gt; void:
        if not bullet:
            return

        take_damage(bullet.damage)

```

代码这里的意图是`bullet`参数要要更精确的指定为项目中创建的`Bullet`类型。到时如果这个参数传了其它类型的节点如`Area2D`，或者非继承自`Bullet`的节点，`bullet`参数会被赋值为`null`。
## 警告机制

请参看单独的[警告机制](https://docs.godotengine.org/en/stable/getting_started/scripting/gdscript/warning_system.html)章节。
## 无法声明类型的场景

列出无法使用类型提示的几种场景，下面所有例子都会引发错误。
### 1、枚举不能用作类型。

```
    enum MoveDirection {UP, DOWN, LEFT, RIGHT}
    var current_direction: MoveDirection

```

### 2、数组内的单个成员无法指定类型。

```
    var enemies: Array = [$Goblin: Enemy, $Zombie: Enemy]

```

### 3、`for`循环中不能强制指定类型，因为通过`for`关键字循环展开的每个元素已经变为不同的类型。因此，不能写成下面这样：

```
    var names = ["John", "Marta", "Samantha", "Jimmy"]
    for name: String in names:
        pass

```

### 4、两个脚本间不能形成循环依赖。

```
    # Player.gd

    extends Area2D
    class_name Player

    var rifle: Rifle

```

```
    # Rifle.gd

    extends Area2D
    class_name Rifle

    var player: Player

```

## 小结

类型化的GDScript是一种强大的工具。Godot 从 3.1 版本开始支持这种特性，能帮助开发者编写更结构化的代码，避免一些常见错误，并且能创建出更具伸缩性的系统。基于编译器的优化能力，静态类型特性将来还能带来更好的性能。