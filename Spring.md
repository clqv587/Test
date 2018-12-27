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
       * 在单例中会帮我们建立对象后初始化和销毁前调用destory-method  @PostConstruct  
       * 多例中会初始化但不会在销毁前调用destory-method  @PreDestroy   
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
* 动态代理  
    * 原理：创建动态代理对象，增强原来的方法，JDK中proxy，spring中cglib来创建动态代理对象，proxy是  
    实现统一接口，cglib是继承，都是在程序运行时期生成对应的字节码  
    * WHAT + WHERE + WHEN  
    * \<aop:config>  
       * \<aop:ascept ref="增强方法类">  <aop:pointcut excetion="asceptj语法(指明增强方法)" id="">  
       <aop:before(前置增强) after(最终增强) afterreturning(正常) afterthrowing(异常)>   
       </aop:ascept>  
    * 增强类中方法参数  
       * 异常增强（joinpoint（joinpoint必须为第一个参数），throwable）  
       joinpoint不用在xml中配，但throwable要配\<afterthrowing method="" pointcut-ref="aop的id" throw="">
       * 正常（joinpoint） 
       * around增强（proccedjoinpoint）  
* 注解开发动态代理  
    * aop注解解析器  
       * \<aop:asceptj-autoproxy proxy-trage-class="false(false使用proxy，true使用cglib)"/>  
    * 在增强的方法类上贴 @ascept  
    * 定义一个方法，名字相当于xml中的id，贴上@pointcut("execution表达式")  
    * 在增强方法上贴上@before或@afterreturning...(可以写要传入的参数（joinpoint可以不写）,value="pointcut中的id加上（）")   
    注意实际开发可能先执行finaly再执行afterretruning，所以实际开发around用得多  
* 对事物进行aop   
    * 配置事务管理器DataSourceTransactionManager\<bean id="" class=""> <porperties name="datasoruce" ref="druid连接池beanid">  
    * 配置事务增强配置  
   \<tx:advice id="" transaction-manager="事务管理器id">  
           <tx:attributes>  
              <tx: method   有各种属性 read-onlyxx表示查询>  
            <tx:attributes/>  
    <tx:advice>         
    * 配置aopconfig,<aop:pointcut> <aop:advisor> </aopconfig>  
    * spring事务主要是三个接口类 datasourcetransaction transactiondefne transactionstatus
* 注解开发事务  
       * 在xml中写事务注解扫描器 \<tx:annotation-driven transaction-manager="配置事务管理器的id(默认transactionManager)"/>  
       * 在要使用事务的server类上贴@transaction,如果某一方法为查询，可以在方法上贴@Tracsaction(read-only=true)  
* 使用java代码来代替xml  
       * 使用@configuration 贴在类上 来标明当前类为配置类  
       * 使用@import(xx.class)贴在类上 来标明引入其他的class  
       * 使用@properties("classpath:")贴在类上, 来引入外部properties配置  
       * 使用@componentscan贴在类上 来开启扫描IoC注解，会自动扫描当前包和子包  
       * 使用@bean 贴在方法上，方法返回的类即是被spring管理的bean，需要注入的类对象直接在方法里写形参即可，spring会根据形参的类型来找spring管理的bean来注入  
       * 测试类里写springjuitconfig（classes=xxx.class） 
       * 使用@enabletransactionmanager表示开启事务注解扫描，
       













