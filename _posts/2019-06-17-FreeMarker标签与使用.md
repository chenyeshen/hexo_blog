---
layout:     post
title:      FreeMarker标签与使用
subtitle:   学习笔记
date:       2019-06-17
author:     chenyeshen
header-img: img/img17.jpg
catalog: true
tags:
    - 模板引擎
    - FreeMarker
---



​    那么现在开源的模板技术有好几种，多了之后就有一个选择的问题了，如何选择一个满足自己需要的模板的呢，写了一个例子，我使用了几种设计模式来完成了这个例子，这个例子中，同时使用了freemarker和velocity，这样同学们可以通过代码很直观的比较两种模板技术，通过这个例子，我认识到freemarker在功能上要比velocity强大 
1。在view层的时候，它提供了format日期和数字的功能，我想大家都有在页面上format日期或数字的经验，用jsp的同学可能对jstl的fmt标签很有感情，使用了freemarker之后也可以使用freemarker提供的功能来formmat日期和数据，这个功能我想是很贴心的



2。freemarker对jsptag的支持很好，算了，不到迫不得已还是不要这样做吧。

还有就是两者的语法格式，这一点上不同的人有不同倾向

下面就先介绍标签吧

 

# 二、表达式 

表达式是FreeMarker的核心功能。表达式放置在插值语法（${...}）之中时，表面需要输出表达式的值，表达式语法也可以与FreeMarker标签结合，用于控制输出

####     1、直接指定值

​      例如：
​      a、字符串
​         ${'我的名字是\"yeek\"'};
​         ${"我的文件保存在d：\\盘"};
​      b、数值
​      c、布尔值
​      d、日期型
​         FreeMarker支持date、time、datetime三种类型，这三种类型的值无法直接指定，通常需要借助字符串的date、time、datetime三个内建函数进行转换才可以
​           <#assign test1 = "2009-01-22"?date("yyyy-MM-dd") />;
​           <#assign test2 ="16:34:43"?time("HH:mm:ss") />
​           <#assign test2 = "2009-01-22 17:23:45"?datetime("yyyy-MM-dd HH:mm:ss") />
​           ${test1?string.full}

####       e、集合

​        集合以方括号包括，各集合元素之间以英文逗号(,)分隔，看如下的示例:
​      <#list["星期一",,["星期二",["星期三",["星期四",["星期五"] as x>
​         ${s};
​        </#list>

####       f、Map集合

​         Map对象使用花括号包括，Map中的key-value对之间以英文冒号(:)隔开，多组key-value对之间以英文逗号(,) 隔开
​           例如
​           <#assign score = {"语文":78,"数学":83,"Java":89} >
​             <#list score?key as x>
​              ${x}--->${score[x]};
​             </#list>

####       2、输出变量值

​          FreeMarker的表达式输出变量时，这些变量可以是顶层变量，也可以是Map对象中的变量，还可以是集合中的变量，并可以使用点(.)语法来访问Java对象的属性
​          a、顶层变量
​             Map root = new HashMap();
​             root.put("name","wenchao");
​             对应顶层变量，直接使用${variableName}来输出变量值，变量名只能是数字、字母、下划线、$、@和#的组合，并不能以数字开头

####           b、输出集合元素

​             如果需要输出集合元素，则可以根据集合元素的索引来输出元素。集合元素的索引以方括号指定。
​             假设有集合对象为：["星期一","星期二","星期三","星期四","星期五","星期六"],该集合对象名为week, 如果需要输出星期三，则可以使用如下语法：
​                ${week[2]}
​             集合里的第一个元素的索引是0
​          c、输出Map元素
​              这里的Map对象可以是直接HashMap的实例，甚至包括 JavaBean实例，对应JavaBean实例，我们一样可以把其当成属性为key，属性为value的Map实例
​      3、字符串操作
​         a、字符串链接
​           字符串连接有两种语法
​           A、使用${..}(或#{..})在字符串常量部分插入表达式的值，从而完成字符串连接
​           B、直接使用连接运算符（+）来连接字符串
​             使用第一种语法来连接字符串
​             ${"Hello,${user}!"}
​              第二种使用连接符号来连接字符串
​             ${"Hello,"+user+"!"};
​               值的注意的是，${..}只能用于文本部分，因此，下面的代码是错误的：
​                 <#if ${isBig}>Wow!</#if>
​                 <#if "${isBig}">Wow!</#if>
​                 应该写成：
​                 <#if isBig>Wow!</#if>

####          b、截取字符串

​            Map root = new HashMap();
​            root.put("book","疯狂Ajax讲义")；
​            ${book[0]}
​            ${book[4]}
​            ${book[1..4]}

####       4、集合连接运算符

​        这里所说的集合连接运算时将两个集合连接成一个新的集合，连接集合的运算符是+，例如
​        <#list ["星期一"," 星期二","星期三"]+["星期四","星期五"] as x>
​           ${x}
​        </#list>

####       5、Map连接运算符

​             Map对象的连接运算也是将两个Map对象连接成一个新的Map对象，Map对象的连接运算符是+。如果两个Map对象具有相同的 key，则后加入Map里的key所
​         对应的value替代原来key所对应的value

####       6、算术运算符

​         FreeMarker表达式中完全支持算术运算，FreeMarker支持的算术运算符包括： +，-，*，/，%
​         看如下代码示范
​           <#assign x = 5 />
​           ${x* -100}
​           ${x/2}
​           ${12%10}
​         在表达式中使用算术运算时要注意以下几点。
​         A、运算符两边的运算数必须是数字，因此下面的代码是错误的：
​           ${3*"5"}
​         B、使用+（既可以作为加号，也可以作为字符串连接运算符）运算时，如果一边是数字，一边是字符串，就会自动将数字转化为字符串。例如
​            ${3+"5"}
​            输出结果：35
​         C、使用内建的int函数可对数值取整。例如
​            <#assign x = 5>
​            ${(x/2)?int}
​            ${1.1?int}
​            ${1.999?int}
​            ${-1.9999?int}
​            ${-1.1?int}

####        7、比较运算符

​           表达式中支持的比较运算符有如下几个
​           a、=（或者==）:判断两个值是否相等.
​           b、!=:判断两个值是否不相等
​           c、 >(或者gt):判断坐标值是否大于右边值
​           d、 >=(或者gte):判断坐标值是否大于等于右边值
​           e、 <(或者lt):判断左边值是否小于右边值
​           f、 <=(或者lte):判断左边值是否小于等于右边值          

####        8、逻辑运算符

​          逻辑运算符有如下几个
​          a、逻辑与：&&
​          b、逻辑或：||
​          c、逻辑非：!
​          逻辑运算符只能作用于布尔值，否则将产生错误。

####        9、内建函数

​          FreeMarker还提供了一些内建函数来转换输出，可以在任何变量后紧跟?,?后紧跟内建函数，就可通过内建函数来转换输出变量
​          下面是常用的内建的字符串函数
​          a、html：对字符串进行HTML编码
​          b、cap_first:将字符串第一个字母成大写
​          c、lower_case:将字符串转换成小写
​          d、upper_case:将字符串转换成大写
​          e、trim: 去掉字符串前后的空白字符
​          下面是集合的常用的内建函数
​          a、size： 获得序列中元素的数目
​          下面是数字值的常用的内建函数
​          a、int 取得数字的整数部分
​          例如
​          <#assign test="Tom & Jerry" />
​          ${test?html}
​          ${test?upper_case?html}

####        10、空值处理运算符

​          FreeMarker对空值的处理非常严格，FreeMarker的变量必须有值，没有被赋值的变量就会抛出异常。

####        11、运算符优先级

### **  三、FreeMarker 的常用指令**     1、if指令

####         分支控制语句

​        语法格式如下
​       <#if condition>
​            ....
​       <#elseif condition2>
​          ...
​       <#elseif condition3>      
​          ...
​       <#else>
​          ...
​       </#if>

####      2、switch、case、default、break指令

​        <#switch value>
​           <#case refValue>
​              ...
​              <#bread>
​           <#case refValue>
​              ...
​              <#bread>
​           <#default>
​              ...
​        </#switch>
​        虽然FreeMarker提供了switch指令，但它并不推荐使用switch指令来控制也输出，而是推荐使用FreeMarker的if..elseif..else 指令来替代它。

####     3、list、break指令

​    list指令时一个典型的迭代输出指令，用于迭代输出数据模型中的集合。list指令的语法格式如下：
​     <#list sequence as item>
​       ...
​     </#list>
​      除此之外，迭代集合对象时，还包括两个特殊的循环变量：
​      a、item_index：当前变量的索引值。
​      b、item_has_next:是否存在下一个对象
​      也可以使用<#break>指令跳出迭代
​      <#list ["星期一","星期二","星期三","星期四","星期五"] as x>
​          ${x_index +1}.${x} <#if x_has_next>,</#if>
​          <#if x = "星期四"><#break></#if>
​      </#list>

####       4、include 指令

​        include指令的作用类似于JSP的包含指令，用于包含指定页，include指令的语法格式如下
​         <#include filename [options]
​          在上面的语法格式中，两个参数的解释如下
​          a、filename：该参数指定被包含的模板文件
​          b、options：该参数可以省略，指定包含时的选项，包含encoding和parse两个选项，encoding指定包含页面时所使用的解码集，而parse指定被
​             包含是否作为FTL文件来解析。如果省略了parse选项值，则该选项值默认是true

####      5、 import指令

​        该指令用于导入FreeMarker模板中的所有变量，并将该变量放置在指定的Map对象中，import 指令的语法格式如下
​        <#import path as mapObject>
​        在上面的语法格式中，path指定要被导入的模板文件，而mapObject是一个Map对象名，通过这行代码，将导致path模板中的所有变量都被放置
​        在mapObject中
​        <#import "/lib/common.ftl" as com>

####      6、noparse指令

​         noparse指令指定FreeMarker不处理该指令里包含的内容，该指令的语法格式如下：
​         <#noparse>
​            ...
​         </#noparse>

####      7、escape、noescape指令

####      8、assign指令

​        它用于为该模板页面创建或替换一个顶层变量

####      9、setting指令

​        该指令用于设置FreeMarker的运行环境，该指令的语法格式如下：
​        <#setting name = value>
​        name 的取值范围包括如下几个
​         locale ：该选项指定该模板所用的国家/语言选项
​         number_format:该选项指定格式化输出数字的格式
​         boolean_format:该选项指定两个布尔值的语法格式，默认值是"true、false"
​         date_format,time_format,datetime_format：该选项指定格式化输出日期的格式
​         time_zone:  设置格式化输出日期时所使用的时区

####      10、macro、nested、return指令

 

下面再介绍一个例子

Java代码

public class TemplateTest {  
​    /** 
​     * @param args 
​     */  
​    public static void main(String[] args) throws Exception{  
​        /* 准备数据 */  
​        Map latest = new HashMap();  
​        latest.put("url", "products/greenmouse.html");  
​        latest.put("name", "green mouse");  
​        Map root = new HashMap();  
​        root.put("user", "Big Joe");  
​        root.put("latestProduct", latest);  
​        root.put("number", new Long(2222));  
​        root.put("date",new Date());  
​        List listTest = new ArrayList();  
​        listTest.add("1");  
​        listTest.add("2");  
​        root.put("list",listTest);  
​        TemplateEngine freemarkerEngine = (TemplateEngine)TemplateFactory.getInstance().getBean("freemarker");  
​        freemarkerEngine.run(root);//使用freemarker模板技术  
​        TemplateEngine velocityEngine = (TemplateEngine)TemplateFactory.getInstance().getBean("velocity");  
​        velocityEngine.run(root);//使用velocity模板技术  
​    }  
} 

 

工厂类，用来得到模板引擎

Java代码

public class TemplateFactory {  
​    private static TemplateFactory instance;  
​    private Map objectMap;  
​    static{  
​        instance = new TemplateFactory();  
​    }  
​    public TemplateFactory() {  
​        super();  
​        this.objectMap = new HashMap();  
​        synchronized (this) {  
​            objectMap.put("freemarker", new FreemarkerTemplateEngine(){  
​                public String getTemplatePath() {  
​                    return "template";  
​                }  
​            });  
​            objectMap.put("velocity", new VelocityTemplateEngine());  
​        }  
​    }  
​    public static TemplateFactory getInstance(){  
​        return instance;  
​    }  
​    /** 
​     * 模仿spring的工厂 
​     * @param beanName 
​     * @return 
​     */  
​    public Object getBean(String beanName){  
​        return objectMap.get(beanName);  
​    }  
} 

 

引擎接口

Java代码

public interface TemplateEngine {  
​    void run(Map context)throws Exception;  
} 

 

模板引擎的实现使用method template模式，因为有两个实现，这两个实现又存在公共的逻辑，所以选择了这个模式

Java代码

public abstract class AbstractTemplateEngine implements TemplateEngine{  
​    public abstract String getTemplatePath();  
​    public abstract String getTemplate();  
​    public abstract String getEngineType();  
​    public void run(Map context)throws Exception{  
​        if(Constants.ENGINE_TYPE_FREEMARKER.equals(getEngineType()))  
​            executeFreemarker(context);  
​        else  
​            executeVelocity(context);  
​    }  
​    private void executeFreemarker(Map context)throws Exception{  
​        Configuration cfg = new Configuration();  
​        cfg.setDirectoryForTemplateLoading(  
​                new File(getTemplatePath()));  
​        cfg.setObjectWrapper(new DefaultObjectWrapper());  
​        cfg.setCacheStorage(new freemarker.cache.MruCacheStorage(20, 250));  
​        Template temp = cfg.getTemplate(getTemplate());  
​        Writer out = new OutputStreamWriter(System.out);  
​        temp.process(context, out);  
​        out.flush();  
​    }  
​    private void executeVelocity(Map root)throws Exception{  
​        Velocity.init();  
​        VelocityContext context = new VelocityContext(root);  
​        org.apache.velocity.Template template = null;  
​        template = Velocity.getTemplate(getTemplatePath()+getTemplate());  
​        StringWriter sw = new StringWriter();  
​        template.merge( context, sw );  
​        System.out.print(sw.toString());  
​    }  
} 

 

这个是freemarker实现

Java代码

 

public class FreemarkerTemplateEngine extends AbstractTemplateEngine{  
​    private static final String DEFAULT_TEMPLATE = "FreemarkerExample.ftl";  
​    /** 
​     * 这个方法应该实现的是读取配置文件 
​     */  
​    public String getTemplatePath() {  
​        return null;  
​    }  
​    public void run(Map root) throws Exception{  
​        super.run(root);  
​    }  
​    public String getTemplate() {  
​        // TODO Auto-generated method stub  
​        return DEFAULT_TEMPLATE;  
​    }  
​    public String getEngineType() {  
​        return Constants.ENGINE_TYPE_FREEMARKER;  
​    }  
}

 

这个是velocity实现

Java代码

 public class VelocityTemplateEngine extends AbstractTemplateEngine{  
private static final String DEFAULT_TEMPLATE = "VelocityExample.vm";  
​    public String getTemplatePath() {  
​        return "/template/";  
​    }  
​    public void run(Map map) throws Exception{  
​        super.run(map);  
​    }  
​    public String getTemplate() {  
​        // TODO Auto-generated method stub  
​        return DEFAULT_TEMPLATE;  
​    }  
​    public String getEngineType() {  
​        // TODO Auto-generated method stub  
​        return Constants.ENGINE_TYPE_VELOCITY;  
​    }  
}

 

以下是模板 
1，freemarker模板 
Java代码

freemarker template test:  
string test-----------${user}-----------${number}-----------${latestProduct.url}-----------${latestProduct.name}  
condition test-----------  
<#if user == "Big Joe">  
list iterator-----------  
<#list list as aa>  
${aa}  
</#list>   
</#if>  
date test-----------${date?string("MMM/dd/yyyy")}    

2，velocity模板

至此整个例子就结束了，这个例子比较直观的表现两种技术的应用

 

 

 
