---
keyword: [WebSocket协议, WebSocket多活, WebSocket协议集群]
---

# WebSocket多活实践

WebSocket是一种新的HTML5协议，它实现了浏览器与服务器全双工通信，能更好地节省服务器资源和带宽并达到实时通讯。本文介绍如何在命名空间接入WebSocket协议集群，目前WebSocket仅支持异地多活。

-   已开通、购买并创建ECS，更多信息，请参见[ECS入门概述](/cn.zh-CN/快速入门/ECS入门概述.md)。
-   已开通、购买并创建SLB，更多信息，请参见[SLB入门概述](/cn.zh-CN/传统型负载均衡CLB/CLB快速入门/入门概述.md)。
-   已创建命名空间，更多信息， 请参见[新建命名空间](/cn.zh-CN/多活容灾/用户指南/异地双活配置/新建命名空间.md)。

## 步骤一：创建WebSocket协议集群

1.  登录[MSHA控制台](https://msha.console.aliyun.com)。

2.  在左侧导航栏选择**后台管理** \> **接入层集群**。

3.  在接入层集群管控页面，单击要创建的单元页签，然后单击页面右上角的**创建集群**。

4.  在新建集群对话框中，选择创建好的ECS实例，**协议**选择**websocket**，设置**集群名称**，然后单击**确定**。

    ![websocket1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9657094061/p180122.png)

5.  在左侧导航栏选择**后台管理** \> **网络SLB**。

6.  在网络SLB列表页面，单击要创建的单元页签，然后单击右上角的**同步SLB**。

7.  在同步SLB的对话框中，选择要新增的SLB，然后单击**确定**。

8.  完成本单元的接入层集群创建后，继续重复步骤[2](#step_4xq_xnl_nzq)至步骤[7](#step_n3w_h9d_vkb)的操作，在另一单元创建接入层集群，完成两个单元的WebSocket接入层集群创建。


## 步骤二：WebSocket协议集群加入接入层集群

1.  在左侧导航栏选择**配置** \> **全局配置概览**，在已创建好的命名空间中单击**继续配置**。

2.  单击**下一步**，进入添加单元页面。

3.  分别单击不同单元下的**+修改**，在修改单元面板中的**接入层集群**，分别选择创建好的WebSocket协议集群，然后单击**确定**。

    WebSocket协议集群加入接入层集群后，您可以在左侧导航栏选择**配置** \> **接入层配置**，在接入层配置页面即可看见这两个集群。

    ![websocket2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0757094061/p180150.png)


## 步骤三：创建WebSocket协议域名

1.  在左侧导航栏选择**配置** \> **接入层配置**，单击**新增域名**。

2.  在设置域名详情面板，设置域名的各个参数，然后单击**确定**。

    ![Websocket3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0757094061/p180154.png)

    |参数|说明|示例|
    |--|--|--|
    |**接入类型**|WebSocket协议的接入类型目前仅支持**域名**。|域名|
    |**域名**|编辑**域名**。填写域名后，单元子域名区域将按照之前定义的单元，自动生成每个单元下的子域名。|websocket.msha.tech|
    |**域名解析类型**|设置域名解析类型：    -   **DNS解析**：阿里云DNS请选择DNS解析。
    -   **全局流量管理**：管理全局流量。
    -   **不解析**：如果不是阿里云DNS，是其它供应商，域名解析类型请选择不解析。
|DNS解析|
    |**多单元解析**|是否进行多单元解析。|是|
    |**单元子域名**|填写**域名**后，单元子域名区域将按照之前定义的单元，自动生成每个单元下的子域名。|    -   center.websocket.msha.tech
    -   unbj.websocket.msha.tech |
    |**纠错类型**|WebSocket协议的纠结类型目前仅支持**重定向**。|重定向|
    |**协议**|选择**websocket**。|websocket|
    |**生效集群**|分别选择不同单元对应的WebSocket协议集群。|    -   杭州中心：ws-hz-2
    -   北京单元：ws-bj-2 |

3.  在接入层配置页面，单击新增WebSocket域名**配置**列的**URI**。

    ![URI](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9682194061/p180169.png)

4.  在配置URI的面板中，单击**添加**，按需配置URI的信息，然后单击**确定**。

    **说明：** 回源应用信息的输入格式为IP:PORT，多个回源应用用英文逗号相隔。

    ![websocket-URI1.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8682194061/p180173.png)

5.  单击WebSocket域名**配置**列的**生效**，然后单击**确认**。WebSocket协议域名创建完成。

    ![生效](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8682194061/p180168.png)


## 验证WebSocket多活

上述**URI**配置的**回源应用ip:port**是两个单元各自的WebSocket Server的地址。在本示例中，WebSocket Server主要业务逻辑就是定时的向所有Client广播消息，表明自己所在单元。

您可以重点关注Client，以下示例采用NodeJS的WebSocket Library：

```
const WebSocket = require('ws');

let host = "http://websocket.msha.tech/";

let routerId = 1111;
// routerId = 6249;
routerId = 8330;

let options = {
    'headers': {
        routerId: routerId,
        unitType: "unit_type",
    }
};

let ws = handleWs();

function handleWs(){
    let ws = new WebSocket(host,[],options);
    ws.on('upgrade', function open(resp) {
        // console.log('upgrade ',resp);
    });

    ws.on('open', function open() {
        console.log('connected:'+routerId);
        ws.send(Date.now());
    });

    ws.on('error', function error(e) {
        console.log('err',e);
    });

    ws.on('close', function close() {
        console.log('disconnected');
    //断连后重连。
        let retryTime = 1500;
        setTimeout(()=>{
            console.log('!!! reconnecting in ...'+retryTime+' ms');
            ws = handleWs();
        }, retryTime);
    });

    ws.on('message', function incoming(data) {
        console.log(`msg: ${data} `);
    });

    ws.on('unexpected-response', function handleerr(req,resp) {
        //处理重定向。
    if ((resp.statusCode+'').startsWith("30")){
            console.log("!!! redirecting... from ", host," to",resp.headers.location);
            host = resp.headers.location;
            ws = handleWs();
        }

    });
    return ws;
}
```

**单元分流**

1.  在左侧导航栏选择**异地切流列表**，然后单击页面右上角的**切流**。

2.  在切流详情页面，查看当前流量规则，如下图所示。

    当前流量规则为当流量的routerId是0~5997，则访问杭州中心单元；当流量的routerId是5998~9999，则访问北京单元。

    ![单元分流.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9682194061/p180184.png)

3.  将上述示例中两个Client的routerId分别设置为1111和8330。

    ```
    let routerId = 1111;
    routerId = 8330;
    ```

    单元切流结果分别如下：

    ```
    // 1111
    !!! redirecting... from  http://websocket.msha.tech/  to http://center.websocket.msha.tech/
    connected:1111
    msg: Welcome to the server!hangzhou 
    msg: hangzhou new connection: / 
    msg: 1604389722277:hangzhou 
    msg: 0.132955630917172:hangzhou 
    msg: 0.8012559750359831:hangzhou 
    
    // 8330
    connected:8330
    msg: Welcome to the server!beijing 
    msg: beijing new connection: / 
    msg: 1604389731323:beijing 
    msg: 0.4186786493131692:beijing 
    msg: 0.897348812107992:beijing 
    msg: 0.5328893935466773:beijing 
    ```

    从以上结果可以看出：1111访问的时候，`websocket.msha.tech`的cname `unbj.websocket.msha.tech`生效了，于是被重定向到了相应的单元`center.websocket.msha.tech`。而8330访问的时候`unbj.websocket.msha.tech`是正确的单元，所以直接返回正确结果。


**切流**

1.  将三个Client的routerId分别设置为1111、6249和8330，同时发起WebSocket连接。

    ```
    let routerId = 1111;
    routerId = 6249;
    routerId = 8330;
    ```

2.  在MSHA控制台左侧导航栏选择**异地切流列表**，然后单击右上角的**切流**。

3.  在切流详情页面，调整切流规则。杭州中心routerId规则修改为0~6380，则北京单元的routerId规则为6381~9999。

4.  单击**生成预览**，查看切流规则。

5.  单击**规则文本**，即可对比查看切流规则前后变更详情。确认后单击**执行预检查**。

6.  在切流检查区域查看切流检查，待所有检查项均通过后，单击**确认**。

    **说明：** 若有检查项检查不通过，可在该检查项右侧单击重试或跳过。跳过功能一般用于紧急切流场景，请谨慎使用。

7.  单击**确认**，开始切流。

    ![切流.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1813894061/p180281.png)

    切流后，Client的结果如下。

    ```
    !!! redirecting... from  http://websocket.msha.tech/  to http://center.websocket.msha.tech/
    connected:1111
    msg: Welcome to the server!hangzhou 
    msg: 1604390454108:hangzhou 
    msg: 0.38414805855739653:hangzhou 
    msg: 0.13875630357195323:hangzhou 
    msg: 0.6229300725811783:hangzhou 
    msg: 0.11019882091734623:hangzhou 
    msg: 0.7957423074512242:hangzhou 
    msg: 0.4736047658982191:hangzhou 
    msg: 0.5014541304674829:hangzhou 
    msg: 0.614086617348312:hangzhou 
    msg: 0.1484071030030174:hangzhou 
    msg: 0.6652626409517592:hangzhou 
    msg: 0.40154994570197045:hangzhou 
    msg: 0.8643718167863417:hangzhou 
    msg: 0.28831735861784147:hangzhou 
    msg: 0.6652626409517592:hangzhou 
    msg: 0.40154994570197045:hangzhou 
    msg: 0.8643718167863417:hangzhou 
    msg: 0.28831735861784147:hangzhou 
    
    
    connected:6249
    msg: Welcome to the server!beijing 
    msg: 1604390457853:beijing 
    msg: 0.9493741235546642:beijing 
    msg: 0.09769747028250086:beijing 
    msg: 0.5870071708377984:beijing 
    msg: 0.7842176937040484:beijing 
    msg: 0.6607537308351272:beijing 
    msg: 0.6775899565019491:beijing 
    msg: 0.9098061272236709:beijing 
    msg: 0.05783338659476467:beijing 
    msg: 0.8919011012317618:beijing 
    msg: 0.12108282852472352:beijing 
    disconnected
    !!! reconnecting in ...1500 ms
    !!! redirecting... from  http://websocket.msha.tech/  to http://center.websocket.msha.tech/
    connected:6249
    msg: Welcome to the server!hangzhou 
    msg: 1604390479646:hangzhou 
    msg: 0.8032432387270054:hangzhou 
    msg: 0.8504693718670565:hangzhou 
    msg: 0.5079091770595435:hangzhou 
    msg: 0.7248089009268245:hangzhou 
    msg: 0.3223790249502595:hangzhou 
    msg: 0.9069452763009609:hangzhou 
    msg: 0.4537487716609916:hangzhou 
    msg: 0.5672352139323884:hangzhou 
    msg: 0.9136309927556057:hangzhou 
    
    
    connected:8330
    msg: Welcome to the server!beijing 
    msg: 1604390461787:beijing 
    msg: 0.5870071708377984:beijing 
    msg: 0.7842176937040484:beijing 
    msg: 0.6607537308351272:beijing 
    msg: 0.6775899565019491:beijing 
    msg: 0.9098061272236709:beijing 
    msg: 0.05783338659476467:beijing 
    msg: 0.8919011012317618:beijing 
    msg: 0.12108282852472352:beijing 
    msg: 0.7753852558635438:beijing 
    msg: 0.03463907943252087:beijing 
    msg: 0.17068444692028695:beijing 
    msg: 0.723355026768321:beijing 
    msg: 0.4414733762619504:beijing 
    msg: 0.27475324832571923:beijing 
    msg: 0.9036020463889554:beijing 
    msg: 0.9359826074623169:beijing 
    msg: 0.7434708713278148:beijing 
    msg: 0.6591996455893424:beijing 
    ```

    从以上结果可以看出，只有处于变更范围内的routerId 6249访问被切断了连接并重定向了正确的单元，其余两个routerId的访问都一直与正确的单元保持着连接和通信，不受切流影响。


