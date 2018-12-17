# mybatis笔记
* 主要类  
   sqlsessionbuildfactory  
   sqlsessionbuild  
   sqlsession  
   mapper和mapper.xml和mybatis_config.xml  
* 动态sql  
* 对象关系  
* 一对多  
   * 关系在many方维护，如果返回是集合，建立使用额外sql，并设置延迟加载  
   mapper中使用<collection select="">
   * 如果返回的是多想，则用联合查询（即多表查询）  
   mapper中使用<association >
* 一对一  
*  多对多  
 
