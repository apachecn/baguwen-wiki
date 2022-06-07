<!--yml
category: Shiro
date: 0001-01-01 00:00:00
-->

# Shiro 面试题（爪哇程序员）

# 什么是shiro

> 原文：[https://zwmst.com/1406.html](https://zwmst.com/1406.html)

Shiro是一个强大易用的java安全框架，提供了认证、授权、加密、会话管理、与web集成、 缓存等功能，对于任何一个应用程序，都可以提供全面的安全服务，相比其他安全框架，shiro要简单的多。


# 解释下Shiro的核心概念：Subject、SecurityManager、Realm

> 原文：[https://zwmst.com/1408.html](https://zwmst.com/1408.html)

Subject：主体，代表了当前“用户”，这个用户不一定是一个具体的人，与当前应用交互的任 何东西都是Subject，如爬虫、机器人等；即一个抽象概念；所有Subject都绑定到 SecurityManager，与Subject的所有交互都会委托给SecurityManager；可以把Subject认为是一个门面；SecurityManager才是实际的执行者。

SecurityManager：安全管理器；即所有与安全有关的操作都会与SecurityManager交互；且它管理着所有Subject；可以看出它是shiro的核心, SecurityManager相当于spring mvc中 的dispatcherServlet前端控制器。

Realm：域，shiro从Realm获取安全数据(如用户、角色、权限)，就是说SecurityManager 要验证用户身份，那么它需要从Realm获取相应的用户进行比较以确定用户身份是否合法；也 需要从Realm得到用户相应的角色/权限进行验证用户是否能进行操作；可以把Realm看成 DataSource，即安全数据源。


# Shiro的优点

> 原文：[https://zwmst.com/1410.html](https://zwmst.com/1410.html)

1、 简单的身份验证，支持多种数据源

2、对角色的简单授权，支持细粒度的授权（方法）

3、支持一级缓存，以提升应用程序的性能

4、内置基于POJO的企业会话管理，适用于web及非web环境

5、非常简单的API加密

6、不跟任何框架绑定，可以独立运行


# Shiro有哪些组件？

> 原文：[https://zwmst.com/1412.html](https://zwmst.com/1412.html)

Authentication：身份认证/登录，验证用户是不是拥有相应的身份；

Authorization：授权，即权限验证，验证某个已认证的用户是否拥有某个权限；即判断用户 是否能做事情，常见的如：验证某个用户是否拥有某个角色。或者细粒度的验证某个用户对某 个资源是否具有某个权限；

Session Manager：会话管理，即用户登录后就是一次会话，在没有退出之前，它的所有信息 都在会话中；会话可以是普通JavaSE环境的，也可以是如Web环境的；

Cryptography：加密，保护数据的安全性，如密码加密存储到数据库，而不是明文存储；

Web Support：Web支持，可以非常容易的集成到Web环境；

Caching：缓存，比如用户登录后，其用户信息、拥有的角色/权限不必每次去查，这样可以提 高效率；

Concurrency：shiro支持多线程应用的并发验证，即如在一个线程中开启另一个线程，能把 权限自动传播过去；

Testing：提供测试支持；

Run As：允许一个用户假装为另一个用户（如果他们允许）的身份进行访问；

Remember Me：记住我，这个是非常常见的功能，即一次登录后，下次再来的话不用登录 了。

记住一点，Shiro不会去维护用户、维护权限；这些需要我们自己去设计/提供；然后通过相应 的接口注入给Shiro即可。


# 说下Authentication 身份验证的流程

> 原文：[https://zwmst.com/1414.html](https://zwmst.com/1414.html)

principals：身份，即主体的标识属性，可以是任何东西，如用户名、邮箱等，唯一即可。

credentials：证明/凭证，即只有主体知道的安全值，如密码/数字证书等。

身份认证流程：

1）首先调用Subject.login(token)进行登录，其会自动委托给SecurityManager，调用之前 必须通过SecurityUtils.setSecurityManager()设置；

2）SecurityManager负责真正的身份验证逻辑；它会委托给Authenticator进行身份验证；

3）Authenticator才是真正的身份验证者，shiro api中核心的身份认证入口点，此处可以自 定义插入自己的实现；

4）Authenticator可能会委托给相应的AuthenticationStrategy进行多Realm身份验证，默 认ModularRealmAuthenticator会调用AuthenticationStrategy进行多Realm身份验证；

5）Authenticator会把相应的token传入Realm，从Realm获取身份验证信息，如果没有返 回/抛出异常表示身份验证失败了。此处可以配置多个Realm，将按照相应的顺序及策略进行 访问。

6）Authenticator的职责是验证用户账号，是shiro api中身份验证核心的入口点。

7）AuthenticationStrategy 认证策略 ModularRealmAuthenticator默认使用 AtLeastOneSuccessfulStrategy策略

1> FirstSuccessfulStrategy：只要有一个Realm验证成功即可，只返回第一个Realm身份验 证成功的认证信息，其他的忽略；

2> AtLeastOneSuccessfulStrategy：只要有一个Realm验证成功即可，和 FirstSuccessfulStrategy不同，返回所有Realm身份验证成功的认证信息；

3> AllSuccessfulStrategy：所有Realm验证成功才算成功，且返回所有Realm身份验证成功 的认证信息，如果有一个失败就失败了。


# Authorization 授权的方式和流程是怎样的？

> 原文：[https://zwmst.com/1416.html](https://zwmst.com/1416.html)

principals：身份，即主体的标识属性，可以是任何东西，如用户名、邮箱等，唯一即可。

credentials：证明/凭证，即只有主体知道的安全值，如密码/数字证书等。

身份认证流程：

1）首先调用Subject.login(token)进行登录，其会自动委托给SecurityManager，调用之前 必须通过SecurityUtils.setSecurityManager()设置；

2）SecurityManager负责真正的身份验证逻辑；它会委托给Authenticator进行身份验证；

3）Authenticator才是真正的身份验证者，shiro api中核心的身份认证入口点，此处可以自 定义插入自己的实现；

4）Authenticator可能会委托给相应的AuthenticationStrategy进行多Realm身份验证，默 认ModularRealmAuthenticator会调用AuthenticationStrategy进行多Realm身份验证；

5）Authenticator会把相应的token传入Realm，从Realm获取身份验证信息，如果没有返 回/抛出异常表示身份验证失败了。此处可以配置多个Realm，将按照相应的顺序及策略进行 访问。

6）Authenticator的职责是验证用户账号，是shiro api中身份验证核心的入口点。

7）AuthenticationStrategy 认证策略 ModularRealmAuthenticator默认使用 AtLeastOneSuccessfulStrategy策略

1> FirstSuccessfulStrategy：只要有一个Realm验证成功即可，只返回第一个Realm身份验 证成功的认证信息，其他的忽略；

2> AtLeastOneSuccessfulStrategy：只要有一个Realm验证成功即可，和 FirstSuccessfulStrategy不同，返回所有Realm身份验证成功的认证信息；

3> AllSuccessfulStrategy：所有Realm验证成功才算成功，且返回所有Realm身份验证成功 的认证信息，如果有一个失败就失败了。


# Cryptography 加密的过程是这样的？

> 原文：[https://zwmst.com/1418.html](https://zwmst.com/1418.html)

编码/解码

Shiro提供了base64和16进制字符串编码/解码的API支持,方便一些编码解码操作 Base64.encodeToString(str.getBytes())编码

Base64.decodeToString(base64Encoded) 解码

散列算法

常见散列算法如MD5,SHA等

1）首先创建一个DfaultHashService,默认使用SHA-512算法；

2）可以通过hashAlgorithmName属性修改算法；

3）可以通过privateSalt设置一个私盐，其在散列时自动与用户传入的公盐混合产生一个新 盐；

4）可以通过generatePublicSalt属性在用户没有传入公盐的情况下是否生成公盐；

5）可以设置randomNumberGenerator用于生成公盐；

6）可以设置hashIterations属性来修改默认加密迭代次数；

7）需要构建一个HashRequest,传入算法、数据、公盐、迭代次数。

生成随机数

SecureRandomNumberGenerator randomNumberGenerator = new SecureRandomNumberGenerator();

randomNumberGenerator.setSeed(“159”.getBytes());

String hex = randomNumberGenerator.nextBytes().toHex();

加密/解密

提供对称式加密/解密算法的支持，如AES、Blowfish等

PasswordService/CredentialsMatcher

用于提供加密密码及验证密码服务

Shiro默认提供了PasswordService实现DefaultPasswordService;CredentialsMatcher实

现PasswordMatcher及HashedCredentialsMatcher(更强大)

HashedCredentialsMatcher实现密码验证服务

Shiro提供了CredentialsMatcher的散列实现HashedCredentialsMatcher,和

PasswordMatcher不同的是，它只是用于密码验证，且可以提供自己的盐，而不是随机生成 盐，且生成密码散列值的算法需要自己写，因为能提供自己的盐


# Realm 域如何使用？

> 原文：[https://zwmst.com/1420.html](https://zwmst.com/1420.html)

定义Realm（自定义Realm继承AuthorizingRealm即可）

1）UserRealm父类AuthorizingRealm将获取Subject相关信息分成两步：获取身份验证信息 （doGetAuthenticationInfo）及授权信息（doGetAuthorizationInfo）

2）doGetAuthenticationInfo获取身份验证相关信息：首先根据传入的用户名获取User信息；如果user为空，那么抛出没找到账号异常UnknownAccountExecption；如果user找到 但却被锁定了抛出锁定异常LockedAccountException；最后生成AuthenticationInfo信息，交给间接父类AuthenticatingRealm使用CredentialsMatcher进行判断密码是否匹配， 如果不匹配将抛出密码错误异常信息IncorrectCredentialsException；如果密码重试次数太 多将抛出超出重试次数异常ExcessiveAttemptsException；在组装SimpleAuthenticationInfo信息时，需要传入：身份信息（用户名）、凭据（密文密码）、 盐（username+salt），CredentialsMatcher使用盐加密传入的明文密码和此处的密文密码 进行匹配。

3）doGetAuthorizationInfo获取授权信息：PrincipalCollection是一个身份集合，因为只用到了一个Realm，所以直接调用getPrimaryPrincipal得到之前传入的用户名即可；然后根 据用户名调用UserService接口获取角色及权限信息。

AuthenticationInfo的两个作用

1）如果Realm是AuthenticatingRealm子类，则提供给AuthenticatingRealm内部使用的 CredentialsMatcher进行凭据验证；（如果没有继承它需要在自己的Realm中实现验证）；

2）提供给SecurityManager来创建Subject（提供身份信息）；


# shiro拦截器的执行流程

> 原文：[https://zwmst.com/1422.html](https://zwmst.com/1422.html)

**基于表单登录拦截器

onPreHandle主要流程：

1）首先判断是否已经登录过了，如果已经登录过了继续拦截器链即可；

2）如果没有登录，看看是否是登录请求，如果是get方法的登录页面请求，则继续拦截器链（到请求页面），否则如果是get方法的其他页面请求则保存当前请求并重定向到登录页面；

3）如果是post方法的登录页面表单提交请求，则收集用户名/密码登录即可，如果失败了保存 错误消息到“shiroLoginFailure”并返回到登录页面；

4）如果登录成功了，且之前有保存的请求，则重定向到之前的这个请求，否则到默认的成功 页面。

任意角色授权拦截器

流程：

1）首先判断用户有没有任意角色，如果没有返回false，将到onAccessDenied进行处理；

2）如果用户没有角色，接着判断用户有没有登录，如果没有登录先重定向到登录；

3）如果用户没有角色且设置了未授权页面（unauthorizedUrl），那么重定向到未授权页面；否则直接返回401未授权错误码。

默认拦截器

**身份验证相关的

authc 基于表单的拦截器，即验证成功之后才能访问 /=authc authcBasic Basic HTTP身份验证拦截器，主要属性：applicationName logout 退出 /logout=logout

user 用户拦截器 /=user

anon 匿名拦截器，一般用于静态资源过滤 /static/=anon

**授权相关的

roles 角色授权拦截器，主要属性：loginUrl，unauthorizedUrl /admin/=roles[admin] perms 权限授权拦截器 /user/=perms[“user:create”]

port 端口拦截器，主要属性: port(80) /test=port[80]

rest rest风格拦截器 /users=rest[user]，会自动拼接出

“user:read,user:create,user:update,user:delete”

ssl ssl拦截器，只有请求协议是https才能通过


# Session Manager 会话管理介绍一下

> 原文：[https://zwmst.com/1424.html](https://zwmst.com/1424.html)

*   Session

所谓session，即用户访问应用时保持的连接关系，在多次交互中应用能够识别出当前访问的 用户是谁，且可以在多次交互中保存一些数据。

Subject subject = SecurityUtils.getSubject();

Session session = subject.getSession();

session.getId(); // 获取当前session的唯一标识

session.getHost(); // 获取当前Subject的主机地址，该地址是通过

HostAuthenticationToken.getHost()提供的

session.getTimeOut(); // 获取超时时间

session.setTimeOut(); // 设置超时时间（不设置默认是全局过期时间）

session.touch(); // 更新最后访问时间

session.stop(); // 销毁session，当Subject.logout()时会自动调用stop方法来销毁会话。如 果在web中，调用javax.servlet.http.HttpSession.invalidate()也会自动调用shiro

session.top方法进行销毁shiro的会话

session.setAttribute(“key”,”123”); // 设置session属性

session.getAttribute(“key”); // 获取session属性

session.removeAttribute(“key”); // 删除属性

注：Shiro提供的会话可以用于javaSE/javaEE环境，不依赖于任何底层容器，可以独立使 用，是完整的会话模块。

*   Session manager 会话管理器

会话管理器管理着应用中所有Subject的会话的创建、维护、删除、失效、验证等工作。是

Shiro的核心组件，顶层组件SecurityManager直接继承了SessionManager，且提供了

SessionSecurityManager实现直接把会话管理委托给相应的SessionManager、

DefaultSecurityManager及DefaultWebSecurityManager 默认SecurityManager都继承 了SessionSecurityManager。

*   Shiro提供了三个默认实现：

DefaultSessionManager：DefaultSecurityManager使用的默认实现，用于JavaSE环境；

ServletContainerSessionManager: DefaultWebSecurityManager使用的默认实现，用于 Web环境，其直接使用Servlet容器的会话；

DefaultWebSessionManager：用于Web环境的实现，可以替代 ServletContainerSessionManager，自己维护着会话，直接废弃了Servlet容器的会话管 理。