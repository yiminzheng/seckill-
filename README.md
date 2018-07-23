# secKill
项目针对高并发和商品秒杀整合了SSM框架 在IDEA上创建Maven项目，配置pom.xml和web.xml day01--编写Dao层：首先创建数据库并建表，秒杀商品库存表和成功秒杀明细表 根据数据库中表创建实体类，即秒杀商品信息实体类seckill和秒杀商品状态successkill实体类 再创建实体类对应的mapper接口即dao接口，接口中复写各自的特有方法：如查询商品信息和秒杀商品明细 再建立对应的mapper包存放为dao接口方法提供的sq语句的xml配置 然后建立mybatis-config配置文件，和spring-dao配置文件将spring-mybatis整合 创建测试方法通过单元测试 整合mybatis和spring思路是将sql语句放在sqlsessionfactory中交给spring来管理，将mapper和xml配合起来使用。

day02--编写service层：该层主要负责业务逻辑模块的应用设计 站在使用者的角度先设计seckillservice接口，定义方法然后Impl实现这些方法，实现类编写过程中会产生返回数据，为了简化代码提高复用性 再编写Dto类（数据传输对象），该项目中表现为秒杀活动url地址，秒杀商品返回的状态明细等 expection类（异常），该项目中表现为秒杀接口关闭，重复秒杀商品和秒杀失败等异常 为了增加返回执行结果的观赏性，增加了一个枚举类statenum来存放常量数据字段 然后建立spring-service配置文件注入service并结合使用注解方法 创建测试方法通过单元测试

day03--编写web层：View(页面)>Controller(控制层)>Service(业务逻辑)>Dao(数据访问)>Database(数据库) web层负责编写控制层和view页面，view页面通过前端框架bootstrap编写 首先修改web.xml，引入springmvc的dispatcherservlet配置 整合spring-springmvc之后实现秒杀restful方法用来传输结果 然后编写controller类，建立一个全局ajax请求返回类,返回json类型 进入前端页面先获取系统时间判断秒杀活动是否开启，再决定跳转到对应的页面处理 该层除了前端编写，后端主要实现controller类配置dispatcherservlet参数