# 数据查询服务

## Overview

`GuiQueryServer`的功能是为前端界面/插件提供数据查询服务:

- <format style="bold" color="Red">本服务限定为查询服务，不允许涉及增删改</format>。原因是为了调高查询的速度，本服务采用了多线程的方式来处理请求，而增删改请求原则上只能串行处理。
- 本服务定位为前端界面/插件提供查询服务，当然后台服务也不是不能调用，但如果是scada自身的后台服务，直接调用api接口会更快更方便；

## 设计架构

与其他服务类似，数据查询服务也采用以下设计原则：

- api提供具体功能，即包括以下内容：
    - 提供查询报文、回复报文的结构体定义；
    - 提供获取查询报文、回复报文的报文id接口；
    - 提供查询报文处理回调函数、回复报文处理回调函数的定义；
    - 提供查询报文、回复报文的订阅接口；
    - 提供查询报文、回复报文的取消订阅接口；
    - 提供查询报文、回复报文的发送接口；
    - 提供入参为查询报文、出参为回复报文的本地查询接口；
    - 提供入参为查询报文、出参为回复报文的远程查询接口;
- server端订阅查询报文，收到client发送的查询报文后调用本地查询接口获取对应的回复报文，再调用发送接口将其回给对应的client；
- client端有两种处理方式(同步/异步)，视情况选择合适的接口：
    - 同步方式：直接调用远程查询接口获取回复报文，可能需要手动调整接口的超时入参；
    - 异步方式：订阅回复报文，发送查询报文，异步等待收到回复报文(一般来说异步也需要有超时处理，超时后不再等待)；

## 编码实践

从上面架构可以看到，绝大多数的编码工作放在了api侧，server与client端只是简单的调用。如果想提供一个新的查询接口，需要按照api设计原则提供很多定义及接口实现，为了尽量简化开发过程并统一设计实现原则，在实践中采用了宏定义的方式来进行辅助编码。

- 为了方便使用宏定义，先将查询接口抽象出两个定义，查询主体与查询功能。

> 这里主要考虑不同查询主体对同一个查询功能的要求不一致。例如画面浏览工具的右键菜单查询功能、与告警工具的右键菜单查询功能就完全不一样。
> 需要抽象为两个接口：画面浏览工具-菜单查询，告警工具-菜单查询；

### 变量定义宏

变量定义宏的作用是提供查询报文、回复报文的结构体定义、回调函数名称定义等等。其形式为`#define SCADA_REGISTER_QUERY_DEFINE(main, func)`
，其中`main`代表查询主体，`func`代表查询功能。
还是以画面浏览工具的菜单查询为例，相应的宏调用代码为`SCADA_REGISTER_QUERY_DEFINE(Viewer, Menu)`。
> 为了保证自动生成的代码美观度，查询主体及查询功能的命名请按照首字母大写的规则来定义

宏定义的报文结构体命名规则为`Scada##main##func##Request`和`Scada##main##func##Response`
,即画面浏览工具菜单查询的报文结构体定义为`ScadaViewerMenuRequest`和`ScadaViewerMenuResponse`。
宏生成的报文结构体只能是前向声明，还需要手动完成实体定义，如下所示：

 ```C++
 struct ScadaQueryResponse {
    bool success{false};
    std::string msg{};
};

SCADA_REGISTER_QUERY_DEFINE(Viewer, Menu)

struct SCADA_GUI_QUERY_API ScadaViewerMenuRequest {
    String userName{};
    String hostName{};
    TDBOID objOID{};
    Octet instNo{0};
    String graphTypeName{};

    IASP_IOSTREAM_DEFINE(ScadaViewerMenuRequest, userName, hostName, objOID, instNo, graphTypeName)
};

struct SCADA_GUI_QUERY_API ScadaViewerMenuResponse : ScadaQueryResponse {
    std::vector<ScadaViewerMenu> menus{};

    IASP_IOSTREAM_DEFINE(ScadaViewerMenuResponse, success, msg, menus)
};

 ```

报文结构体定义需要注意两点原则：

- 报文结构体内需包含序列化声明IASP_IOSTREAM_DEFINE；
- 回复报文需要从ScadaQueryResponse继承，api在生成回复报文时，success域用于表示查询是否成功，msg域用于填写失败原因；

### 接口定义宏

接口定义宏的作用是提供api接口定义及大部分接口的实现。其形式为`#define SCADA_REGISTER_QUERY_DEFINE(main, func)`
，其中`main`代表查询主体，`func`代表查询功能。
还是以画面浏览工具的菜单查询为例，相应的宏调用代码为`SCADA_REGISTER_QUERY_API(Viewer, Menu)`。以下为宏定义的接口说明：

| 接口形式                                                                                                                   | 调用者                      | 需要自行实现 |
|------------------------------------------------------------------------------------------------------------------------|--------------------------|--------|
| auto queryViewerMenu(const ScadaViewerMenuRequest& req) -> ScadaViewerMenuResponse                                     | 服务程序调用，需保证本地有scadamdl数据库 | 是      |
| auto syncQueryViewerMenu(const ScadaViewerMenuRequest& req, ScadaViewerMenuResponse& resp, int timeout) -> Long        | 客户端程序调用，无本地数据库部署要求       | 否      |
| auto getViewerMenuRequestEventId() const -> ULongLong                                                                  | api接口内部调用                | 否      |
| auto getViewerMenuResponseEventId() const -> ULongLong                                                                 | api接口内部调用                | 否      |
| auto subscribeViewerMenuResponse(const ScadaViewerMenuResponseCb& callback) const -> Long                              | 客户端程序调用                  | 否      |
| auto unsubscribeViewerMenuResponse() const -> Long                                                                     | 客户端程序调用                  | 否      |
| auto sendViewerMenuResponse(const ScadaViewerMenuResponse& resp, const net::NetInfo& info, bool useJson) const -> Long | 服务端程序调用                  | 否      |
| auto subscribeViewerMenuRequest(const ScadaViewerMenuRequestCb& callback) const -> Long                                | 服务端程序调用                  | 否      |
| auto unsubscribeViewerMenuRequest() const -> Long                                                                      | 服务端程序调用                  | 否      |
| auto sendViewerMenuRequest(const ScadaViewerMenuRequest& req, bool useJson) const -> Long                              | 客户端程序调用                  | 否      |

从上表可以看出，只有第一个接口需要自行补充实现，其余接口都是由宏自动生成实现代码。综上所述，新加一个查询接口的代价就是调用两个定义宏，并实现查询/回复报文结构体与通过查询报文得到回复报文的函数。