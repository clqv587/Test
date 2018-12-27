# mybatis笔记
* 主要类  
   sqlsessionbuildfactory  
   sqlsessionbuild  
   sqlsession  
   mapper和mapper.xml和mybatis_config.xml  
* 动态sql  
* 对象关系  
* 一对一  （类设计和一对多一样，只不过多了唯一约束）
* 一对多  
   
   * 外键在many方维护，如果返回是集合，建立使用额外sql，并设置延迟加载  
   mapper中使用\<collection properties="" cloumn="" javatype="" select="">
   * 如果返回的是多想，则用联合查询（即多表查询）  
   mapper中使用\<association >
 
* 多对一  （类设计和多对多一样，也多了唯一约束） 
* 多对多  
* 延迟加载（额外sql）
    * 在mybatis_config.xml中的settings里加\<setting name="lazyloadinge.." value="true" >  
   \<setting name="aggress.." value="false">  
      \<setting name="lazyload..method" value="clone">   
* 获取自动生成的主键  
\<insert useGeneratedKeys="true" keyProperty/>  
* 注解开发  
    * @param注解是在mapper接口中方法传参用的，由于mapper只接受对象或map结构，底层是把参数封装成map，在ognl表达式好提取  
    * @insert 贴在mapper接口上，用来实现此方法，配合@opinion使用  
    * @delete @update   
    * @select 配合@result使用 ，还需定义@results（id="",@result(colum=,property=)）  
**注意：#和$的区别，#会把值当成预编译中的占位符，会带上单引号。$不会参与预编译**    
* 缓存待续...
