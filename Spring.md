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
