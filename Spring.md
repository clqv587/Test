# spring笔记  
* 注入底层  
    * resources = new classresource()  
    * beanfactory = new xmlbeanfactory(resources)  
    * beacfactory.getbean(.class,"")
* xml  
    * \<bean id="" class="">\<porpertie name="" vlaue="">\<bean>  
    * 导入其他配置xml  
        \<import resource="classpath:" />  
* Spring测试框架
    * @RunWith(SpringJUnit4ClassRunner.class)  
    * @ContextConfiguration("classpath:")  
    * Junit5测试    @SpringJUnitConfig  默认找当前类名-context.xml  
* 建议使用applicationcontext而不是beanfactory  
    * appcon会在建立对象时就创建好bean工厂中需要的对象而beanfactory不会  
    * 可以在\<bean lazy-init="true">设置为懒加载  
* bean实例化方式  
    * 构造器实例化  
    * 静态工厂方法实例化  
       * \<bean id="" class="" factory-method="">  
    * 非静态实例化工厂（两个bean）  
       * \<bean id="" class="">  
       * \<bean id="" factory-bean="(工厂beanid)" factory-method="">  
    * 实现factorybean接口的工厂类
       * \<bean id="" class>  
* bean作用域       
    * \<bean id class scope="singleton">  单例  
    * scope="prototype"  多例  
    * scope="request"  针对web请求，每次请求都是一个新的bean  
    * scope="session"  针对wen会话，不同的会话，bean不同  
* bean生命周期  
    * \<bean init-method="" destory-method="">  
       * 在单例中会帮我们建立对象后初始化和销毁前调用destory-method  
       * 多例中会初始化但不会在销毁前调用destory-method  
       * 销毁前调用建立在applicationcontext对象正常关闭的前提下  
* di（注入依赖）   
   * 在bean元素中设置\<bean autowired="type/name/custor../defalut/no">  
       * 自动注入引用类型，通过class，属性名和beanid对应，构造器（通过class），不自动注入  
   * 通过setter注入  
       * bean元素中包含porperty子元素,   通过name（要设置的属性），value（普通值类型,填写值）  
       * bean元素中包含porperty子元素,   通过name（要设置的属性），或ref(引用的beanid)  
       * bean元素中包含porperty子元素,   通过name（要设置的属性），再在porperty中子元素list，set，array的子元素设置value或bean，map中有entry
       中的key，value或key，ref，porperties写子元素value xxx=xxx  
   * 构造器注入  
       * bean元素包含constructor-arg子元素，通过type,index,name(参数名)确定形参的位置，通过value,ref.  
       可以在constructor-arg里面写得bean为内部bean，\<bean class="">不用写id  
* bean继承(即使用同样属性)  
    * 先把定义一个bean\<bean id="" abstract="true">  
    * 子类声明父类\<bean parent="">  
* 加载db.properties  
    * 先引入命名空间  
    * \<context:porperties-placeholder loacltion="classpath:" >  
    * 让spring还可以继续解析\<context:porperties-placeholder ignore-unresolve="true"> 解决配置了多行porperties-placeholder不能解析问题
    * **注意和系统引用冲突**  
* 注入自动注解    
    * 在spring.xml中,\<context:annotation-config /> 表示解析打上autowried标签的代码  
    * autowried会先找同类型 再找名字（id和字段名）和resouce一样   
    * qualifier 通过id注入  
    * value 注入常量  
* IoC注解  
    * 在spring.xml中配置扫描配置了component的类，\<context:component-scan basepackge="">
    * component 把该类给spring实例化,@component("id"),不写id，默认为类名首字母小写
    * @server（服务），@contoral（控制器），@respository（dao）和component一样是把该类给spring管理  
    * @scope 定义bean为单例还是多例  
    * @postconstruct 贴在初始化方法上 会在构建对象后立即执行此方法  
    * @predestory 贴在销毁方法上  




















