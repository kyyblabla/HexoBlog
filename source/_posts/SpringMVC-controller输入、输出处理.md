---
title: SpringMVC controller输入、输出处理
tag:
  - java
  - springMVC
  - controller
categories:
  - java
date: 2017-03-19 20:58:18
---

以RESTful应用为前提，在controller方法中，往往要注入一些固定的对象，如当前用户、权限信息等。而且还要返回固定格式的数据以供前端处理，这里介绍一些常在项目中使用的处理方法。


<!-- more -->


以RESTful应用为前提，在controller方法中，往往要注入一些固定的对象，如当前用户、权限信息等。而且还要返回固定格式的数据以供前端处理，这里介绍一些常在项目中使用的处理方法。

## 注入自定义参数

如下接口用来获取当前用户的地址信息，可以直接在方法中注入用户对象，然而spring参数Resolver并不能直接解析出SessionUserBean，用户信息可能存储于缓存中，通过token标示获取。
```
//SessionUserBean用来存储与表示当前回话用户信息
public class SessionUserBean {     
private Integer userId;
}

@RequestMapping("/address")
public void getAddress(SessionUserBean sessionUser){
//do something
}
```

可以通过实现HandlerMethodArgumentResolver来定义自己的处理器：
```
public class SessionUseResolver implements HandlerMethodArgumentResolver {   

@Override    
public boolean supportsParameter(MethodParameter methodParameter) {
//只处理指定的对象       
 return methodParameter.getParameterType().equals(SessionUserBean.class);  
}

@Override    
public Object resolveArgument(MethodParameter methodParameter, ModelAndViewContainer modelAndViewContainer, NativeWebRequest nativeWebRequest, WebDataBinderFactory webDataBinderFactory) throws Exception {        
HttpServletRequest req = (HttpServletRequest) nativeWebRequest.getNativeRequest();
//这里通过HttpServletRequest的某些头信息获取用户信息
SessionUserBean sessionUser = SessionUserUtil.getSessionUser(req);       
return sessionUser;    
}
}
```
在springboot项目中可通过配置类注册解析器，xml配置方法也是类似方式。
```
@Configurationpublic 
class WebMvcConfig extends WebMvcConfigurerAdapter {      
@Override    
public void addArgumentResolvers(List<HandlerMethodArgumentResolver> argumentResolvers) {        
argumentResolvers.add(new SessionUseResolver());      
//...
}
```
之后便可以在任何需要注入的controller方法中注入对象了。

## 统一封装返回值

假定api统一的返回数据类型如下：
```
public class ResponseVo {    
private String message;   
private Object data;   //接口处理结果 
private String code = "200";  //状态吗，正常时为200，否则为异常码
}
```
我们期望在在controller方法中直接返回业务对象（非ResponseVo对象）或者是不返回任何东西（也代表处理成功），但是最终http请求相应的数据仍未统一的格式，那么可以用@ControllerAdvice来简单的实现我们的需求。

```
@ControllerAdvice
public class ResponseVoAdvice implements ResponseBodyAdvice<Object> {    
@Autowired   
private HttpServletRequest httpServletRequest;    
@Autowired    
private Environment environment;    
@Override    
public boolean supports(MethodParameter returnType, Class converterType) {        
  if (returnType.getMethodAnnotation(RequestMapping.class) != null) {            
    String typeName = returnType.getGenericParameterType().getTypeName();            
   //只处理非 ResponseVo 的返回值类型，包括void类型也会被处理
   if (!StringUtils.equals(typeName, ResponseVo.class.getTypeName())) {                
      return true;            
    }        
  }        
  return false;    
}   
@Override   
public Object beforeBodyWrite(Object body, 
  MethodParameter returnType, 
  MediaType selectedContentType, Class<? extends HttpMessageConverter<?>> selectedConverterType, 
  ServerHttpRequest request, 
  ServerHttpResponse response) {        
  if (body instanceof MappingJacksonValue) {            
    MappingJacksonValue mv = (MappingJacksonValue) body;            
    //构建结果对象
    ResponseVo success = ResponseVo.success(mv.getValue());            
    if (EnvironmentUtil.isTestEvn(environment)) { 
    //测试环境下加入debug信息      
        success.set_debug(httpServletRequest.getAttribute(SYSTEM.RESPONSE_DEBUG));            
    }            
    return success;        
    } else {            
      return body;        
    }    
 }
}
```
上面的示例中只处理正常情况下的数据封装，当业务出现异常时，会由异常处理器统一处理返回结果。

## 还有更多
以上就是一些对于controller方法输入、输出处理的小case，事实上有无数种方法可以达到同样的效果，如修改默认的json序列化类。
总之啦，方法有多种，实用为上。





