## 宇信科技开发规范
### 一、 前言
#### 1.1 编写目的
为提供产品质量，降低因开发风格差异导致的各种问题，编写改规范，力求通过该规范， 约束开发人员的代码编写、模块开发，提高代码可读性和可交付性、降低代码维护成本。
#### 1.2 适用人群
产品开发人员
代码复查人员
项目实施人员
技术支持人员
#### 1.3 适用范围
基础平台研发
产品功能模块研发
项目实施功能开发
代码修订
版本升级 patch
整体性框架调整
项目支持
POC DEMO 制作
#### 1.4 约束范围
Java 文件的命名、编写；  
配置文件（properties、xml、yml）文件命名、编写；
宇信科技-统一服务平台-开发规范
### 二、模块管理
#### 2.1 目录结构
```sh
xy-web
  ├── .setting                      # 工具配置 老版本配置已废弃
  │     └── .remarks.json           # 目录备注
  ├── build 
  │     └── index.js                # 打包编译配置
  ├── mocks
  │     ├── api                     # 公共常量类
  │     │     ├── common        
  │     │     │     ├── data      
  │     │     │     ├── oauth.js    #通用认证权限MOCk模拟     
  │     │     │     └── crud.js     #通用增、删、改服务
  │     │     └── example           #页面模拟数据
  │     │           └── ...    
  │     ├── index.js                # Mock数据模拟入口
  │     ├── mocks-server.js         # Mock热更新配置
  │     └── register.js             # Mock业务模块等级注册表
  ├── src                         
  │     ├── api                     # 公共常量类
  │     │     ├── common
  │     │     │     ├── crud.js     # 字典请求API 保存和删除数据
  │     │     │     ├── lookup.js   # 字典请求API 后端请求    
  │     │     │     └── oauth.js    # 认证相关API模块
  │     │     ├── example           # 请求示例
  │     │     │     └── ...
  │     │     └── protal            # 映射后台API服务请求示例 
  │     │           └── ...     
  │     ├── assets                  # 静态资源 （样式、图片、字体图标）
  │     │    ├── common             # 字体图标，通用样式
  │     │    ├── default            # 默认主题
  │     │    ├── styles             # 样式变量 
  │     │    └── ...        
  │     ├── components              # 组件
  │     │    ├── base               # 通用组件
  │     │    │     └── ...                  
  │     │    ├── features           # 扩展组件
  │     │    │     └── ...                
  │     │    ├── layout             # 框架
  │     │    │     └── ...                
  │     │    └──  website           # 网站  
  │     │          └── ...     
  │     ├── config                  # 配置文件
  │     │    ├── constant           # 接口请求相关配置
  │     │    │     ├── app.data.common.js     # 全局公共全局变量
  │     │    │     ├── app.data.service.js     # 全局后台API服务映射
  │     │    │     ├── app.data.icons.js        # 图标
  │     │    │     └── app.datalookup.js        # 静态字典
  │     │    ├── interceptors       # 拦截器
  │     │    │     └── axios.js     # axios拦截器配置  
  │     │    ├── other              # 其他配置
  │     │    │     ├── components.js     # 自定义组件全局导入
  │     │    │     ├── css.js       # 导入CSS
  │     │    │     └── other.js     # 其他辅助
  │     │    ├── index.js           # 配置入口
  │     │    └── ...                      
  │     ├── locale                  # 多语言配置
  │     ├── router                  # 产品/项目静态路由配置
  │     ├── store                   # 存储器配置
  │     ├── utils                   # 系统全局方法设定配置
  │     ├── views                   # 页面内容
  │     ├── app.vue                 # 入口页面
  │     └── main.js                 # 入口文件
  ├── tests                         # 单元测试模块
  ├── .env.development              # 开发环境配置文件
  ├── .env.production               # 生产环境配置文件
  ├── .env.staging                  # 环境标识：自定义配置文件
  ├── jest.config.js                # 业务功能
  ├── vue.config.js                 # vue-cli配置文件
  ├── gulpfile.js                   # 皮肤压缩配置
  ├── package.json           
  ... 
```
### 三、开发规范
#### 3.1命名风格
1.【强制】代码中的命名均不能以下划线或美元符号开始,也不能以下划线或美元符号结束。

    反例:_name/__name/$Object/name_/name$/Object$

2.【强制】代码中的命名严禁使用拼音与英文混合的方式，更不允许直接使用中文的方式。

    说明：正确的英文拼写和语法可以让阅读者易于理解，避免歧义。注意，即使纯拼音命名方式也要避免采用。

    正例：alibaba/taobao/youku/hangzhou 等国际通用的名称，可视同英文。

    反例：DaZhePromotion [打折]/getPingfenByName() [评分]/int某变量 = 3

3.【强制】类名使用 UpperCamelCase 风格，必须遵从驼峰形式，但以下情形例外：DO/BO/DTO/VO/AO

    正例：MarcoPolo/UserDO/XmlService/TcpUdpDeal/TaPromotion

    反例：macroPolo/UserDo/XMLService/TCPUDPDeal/TAPromotion

4.【强制】方法名、参数名、成员变量、局部变量都统一使用lowerCamelCase 风格，必须遵从驼峰形式。

    正例：localValue/getHttpMessage()/inputUserId

5.【强制】常量命名全部大写，单词间用下划线隔开，力求语义表达完整清楚，不要嫌名字长。

    正例： MAX_STOCK_COUNT

    反例： MAX_COUNT

6.【强制】抽象类命名使用 Abstract 或 Base 开头；异常类命名使用 Exception 结尾；测试类命名以它要测试的类的名称开始，以 Test 结尾。

7.【强制】中括号是数组类型的一部分，数组定义如下：String[] args;

    反例：使用 String args[]的方式来定义。

8.【强制】POJO 类中布尔类型的变量，都不要加 is，否则部分框架解析会引起序列化错误。

    反例：定义为基本数据类型 Boolean isDeleted；的属性，它的方法也是 isDeleted()，
         RPC框架在反向解析的时候，以为对应的属性名称是 deleted，导致属性获取不到，进而抛出异常。

9.【强制】包名统一使用小写，点分隔符之间有且仅有一个自然语义的英语单词。包名统一使用单数形式，但是类名如果有复数含义，类名可以使用复数形式。

    正例： 应用工具类包名为 com.alibaba.open.util、类名为 MessageUtils（此规则参考spring 的框架结构）

10.【强制】杜绝完全不规范的缩写，避免望文不知义。

    反例： AbstractClass“缩写”命名成 AbsClass；condition“缩写”命名成 condi，此类随意缩写严重降低了代码的可阅读性。

11.【强制】对于 Service 和 DAO 类，基于 SOA 的理念，暴露出来的服务一定是接口，内部的实现类用 Impl 的后缀与接口区别。

    正例：CacheServiceImpl 实现 CacheService 接口。

12.【强制】枚举类名建议带上Enum后缀，枚举成员名称需要全大写，单词间用下划线隔开。

    说明：枚举其实就是特殊的常量类，且构造方法被默认强制是私有。

    正例：枚举名字：DealStatusEnum，成员名称：SUCCESS/UNKOWN_REASON。

各层命名规约：

    A) Service/DAO 层方法命名规约
      1） 获取单个对象的方法用get 做前缀。
      2） 获取多个对象的方法用list 做前缀。
      3） 获取统计值的方法用count 做前缀。
      4） 插入的方法用 save（推荐）或 insert 做前缀。
      5） 删除的方法用 remove（推荐）或 delete 做前缀。
      6） 修改的方法用 update 做前缀。
    B) 领域模型命名规约
      1） 数据对象：xxxDO，xxx 即为数据表名。
      2） 数据传输对象：xxxDTO，xxx 为业务领域相关的名称。
      3） 展示对象：xxxVO，xxx 一般为网页名称。
      4） POJO 是 DO/DTO/BO/VO 的统称，禁止命名成 xxxPOJO。
#### 3.2常量定义
1.【强制】不允许任何魔法值（即未经定义的常量）直接出现在代码中。

    反例：String key = "Id#taobao_" + tradeId;

2.【强制】long 或者 Long 初始赋值时，必须使用大写的 L，不能是小写的 l，小写容易跟数字1混淆，造成误解。

    说明：Long a = 2l; 写的是数字的 21，还是 Long 型的 2?

3.【强制】不要使用一个常量类维护所有常量，应该按常量功能进行归类，分开维护。如：缓存相关的常量放在类：CacheConsts下；系统配置相关的常量放在类：ConfigConsts 下。

    说明：大而全的常量类，非得使用查找功能才能定位到修改的常量，不利于理解和维护。

4.【推荐】如果变量值仅在一个范围内变化，且带有名称之外的延伸属性，定义为枚举类。下面正例中的数字就是延伸信息，表示星期几。

    正例：public Enum { MONDAY(1), TUESDAY(2), WEDNESDAY(3), THURSDAY(4), FRIDAY(5), SATURDAY(6),SUNDAY(7);}
#### 3.3代码格式
1.【强制】大括号的使用约定。如果是大括号内为空，则简洁地写成{}即可，不需要换行；如果是非空代码块则：

    1） 左大括号前不换行。
    2） 左大括号后换行。
    3） 右大括号前换行。
    4） 右大括号后还有 else 等代码则不换行；表示终止的右大括号后必须换行。
2.【强制】 左小括号和字符之间不出现空格；同样，右小括号和字符之间也不出现空格。详见第 5 条下方正例提示。

    反例：if (空格 a == b 空格)
3.【强制】if/for/while/switch/do 等保留字与括号之间都必须加空格。

4.【强制】任何二目、三目运算符的左右两边都需要加一个空格。

    说明：运算符包括赋值运算符=、逻辑运算符&&、加减乘除符号等。
5.【强制】缩进采用 4 个空格，禁止使用 tab 字符。

    说明：如果使用 tab 缩进，必须设置 1 个 tab 为 4 个空格。IDEA 设置 tab 为 4 个空格时，请勿勾选 Use tab character；
        而在 eclipse 中，必须勾选 insert spaces for tabs。
    正例： （涉及 1-5 点）
        public static void main(String[] args) {
          // 缩进 4 个空格
          String say = "hello";
          // 运算符的左右必须有一个空格
          int flag = 0;
          // 关键词 if 与括号之间必须有一个空格，括号内的 f 与左括号，0 与右括号不需要空格
          if (flag == 0) {
              System.out.println(say);
          }
          // 左大括号前加空格且不换行；左大括号后换行
          if (flag == 1) {
              System.out.println("world");
              // 右大括号前换行，右大括号后有 else，不用换行
          } else {
              System.out.println("ok");
              // 在右大括号后直接结束，则必须换行
          }
        }

6.【强制】方法参数在定义和传入时，多个参数逗号后边必须加空格。

    正例：下例中实参的"a",后边必须要有一个空格。
         method("a", "b", "c");
#### 3.4 OOP 规约
1.【强制】避免通过一个类的对象引用访问此类的静态变量或静态方法，无谓增加编译器解析成本，直接用类名来访问即可。

2.【强制】所有的覆写方法，必须加@Override 注解。

    说明：getObject()与 get0bject()的问题。一个是字母的 O，一个是数字的 0，加@Override可以准确判断是否覆盖成功。
        另外，如果在抽象类中对方法签名进行修改，其实现类会马上编译报错。
3.【强制】相同参数类型，相同业务含义，才可以使用 Java 的可变参数，避免使用 Object。

    说明：可变参数必须放置在参数列表的最后。（提倡同学们尽量不用可变参数编程）
    正例：public User getUsers(String type, Integer... ids) {...}
4.【强制】外部正在调用或者二方库依赖的接口，不允许修改方法签名，避免对接口调用方产生影响。
接口过时必须加@Deprecated 注解，并清晰地说明采用的新接口或者新服务是什么。

5.【强制】不能使用过时的类或方法。

    说明：java.net.URLDecoder 中的方法 decode(String encodeStr) 这个方法已经过时，
    应该使用双参数 decode(String source, String encode)。接口提供方既然明确是过时接口，
    那么有义务同时提供新的接口；作为调用方来说，有义务去考证过时方法的新实现是什么。
6.【强制】Object 的 equals 方法容易抛空指针异常，应使用常量或确定有值的对象来调用equals。

    正例： "test".equals(object);
    反例： object.equals("test");
    说明：推荐使用 java.util.Objects#equals （JDK7 引入的工具类）
7.【强制】所有的相同类型的包装类对象之间值的比较，全部使用 equals 方法比较。

    说明：对于 Integer var = ? 在-128 至 127 范围内的赋值，Integer 对象是在IntegerCache.cache 产生，会复用已有对象，
        这个区间内的 Integer 值可以直接使用==进行判断，但是这个区间之外的所有数据，都会在堆上产生，
        并不会复用已有对象，这是一个大坑，推荐使用 equals 方法进行判断。
8.关于基本数据类型与包装数据类型的使用标准如下：

    1） 【强制】所有的 POJO 类属性必须使用包装数据类型。
    2） 【强制】RPC方法的返回值和参数必须使用包装数据类型。
    说明：POJO类属性没有初值是提醒使用者在需要使用时，必须自己显式地进行赋值，任何 NPE 问题，或者入库检查，都由使用者来保证。
    正例：数据库的查询结果可能是 null，因为自动拆箱，用基本数据类型接收有 NPE 风险。
    反例：比如显示成交总额涨跌情况，即正负 x%，x 为基本数据类型，调用的 RPC 服务，
        调用不成功时，返回的是默认值，页面显示：0%，这是不合理的，应该显示成中划线-。
        所以包装数据类型的 null 值，能够表示额外的信息，如：远程调用失败，异常退出。
9.【强制】定义 DO/DTO/VO 等 POJO 类时，不要设定任何属性默认值。

    反例：POJO 类的 gmtCreate 默认值为 new Date();但是这个属性在数据提取时并没有置入具体值，
         在更新其它字段时又附带更新了此字段，导致创建时间被修改成当前时间。
10.【强制】构造方法里面禁止加入任何业务逻辑，如果有初始化逻辑，请放在 init 方法中。

11.【强制】POJO 类必须写 toString 方法。使用 IDE 的中工具：source> generate toString时，如果继承了另一个 POJO 类，注意在前面加一下 super.toString。

    说明：在方法执行抛出异常时，可以直接调用 POJO 的 toString()方法打印其属性值，便于排查问题。
#### 3.5集合处理
1.【强制】关于 hashCode 和 equals 的处理，遵循如下规则：

    1）只要重写 equals，就必须重写 hashCode。
    2）因为 Set 存储的是不重复的对象，依据 hashCode 和 equals 进行判断，所以 Set 存储的对象必须重写这两个方法。
    3）如果自定义对象做为 Map 的键，那么必须重写 hashCode 和 equals。
    说明：String重写了hashCode 和 equals 方法，所以我们可以非常愉快地使用 String 对象作为 key 来使用。

2.【强制】ArrayList的subList结果不可强转成ArrayList，否则会抛出ClassCastException异常：java.util.RandomAccessSubList cannot be cast to java.util.ArrayList ;

    说明：subList 返回的是 ArrayList 的内部类 SubList，并不是 ArrayList ，
        而是 ArrayList 的一个视图，对于 SubList 子列表的所有操作最终会反映到原列表上。

3.【强制】在 subList 场景中，高度注意对原集合元素个数的修改，会导致子列表的遍历、增加、删除均产生 ConcurrentModificationException 异常。

4.【强制】使用集合转数组的方法，必须使用集合的 toArray(T[] array)，传入的是类型完全一样的数组，大小就是 list.size()。

    说明：使用 toArray 带参方法，入参分配的数组空间不够大时，toArray 方法内部将重新分配内存空间，
        并返回新数组地址；如果数组元素大于实际所需，下标为[ list.size() ]的数组元素将被置为 null，
        其它数组元素保持原值，因此最好将方法入参数组大小定义与集合元素个数一致。
    正例：
      List<String> list = new ArrayList<String>(2);
      list.add("guan");
      list.add("bao");
      String[] array = new String[list.size()];
      array = list.toArray(array);
    反例：直接使用 toArray 无参方法存在问题，此方法返回值只能是 Object[]类，若强转其它类型数组将出现 ClassCastException 错误。
5.【强制】使用工具类 Arrays.asList()把数组转换成集合时，不能使用其修改集合相关的方法，它的 add/remove/clear 方法会抛出 UnsupportedOperationException 异常。

    说明：asList 的返回对象是一个 Arrays 内部类，并没有实现集合的修改方法。
        Arrays.asList 体现的是适配器模式，只是转换接口，后台的数据仍是数组。
    String[] str = new String[] { "a", "b" };
    List list = Arrays.asList(str);
    第一种情况：list.add("c"); 运行时异常。
    第二种情况：str[0] = "gujin"; 那么 list.get(0)也会随之修改。
6.【强制】泛型通配符<? extends T>来接收返回的数据，此写法的泛型集合不能使用 add 方法，而<? super T>不能使用 get 方法，做为接口调用赋值时易出错。

    说明：扩展说一下 PECS(Producer Extends Consumer Super)原则：
        1）频繁往外读取内容的，适合用上界 Extends。
        2）经常往里插入的，适合用下界 Super。
7.【强制】不要在 foreach 循环里进行元素的 remove/add 操作。remove 元素请使用 Iterator方式，如果并发操作，需要对 Iterator 对象加锁。

    正例：
    Iterator<String> it = a.iterator();
     while (it.hasNext()) {
     String temp = it.next();
     if (删除元素的条件) {
            it.remove();
        }
     }
     反例：
     List<String> a = new ArrayList<String>();
     a.add("1");
     a.add("2");
     for (String temp : a) {
        if ("1".equals(temp)) {
            a.remove(temp);
        }
     }
    说明：以上代码的执行结果肯定会出乎大家的意料，那么试一下把“1”换成“2”，会是同样的结果吗？

8.【强制】在 JDK7 版本及以上，Comparator 要满足如下三个条件，不然 Arrays.sort，Collections.sort 会报 IllegalArgumentException 异常。

    说明：
         1） x，y 的比较结果和 y，x 的比较结果相反。
         2） x>y，y>z，则 x>z。
         3） x=y，则 x，z 比较结果和 y，z 比较结果相同。
         反例：下例中没有处理相等的情况，实际使用中可能会出现异常：
         new Comparator<Student>() {
         @Override
         public int compare(Student o1, Student o2) {
                return o1.getId() > o2.getId() ? 1 : -1;
            }
         };
#### 3.6语句规范
1.【强制】简单语句每一行只能包含一个语句。

    正例：argv++; // 正确
         argc--; // 正确
    反例：argv++; argc--;
2.【强制】不要在条件语句内用=, 这会与==混乱(同时适用于 while 语句内条件说明)

3.【强制】在混合运算表达式中使用括号避免运算优先级问题，即使对运算的优 先顺序非常清晰，也应该这么做。(同时适用于 while 语句内条件说明)

    正例：if ((a == b) && (c == d))
    反例：if (a == b && c == d)

4.【强制】每一个 Switch 的 case 建议有 default 做为最后出口

5.【强制】import 中标准的包名要在本地的包名之前。import 语句建议遵循以下导入顺序：

    1. jdk 标准包
    2. java 扩展包
    3. 使用外部库的包
    4. 使用的公共包
    5. 使用项目的公共包

6.【强制】import 语句尽量不使用通配符“*”(会加大程序编译时的开销和生成的类文件的大小)。

7.【强制】不要将变量的声明放在同一行。尽量在声明局部变量的同时初始化。唯一不这么做的理由是变量的初始值依赖于某些先前发生的计算。

    正例：int foo;
         int [] fooarray;
    反例：int foo, fooarray[];
8.【强制】避免声明的局部变量与上一级变量重名。
#### 3.7注释规约
1.【强制】类、类属性、类方法的注释必须使用 Javadoc 规范，使用/**内容*/格式，不得使用//xxx 方式。

    说明：在 IDE 编辑窗口中，Javadoc 方式会提示相关注释，生成 Javadoc 可以正确输出相应注释；在 IDE 中，工程调用方法时，
        不进入方法即可悬浮提示方法、参数、返回值的意义，提高阅读效率。
    例如：类注释：
               /**
                * @项目名称: yusp-admin
                * @类名称: AdminSmLogicSyResource
                * @类描述:
                * @功能描述:
                * @创建人: ????@yusys.com.cn
                * @创建时间: 2017-12-19 11:18
                * @修改备注:
                * @修改记录: 修改时间 修改人员 修改
                * 原因
                * @version 1.0.0
                * @Copyright (c) 2017宇信科技-版权所有
                */
        方法注释：
               /**
                * @方法名称:${方法名称}
                * @方法描述:
                * @参数与返回说明:
                * @算法描述:
                */
2.【强制】所有的抽象方法（包括接口中的方法）必须要用 Javadoc 注释、除了返回值、参数、异常说明外，还必须指出该方法做什么事情，实现什么功能。

    说明：对子类的实现要求，或者调用注意事项，请一并说明。
3.【强制】全局常量注释,注释需要使用多行注释。
### 四、异常日志
#### 4.1异常处理
1.【强制】Java 类库中定义的一类 RuntimeException 可以通过预先检查进行规避，而不应该通过 catch 来处理，比如：IndexOutOfBoundsException，NullPointerException 等等。

    说明：无法通过预检查的异常除外，如在解析一个外部传来的字符串形式数字时，通过 catch NumberFormatException 来实现。
    正例：if (obj != null) {...}
    反例：try { obj.method() } catch (NullPointerException e) {...}
2.【强制】异常不要用来做流程控制，条件控制，因为异常的处理效率比条件分支低。

3.【强制】对大段代码进行 try-catch，这是不负责任的表现。catch 时请分清稳定代码和非稳定代码，稳定代码指的是无论如何不会出错的代码。对于非稳定代码的 catch 尽可能进行区分异常类型，再做对应的异常处理。

4.【强制】捕获异常是为了处理它，不要捕获了却什么都不处理而抛弃之，如果不想处理它，请将该异常抛给它的调用者。最外层的业务使用者，必须处理异常，将其转化为用户可以理解的内容。

5.【强制】有 try 块放到了事务代码中，catch 异常后，如果需要回滚事务，一定要注意手动回滚事务。

6.【强制】finally 块必须对资源对象、流对象进行关闭，有异常也要做 try-catch。

    说明：如果 JDK7 及以上，可以使用 try-with-resources 方式。
7.【强制】不能在 finally 块中使用 return，finally 块中的 return 返回后方法结束执行，不会再执行 try 块中的 return 语句。

8.【强制】捕获异常与抛异常，必须是完全匹配，或者捕获异常是抛异常的父类。

    说明：如果预期对方抛的是绣球，实际接到的是铅球，就会产生意外情况。
#### 4.2日志规约
1.【强制】应用中不可直接使用日志系统（Log4j、Logback）中的 API，而应依赖使用日志框架SLF4J 中的 API，使用门面模式的日志框架，有利于维护和各个类的日志处理方式统一。

    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    private static final Logger logger = LoggerFactory.getLogger(Abc.class);
2.【强制】日志文件推荐至少保存 15 天，因为有些异常具备以“周”为频次发生的特点。

3.【强制】应用中的扩展日志（如打点、临时监控、访问日志等）命名方式：

    appName_logType_logName.log。logType:日志类型，推荐分类有
    stats/desc/monitor/visit 等；logName:日志描述。这种命名的好处：
    通过文件名就可知道日志文件属于什么应用，什么类型，什么目的，也有利于归类查找。
    正例：mppserver 应用中单独监控时区转换异常，如：mppserver_monitor_timeZoneConvert.log
    说明：推荐对日志进行分类，如将错误日志和业务日志分开存放，便于开发人员查看，也便于通过日志对系统进行及时监控。
4.【强制】对 trace/debug/info 级别的日志输出，必须使用条件输出形式或者使用占位符的方式。

    说明：logger.debug("Processing trade with id: " + id + " symbol: " + symbol);
    如果日志级别是 warn，上述日志不会打印，但是会执行字符串拼接操作，如果 symbol 是对象，
    会执行 toString()方法，浪费了系统资源，执行了上述操作，最终日志却没有打印。
    正例：（条件）
        if (logger.isDebugEnabled()) {
          logger.debug("Processing trade with id: " + id + " symbol: " + symbol);
        }
    正例：（占位符）
        logger.debug("Processing trade with id: {} symbol : {} ", id, symbol);
5.【强制】避免重复打印日志，浪费磁盘空间，务必在 log4j.xml 中设置 additivity=false。

    正例：<logger name="com.taobao.dubbo.config" additivity="false">
6.【强制】异常信息应该包括两类信息：案发现场信息和异常堆栈信息。如果不处理，那么通过关键字 throws 往上抛出。

    正例：logger.error(各类参数或者对象 toString + "_" + e.getMessage(), e);
