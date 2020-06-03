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

	<!-- 视图解析器 -->
	<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    	<property name="prefix" value="/"></property>
    	<property name="suffix" value=".jsp"></property>
    </bean>
</beans>
```
