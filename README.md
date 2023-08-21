# Studying
## WebSocket实现来单提醒是如何实现的？

:::warning
WbeSocket是一个基于TCP的一种新的**网络协议**（ws协议）（不同于Http协议），是一种**全双工**的通信协议，它即允许浏览器向服务器端推送消息，同时也允许服务器端向浏览器推送消息。浏览器和服务器只需要经历一次握手，就可以创建一个**持久性连接**，并在连接中进行双向数据传输。
:::

> WebSocket和Http有什么不同？

WebSocket是一种全双工的通信方式，它允许两端都可以主动的向对方推送消息，因此Websocket更像是现实生活中打电话的场景，电话接通后，双方都可以听到对方的信息。而Http它是请求响应模式，由客户端发出请求，浏览器回以响应。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1690872227077-38fcaa95-6f59-4304-b42a-e2810bb76ba3.png#averageHue=%234ba4c9&clientId=u9c6b0c4d-01fe-4&from=paste&height=332&id=u0c13b379&originHeight=740&originWidth=486&originalType=binary&ratio=1&rotation=0&showTitle=false&size=143507&status=done&style=none&taskId=u0cb78d78-920a-4132-8982-52ffede4f64&title=&width=218)

> Websocket的应用场景（页面不刷新，但数据可以实时变化）

视频弹幕、网页聊天（通过Websocket把聊天消息推送到页面中显示）、体育实况更新、股票基金报价实时更新
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1690871933655-8ae729f7-b16c-4a8c-a763-752cbab4137a.png#averageHue=%234074e7&clientId=u9c6b0c4d-01fe-4&from=paste&height=531&id=ue3ce7647&originHeight=531&originWidth=1110&originalType=binary&ratio=1&rotation=0&showTitle=false&size=374665&status=done&style=none&taskId=ue754b3e7-ee79-4288-887e-8c47e8fbc78&title=&width=1110)

> WebSocket的原理是什么？

WebSocket握手
客户端向服务器发送建立连接的请求，此时发送的请求信息如下：

```java
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
Sec-WebSocket-Protocol: chat, superchat
Sec-WebSocket-Version: 13
Origin: http://example.com
```

**Upgrade: **在 HTTP 请求中，Upgrade 头部字段通知服务器客户端希望升级到其他协议。它指示服务器在响应中是否支持升级，并将协议更改为请求中指定的协议。
**Connection: Upgrade:** 在 HTTP 请求中，Connection 头部字段指示客户端是否希望与服务器建立持久连接。而当与 Upgrade 头部一同使用时，Connection: Upgrade 表示客户端希望升级到其他协议，并要求服务器在响应中进行协议升级。
在服务器的响应中，如果支持升级到 WebSocket，会包含如下的响应头部：

```java
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
```

这样，客户端和服务器之间的连接就会从普通的 HTTP 连接升级为 WebSocket 连接，后续通信将使用 WebSocket 协议。

> 在WeSocket之前是如何进行实时通信的？

1. **轮询。**客户端定期向服务器发送请求，判断服务器中是否有新的数据可用。
   拿来单提醒这个功能举例，如果不使用WebSocket，就需要客户端向服务端轮询的发起查询请求，判断数据库中是否存在新的还未进行来单提醒订单数据，如果存在的话，则将来单提醒需要的信息返回给前端。
   **缺点：**会在客户端与服务器之间产生大量的请求与响应，导致不必要的网络开销和延迟。
2. **长轮询。**客户端发出请求后，保持连接打开，等待新数据响应后在关闭连接。
   **优缺点：**解决了无效轮询的数量，但仍然需要频繁建立和关闭连接。
3. **Comet。**模拟实时通信，在返回请求后继续保持连接打开。核心思想是保持长连接来实现实时通信，并允许服务器通过流式传输等推送技术来主动向客户端推送消息。
   **缺点： **该方法依然依赖于无状态的HTTP连接，其要求服务器端有特殊的功能(类似于流式传输等推送技术)来临时挂起连接。  

> WebSocket的优势

1. **双向实时通信。**在单个、长时间的连接上进行双向实时通信。在需要快速实时更新的应用程序里，比HTTP更高效。
2. **降低延迟。**数据可用在客户端与服务器之间以比HTTP更低的延迟进行传输。（头部相对较小；在长连接里传输数据，不必在每次建立连接）
3. **更高效的资源利用。**由于连接只建立了一次，因此减少了重复请求和响应的开销

> WebSocket的限制

1. 不提供加密功能。如果传输的数据要保证安全性，需采用像SSL这样的协议
2. 不支持古老浏览器。
3. 保持长连接需要服务器不断维护和处理连接的状态。

> 参考

[一文吃透 WebSocket 原理 刚面试完，趁热赶紧整理 - 掘金](https://juejin.cn/post/7020964728386093093#heading-4)
[10 分钟 理论 + 实操 搞懂 WebSocket_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1ac411c7vr/?spm_id_from=333.337.search-card.all.click&vd_source=028fc5fb3f265ee4a69cb86472cc5bba)

### 实现步骤

1. 使用websocket.html页面作为WebSocket客户端（由客户端向服务端发送握手请求，服务端响应后，二者就建立了持久连接）
2. 导入WebSocket的maven坐标
3. 导入WebSocket服务端组件WebSocketServer（接收客户端发来的请求并处理，类似于Controller），用于和客户端通信
4. 导入配置类WebSocketConfiguration，注册WebSocket的服务端组件
5. 导入定时任务类WebSocketTask，定时向客户端推送数据（用于测试，可有可无）

| 函数/注解                    | 作用                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| new WebSocket(url)           | 向地址为url的服务端建立连接，并返回ws对象，里面提供了连接相关的API |
| @ServerEndpoint("/ws/{sid}") | 将目前的类定义成一个websocket服务器端, 注解的值将被用于监听用户连接的终端访问URL地址,客户端可以通过这个URL来连接到WebSocket服务器端 |
| @OnOpen                      | 连接建立成功调用方法                                         |
| @OnMessage                   | 收到客户端消息后调用方法                                     |

WebSocket组件

```java
package com.sky.websocket;

import org.springframework.stereotype.Component;
import javax.websocket.OnClose;
import javax.websocket.OnMessage;
import javax.websocket.OnOpen;
import javax.websocket.Session;
import javax.websocket.server.PathParam;
import javax.websocket.server.ServerEndpoint;
import java.util.Collection;
import java.util.HashMap;
import java.util.Map;

/**
 * WebSocket服务
 */
@Component
//标识该类为WebSokcet服务器端，监听该URL地址，客户端可通过该URL连接到该服务器端
@ServerEndpoint("/ws/{sid}")
public class WebSocketServer {

    //存放会话对象
    //一个Session就是一个会话，当客户端与服务端建立连接后，就会生成一个session会话
    private static Map<String, Session> sessionMap = new HashMap();

    /**
     * 连接建立成功调用的方法
     * sid为客户端的标识，连接建立成功则把该会话存入到map中
     */
    @OnOpen
    public void onOpen(Session session, @PathParam("sid") String sid) {
        System.out.println("客户端：" + sid + "建立连接");
        sessionMap.put(sid, session);
    }

    /**
     * 收到客户端消息后调用的方法
     *
     * @param message 客户端发送过来的消息
     */
    @OnMessage
    public void onMessage(String message, @PathParam("sid") String sid) {
        System.out.println("收到来自客户端：" + sid + "的信息:" + message);
    }

    /**
     * 连接关闭调用的方法
     *
     * @param sid
     */
    @OnClose
    public void onClose(@PathParam("sid") String sid) {
        System.out.println("连接断开:" + sid);
        sessionMap.remove(sid);
    }

    /**
     * 群发
     *
     * @param message
     */
    public void sendToAllClient(String message) {
        Collection<Session> sessions = sessionMap.values();
        for (Session session : sessions) {
            try {
                //服务器向客户端发送消息
                session.getBasicRemote().sendText(message);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }

}
```

定义配置类，注册WebSocket的服务端组件

```java
package com.sky.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.socket.server.standard.ServerEndpointExporter;

/**
 * WebSocket配置类，用于注册WebSocket的Bean
 */
@Configuration
public class WebSocketConfiguration {
    @Bean
    public ServerEndpointExporter serverEndpointExporter() {
        return new ServerEndpointExporter();
    }

}
```

### 
