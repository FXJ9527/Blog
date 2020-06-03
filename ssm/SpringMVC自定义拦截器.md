web.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="3.0" xmlns="http://java.sun.com/xml/ns/javaee"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee                       
	http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd">
	<!-- 配置前端控制器 -->
	<servlet>
		<servlet-name>jqk</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>classpath:springmvc.xml</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
	<servlet-mapping>
		<servlet-name>jqk</servlet-name>
		<url-pattern>/</url-pattern>
	</servlet-mapping>
	
	<!-- 字符编码过滤器 -->
	<filter>
		<filter-name>encoding</filter-name>
		<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
		<init-param>
			<param-name>encoding</param-name>
			<param-value>utf-8</param-value>
		</init-param>
	</filter>
	<filter-mapping>
		<filter-name>encoding</filter-name>
		<url-pattern>/*</url-pattern>
	</filter-mapping>
</web-app>
```

springmvc.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd">
    <!-- 扫描注解 -->
	<context:component-scan base-package="com.bjsxt.controller"></context:component-scan>
	<!-- 注解驱动 -->
	<!-- org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping -->
	<!-- org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter -->
	<mvc:annotation-driven></mvc:annotation-driven>
	<!-- 静态资源 -->
	<mvc:resources location="/js/" mapping="/js/**"></mvc:resources>
	<mvc:resources location="/css/" mapping="/css/**"></mvc:resources>
	<mvc:resources location="/images/" mapping="/images/**"></mvc:resources>
	<mvc:resources location="/files/" mapping="/files/**"></mvc:resources>
	<!-- 拦截器 -->
	<mvc:interceptors>
		<mvc:interceptor>
			<mvc:mapping path="/demo"/>
			<mvc:mapping path="/demo1"/>
			<mvc:mapping path="/demo2"/>
			<bean class="com.bjsxt.interceptor.DemoInterceptor"></bean>
		</mvc:interceptor>
	</mvc:interceptors>
</beans>
```

自定义拦截器类继承HandleInteceptor
```
package com.bjsxt.interceptor;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

public class DemoInterceptor implements HandlerInterceptor {
	//在进入控制器之前执行
	//如果返回值为false,阻止进入控制器
	//控制代码
	@Override
	public boolean preHandle(HttpServletRequest arg0, HttpServletResponse arg1, Object arg2) throws Exception {
		System.out.println("arg2:"+arg2);
		System.out.println("preHandle");
		return true;
	}
	//控制器执行完成,进入到jsp之前执行.
	//日志记录.
	//敏感词语过滤
	@Override
	public void postHandle(HttpServletRequest arg0, HttpServletResponse arg1, Object arg2, ModelAndView arg3)
			throws Exception {
		
		System.out.println("往"+arg3.getViewName()+"跳转");
		System.out.println("model的值"+arg3.getModel().get("model"));
		String word = arg3.getModel().get("model").toString();
		String newWord = word.replace("祖国", "**");
		arg3.getModel().put("model", newWord);
//		arg3.getModel().put("model", "修改后的内容");
		System.out.println("postHandle");
	}
	//jsp执行完成后执行
	//记录执行过程中出现的异常.
	//可以把异常记录到日志中
	@Override
	public void afterCompletion(HttpServletRequest arg0, HttpServletResponse arg1, Object arg2, Exception arg3)
			throws Exception {
		System.out.println("arg3:"+arg3);
		System.out.println("afterCompletion"+arg3.getMessage());
	}
}

```

