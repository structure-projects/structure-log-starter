# structure-log-starter
一个日志输出的封装

## 功能 
1. web接口 Log 
2. 方法Log 
3. 默认json化主要用于给elk做日志收集使用

### web接口的开启
默认开启了 WebAopLog 的功能需要配置aop的切入点
```yaml
structure:
  log:
    aop:
      expression: execution(public * cn.structure.example.log.controller..*Controller.*(..))
```
方法二 利用开关开启和关闭webLog
```yaml
structure:
  log:
    aop:
      enable: false
      expression: execution(public * cn.structure.example.log.controller..*Controller.*(..))
```
使用 EnableWebAopLog 注解则开关无效
```java
/**
 * <p>
 * 日志例子启动器
 * </p>
 *
 * @author chuck
 * @version 1.0.1
 * @since 2021/1/3 14:12
 */
@EnableWebAopLog
@SpringBootApplication
public class LogApplication {
    public static void main(String[] args) {
        SpringApplication.run(LogApplication.class,args);
    }
}
```

### 方法Log 的使用 

```java
    /**
     * 使用 AspectParamLog 对方法的日志进行记录
     * @param reqTestVO
     * @return
     */
    @AspectParamLog()
    @RequestMapping(value = "test")
    public ResTestVO testLog (@RequestBody ReqTestVO reqTestVO) {
        ResTestVO resTestVO = new ResTestVO();
        resTestVO.setId(reqTestVO.getId());
        resTestVO.setName(reqTestVO.getName());
        return resTestVO;
    }
```
### 日志需要配置 spring.application.name 
```yaml
spring:
  application:
    name: log-example
```