com-bilein-filter.jar
微认证登录调用流程说明
集成网页端微认证登录步骤如下:
1、请先确认sis_labor.properties配置文件是否已配置完成。
2、在web.xml中配置过滤器，拦截登录路径，并且将拦截登录路径的过滤器映射至LoginFilter.java中。
3、在web.xml中配置过滤器，拦截回调处理路径，并且将回调处理路径的过滤器映射至CallbackFilter.java中。
4、在请求头中获取到回调处理得到的学工号，进行登录。

### 网页端微认证登录代码结构 ###
    |-- com.bilein.filter
    |   |-- LoginFilter.java     ## 登陆拦截过滤器 ##
            方法:doFilter()      过滤登录地址，处理请求
                 1.读取配置文件，依赖Sis.java
                 2.在消息头和Session里面获取学工号
                 3.没有获取到，组装参数，
                   读取signin.httl页面，生成二维码页面，并响应
                 4.如果获取到将学工号（uniqueNo）存放至消息头，
                   转发至成功登录地址，
                   依赖ModifyHttpServletRequestWrapper.java

    |   |-- CallbackFilter.java  ## 回调处理过滤器 ##
            方法:doFilter()      过滤回调地址，处理请求
                 1.获取相应参数，进行校验，
                 2.获取校验结果，依赖ExcuteUtil,java
                 3.在结果中获取学工号失败，重新生成二维码进行登录
                 4.获取学工号成功，存放在session和请求头
                 5.转发至成功登录地址

    |   |-- SigninUtil.java      ## 网页端登录工具类 ##
            方法:signin()               封装参数，并返回参数集合
            方法:getString(页面路径)   根据传给的路径读取文件为字符串

    |   |-- signin.httl          ## 二维码生成页面 ##

    |-- system.lib  依赖类库
    |   |-- Sis.java
            方法:getInstance(文件名)   读取配置文件，初始化类属性
            方法:get(属性名)           获取文件的属性值

    |-- utils.handle 依赖类库
    |   |-- ModifyHttpServletRequestWrapper.java  向请求头添加数据            方法:putHeader(参数名，参数值); 在请求头添加数据

    |-- eu.jar
    |   |-- com.bilein.handle
    |       |-- ExcuteUtil.java
                方法：checkClientAuth(); 校验身份，并获取学工号

    |-- resources(项目的根目录)
        |-- sis_labor.properties  配置文件
	        `-- urlHead           微认证地址
            `-- appid             应用标识
            `-- tokenKey          令牌
            `-- aeskey    	      公钥
            `-- clienthost        本项目地址
	        `-- signinurl         网页端需要拦截的登录地址
	        `-- signinSuccess     网页端登录成功地址
	        `-- callback          网页端认证回调地址
            `-- title             生成的二维码页面标题


集成微信端微认证登录步骤如下:
1、请先确认sis_labor.properties配置文件是否已配置完成。
2、在web.xml中配置过滤器，拦截微信端登录路径，并且将拦截登录路径的过滤器映射至WCLoginFilter.java中。
3、在web.xml中配置过滤器，拦截回调处理路径，并且将回调处理路径的过滤器映射至WCCallbackFilter.java中。
4、在请求头中获取到回调处理得到的学工号（uniqueNo），进行登录。


### 微信端微认证登录代码结构 ###
    |-- com.bilein.filter
    |   |-- WCLoginFilter.java     ## 登陆拦截过滤器 ##
            方法:doFilter()      过滤登录地址，处理请求
                  1.获取相应参数，进行校验，
                 2.获取校验结果，依赖ExcuteUtil,java
                 3.在结果中获取学工号失败，重新生成二维码进行登录
                 4.获取学工号成功（uniqueNo），
                   存放在session和请求头，并转发至成功登录地址

    |   |-- WCCallbackFilter.java  ## 回调处理过滤器 ##
            方法:doFilter()      过滤回调地址，处理请求
                 1.获取相应参数，进行校验，获取校验结果
                 2.在结果中获取学工号失败，响应错误提示
                 3.获取学工号成功（uniqueNo），
存放在session和请求头，并转发至成功登录地址

    |   |-- WCSigninUtil.java      ## 网页端登录工具类 ##
            方法:generateUrl()      生成url重定向发送请求

    |-- system.lib  依赖类库
    |   |-- Sis.java
            方法:getInstance(文件名)   读取配置文件，初始化类属性
            方法:get(属性名)           获取文件的属性值

    |-- utils.handle  依赖类库
    |   |-- ModifyHttpServletRequestWrapper.java 向请求头添加数据
方法:putHeader(参数名，参数值); 在请求头添加数据

    |-- eu.jar   依赖类库
    |   |-- com.bilein.handle
    |       |-- ExcuteUtil.java
                方法：generateAuthUrl(); 组装参数生成url

    |-- resources(项目的根目录)
        |-- sis_labor.properties  配置文件，调用方法之前请确认配置正确
	        `-- urlHead           微认证地址
            `-- appid             应用标识
            `-- tokenKey          令牌
            `-- aeskey    	      公钥
            `-- clienthost        本项目地址
            `-- wccallback    	  微信端登录时回调地址
	        `-- wcsuccessurl      微信端验证成功跳转地址



