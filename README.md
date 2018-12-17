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
   mapper中使用<collection properties="" cloumn="" javatype="" select="">
   * 如果返回的是多想，则用联合查询（即多表查询）  
   mapper中使用<association >
 
* 多对一  （类设计和多对多一样，也多了唯一约束） 
* 多对多  
* 延迟加载（额外sql）
    * 在mybatis_config.xml中的settings里加<setting name="lazyloadinge.." value="true" >  
   <setting name="aggress.." value="false">  
      <setting name="lazyload..method" value="clone">  
* 缓存待续...
