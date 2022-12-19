
## tomcat启动与类加载

顶层元素:Server，Service

连接器元素:Connector(HTTP，AJP 等)

容器元素:Engine，Host，Context

组件元素:Logger，Valve，Realm，Listener，Cluster 等

Pipeline
List<Value> values 阀门

Server(对应jvm虚拟机)

	Service

		Connector：通过socket传输数据，将数据封装成Request对象

			Container（以下都属于容器，继承了Container接口）
				Engine
					Host容器，接收到Connector传输过来的请求对象后不会自己处理，而是交给对应的Host处理
				Host
					Context容器
				Context
					List<Wrapper> wrappers
				Wrapper
					根据servlet类型分类
					List<Servlet> servlets

					StrandardWrapperValue


Bootstrap 完成了两项工作: 创建类加载器和调用 Catalina 的方法。

	是启动类，startup.sh会调用catalina.sh，该脚本中会调用Bootstrap.class的main方法，通过传入的参数进行启动或停止



### 类加载顺序
委托模型
Bootstrap：该加载器用于 JVM 加载核心类，如 java.lang.*，java.io.*
Extension：而 Extension 类加载器加载的是不需要指定环境变量的类，这些类位于:$JAVA_HOME/jre/lib/ext
System：此类加载器用于加载 CLASSPATH 中指定的 JAR 和类，还用于加载入口函数类(仅含有 main()方法的类)，它还是上面没有覆盖到的类的加载器。

### 为什么tomcat要自定义类加载器
程序开发人员和部署人员要决定在哪里放置类和资源文件，以便它们可以被网络程序使用
对于某个网络程序所特有的类和资源，这些未包装的类和资源放置在你的网络程序 档案/WEB-INF/classes 目录下面，或者，包含这些类和资源的 JAR 文件放置在你的 网络程序档案/WEB-INF/lib 目录下面; 对于必须被所有网络程序共享的类和资源，未包装的这些类和资源放置在 $CATALINA_HOME/shared/classes 下面，或者，包含这些类和资源的 JAR 文件放 置在$CATALINA_HOME/shared/lib 下面。

### Servlet

DefaultServlet


### Value

Value可以存在于容器之中(Engin、Host、Context)

AccessLogValve：可以记录客户端访问日志
RemoteAddrValve：可以根据远程客户的 IP 地址决定是否接受客户的请求


### 问题
1. 连接池参数调优
2. springboot如何集成tomcat




参考资料：docs/精通Tomcat：Java Web应用开发、框架分析与组件配置、系统集成与案例实战.pdf
























## Welcome to Apache Tomcat!

### What Is It?

The Apache Tomcat® software is an open source implementation of the Java
Servlet, JavaServer Pages, Java Expression Language and Java WebSocket
technologies. The Java Servlet, JavaServer Pages, Java Expression Language and
Java WebSocket specifications are developed under the
[Java Community Process](https://jcp.org/en/introduction/overview).

The Apache Tomcat software is developed in an open and participatory
environment and released under the
[Apache License version 2](https://www.apache.org/licenses/). The Apache Tomcat
project is intended to be a collaboration of the best-of-breed developers from
around the world. We invite you to participate in this open development
project. To learn more about getting involved,
[click here](https://tomcat.apache.org/getinvolved.html) or keep reading.

Apache Tomcat software powers numerous large-scale, mission-critical web
applications across a diverse range of industries and organizations. Some of
these users and their stories are listed on the
[PoweredBy wiki page](https://cwiki.apache.org/confluence/display/TOMCAT/PoweredBy).

Apache Tomcat, Tomcat, Apache, the Apache feather, and the Apache Tomcat
project logo are trademarks of the Apache Software Foundation.

### Get It

For every major Tomcat version there is one download page containing
links to the latest binary and source code downloads, but also
links for browsing the download directories and archives:
- [Tomcat 11](https://tomcat.apache.org/download-11.cgi)
- [Tomcat 10](https://tomcat.apache.org/download-10.cgi)
- [Tomcat 9](https://tomcat.apache.org/download-90.cgi)
- [Tomcat 8](https://tomcat.apache.org/download-80.cgi)
- [Tomcat 7](https://tomcat.apache.org/download-70.cgi)

To facilitate choosing the right major Tomcat version one, we have provided a
[version overview page](https://tomcat.apache.org/whichversion.html).

### Documentation

The documentation available as of the date of this release is
included in the docs webapp which ships with tomcat. You can access that webapp
by starting tomcat and visiting <http://localhost:8080/docs/> in your browser.
The most up-to-date documentation for each version can be found at:
- [Tomcat 11.0](https://tomcat.apache.org/tomcat-11.0-doc/)
- [Tomcat 10](https://tomcat.apache.org/tomcat-10.1-doc/)
- [Tomcat 9](https://tomcat.apache.org/tomcat-9.0-doc/)
- [Tomcat 8](https://tomcat.apache.org/tomcat-8.5-doc/)

### Installation

Please see [RUNNING.txt](RUNNING.txt) for more info.

### Licensing

Please see [LICENSE](LICENSE) for more info.

### Support and Mailing List Information

* Free community support is available through the
[tomcat-users](https://tomcat.apache.org/lists.html#tomcat-users) email list and
a dedicated [IRC channel](https://tomcat.apache.org/irc.html) (#tomcat on
Freenode).

* If you want freely available support for running Apache Tomcat, please see the
resources page [here](https://tomcat.apache.org/findhelp.html).

* If you want to be informed about new code releases, bug fixes,
security fixes, general news and information about Apache Tomcat, please
subscribe to the
[tomcat-announce](https://tomcat.apache.org/lists.html#tomcat-announce) email
list.

* If you have a concrete bug report for Apache Tomcat, please see the
instructions for reporting a bug
[here](https://tomcat.apache.org/bugreport.html).

### Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for more info.
