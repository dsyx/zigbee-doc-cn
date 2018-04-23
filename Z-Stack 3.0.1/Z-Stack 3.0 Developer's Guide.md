 ***Z-Stack 3.0 开发指南 (Z-Stack 3.0 Developer's Guide)*** 
 =========================================================

- [ ***Z-Stack 3.0 开发指南 (Z-Stack 3.0 Developer's Guide)*** ](#z-stack-30--z-stack-30-developers-guide)
- [**1. 引言 (Introduction)**](#1--introduction)
    - [**1.1 目的 (Purpose)**](#11--purpose)
    - [**1.2 范围 (Scope)**](#12--scope)
    - [**1.3 术语及其定义 (Definitions, Abbreviations and Acronyms)**](#13--definitions--abbreviations-and-acronyms)
    - [**1.4 参考文档 (Reference Documents)**](#14--reference-documents)
- [**2. ZigBee**](#2-zigbee)
    - [**2.1 设备类型 (Device Types)**](#21--device-types)
        - [**2.1.1 协调器 (Coordinator)**](#211--coordinator)
        - [**2.1.2 路由器 (Router)**](#212--router)
        - [**2.1.3 终端设备 (End-device)**](#213--end-device)
    - [**2.2 栈配置文件 (Stack Profile)**](#22--stack-profile)
- [**3. 地址 (Addressing)**](#3--addressing)
    - [**3.1 地址类型 (Address types)**](#31--address-types)
    - [**3.2 网络地址分配 (Network address assignment)**](#32--network-address-assignment)
        - [**3.2.1 随机编址 (Stochastic Addressing)**](#321--stochastic-addressing)
    - [**3.3 Z-Stack寻址 (Addressing in Z-Stack)**](#33-z-stack-addressing-in-z-stack)
        - [**3.3.1 单点寻址/单播 (Unicast)**](#331---unicast)
        - [**3.3.2 间接寻址 (Indirect)**](#332--indirect)
        - [**3.3.3 广播寻址/广播 (Broadcast)**](#333---broadcast)
        - [**3.3.4 组寻址/组播 (Group Addressing)**](#334---group-addressing)
    - [**3.4 重要设备地址 (Important Device Addresses)**](#34--important-device-addresses)
- [**4. 绑定 (Binding)**](#4--binding)
    - [**4.1 建立绑定表 (Building a Binding Table)**](#41--building-a-binding-table)
        - [**4.1.1 ZigBee设备对象绑定请求 (ZigBee Device Object Bind Request)**](#411-zigbee-zigbee-device-object-bind-request)
            - [**4.1.1.1 启动应用 (The Commissioning Application)**](#4111--the-commissioning-application)
            - [**4.1.1.2 ZigBee设备对象终端设备绑定请求 (ZigBee Device Object End Device Bind Request)**](#4112-zigbee-zigbee-device-object-end-device-bind-request)
        - [**4.1.2 设备应用程序绑定管理器 (Device Application Binding Manager)**](#412--device-application-binding-manager)
        - [**4.1.3 查找和绑定 (Finding and binding)**](#413--finding-and-binding)
    - [**4.2 配置源绑定 (Configuring Source Binding)**](#42--configuring-source-binding)
- [**5. 路由 (Routing)**](#5--routing)
    - [**5.1 概述 (Overview)**](#51--overview)
    - [**5.2 路由协议 (Routing protocol)**](#52--routing-protocol)
        - [**5.2.1 路由发现和选择 (Route Discovery and Selection)**](#521--route-discovery-and-selection)
        - [**5.2.2 路由维护 (Route maintenance)**](#522--route-maintenance)
        - [**5.2.3 路由过期 (Route expiry)**](#523--route-expiry)
    - [**5.3 表存储 (Table storage)**](#53--table-storage)
        - [**5.3.1 路由表 (Routing table)**](#531--routing-table)
        - [**5.3.2 路由发现表 (Route discovery table)**](#532--route-discovery-table)
    - [**5.4 多对一路由协议 (Many-to-One Routing Protocol)**](#54--many-to-one-routing-protocol)
        - [**5.4.1 多对一路由概述 (Many-to-One Routing Overview)**](#541--many-to-one-routing-overview)
        - [**5.4.2 多对一路由发现 (Many-to-One Route Discovery)**](#542--many-to-one-route-discovery)
        - [**5.4.3 路由记录命令 (Route Record Command)**](#543--route-record-command)
        - [**5.4.4 多对一路由维护 (Many-to-One Route Maintenance)**](#544--many-to-one-route-maintenance)
    - [**5.5 路由设置快速参考 (Routing Settings Quick Reference)**](#55--routing-settings-quick-reference)
    - [**5.6 路由器离网关联清理 (Router Off-Network Association Cleanup)**](#56--router-off-network-association-cleanup)
- [**6. ZDO 消息请求 (ZDO Message Requests)**](#6-zdo--zdo-message-requests)
- [**7. 便携式设备 (Portable Devices)**](#7--portable-devices)
- [**8. 端到端确认 (End-to-end acknowledgements)**](#8--end-to-end-acknowledgements)
- [**9. 杂项 (Miscellaneous)**](#9--miscellaneous)
    - [**9.1 信道配置 (Configuring channel)**](#91--configuring-channel)
    - [**9.2 PAN ID 配置和加入网络 (Configuring the PAN ID and network to join)**](#92-pan-id--configuring-the-pan-id-and-network-to-join)
    - [**9.3 最大有效载荷大小 (Maximum payload size)**](#93--maximum-payload-size)
    - [**9.4 离开网络 (Leave Network)**](#94--leave-network)
    - [**9.5 描述符 (Descriptors)**](#95--descriptors)
    - [**9.6 非易失性存储项 (Non-Volatile Memory Items)**](#96--non-volatile-memory-items)
        - [**9.6.1 非易失性存储全局配置 (Global Configuration Non-Volatile Memory)**](#961--global-configuration-non-volatile-memory)
        - [**9.6.2 网络层非易失性存储 (Network Layer Non-Volatile Memory)**](#962--network-layer-non-volatile-memory)
        - [**9.6.3 应用非易失性存储 (Application Non-Volatile Memory)**](#963--application-non-volatile-memory)
    - [**9.7 异步链接 (Asynchronous Links)**](#97--asynchronous-links)
    - [**9.8 多播消息 (Multicast Messages)**](#98--multicast-messages)
    - [**9.9 分片 (Fragmentation)**](#99--fragmentation)
        - [**9.9.1 快速参考 (Quick Reference)**](#991--quick-reference)
    - [**9.10 扩展的 PAN ID (Extended PAN IDs)**](#910--pan-id-extended-pan-ids)
    - [**9.11 以预启动的网络参数重新加入网络 (Rejoining with Pre-Commissioned Network parameters)**](#911--rejoining-with-pre-commissioned-network-parameters)
    - [**9.12 子管理 (Child management)**](#912--child-management)
        - [**9.12.1 配置父设备的子管理 (Configuring child management for parent device)**](#9121--configuring-child-management-for-parent-device)
        - [**9.12.2 配置子设备的子管理 (Configuring child management for child devices)**](#9122--configuring-child-management-for-child-devices)
        - [**9.12.3 父设备 Annce (Parent Annce)**](#9123--annce-parent-annce)
- [**10. 安全 (Security)**](#10--security)
    - [**10.1 概述 (Overview)**](#101--overview)
    - [**10.2 配置 (Configuration)**](#102--configuration)
    - [**10.3 集中式安全网络 (Centralized security network)**](#103--centralized-security-network)
        - [**10.3.1 信任中心策略 (Trust center policies)**](#1031--trust-center-policies)
            - [**10.3.1.1 zgAllowRemoteTCPolicyChange**](#10311-zgallowremotetcpolicychange)
            - [**10.3.1.2 bdbJoinUsesInstallCodeKey**](#10312-bdbjoinusesinstallcodekey)
            - [**10.3.1.3 bdbTrustCenterRequireKeyExchange**](#10313-bdbtrustcenterrequirekeyexchange)
        - [**10.3.2 密钥更新 (Key Updates)**](#1032--key-updates)
    - [**10.4 分布式安全网络 (Distributed security network)**](#104--distributed-security-network)
    - [**10.5 链接密钥类型 (Link Key types)**](#105--link-key-types)
        - [**10.5.1 默认全局信任中心链接密钥 (Default global Trust Center link key)**](#1051--default-global-trust-center-link-key)
        - [**10.5.2 安装代码派生的信任中心链接密钥 (Install Code Derived Trust Center Link Key)**](#1052--install-code-derived-trust-center-link-key)
        - [**10.5.3 分布式安全全局链接密钥 (Distributed security global link key)**](#1053--distributed-security-global-link-key)
        - [**10.5.4 Touchlink 预配置链接密钥 (Touchlink preconfigured Link Key)**](#1054-touchlink--touchlink-preconfigured-link-key)
    - [**10.6 非安全入网 (Unsecure join to a network)**](#106--unsecure-join-to-a-network)


# **1. 引言 (Introduction)**

## **1.1 目的 (Purpose)**

本文将讲解德州仪器的 ZigBee 栈(Z-Stack)的一些组件及其功能，并阐述该栈中可配置的参数及其配置方法，让开发者清楚应该如何更改参数以适应应用程序的需求。

## **1.2 范围 (Scope)**

本文将介绍德州仪器的 *Z-Stack™* 发行版里的概念和设置。 Z-Stack 是一个兼容ZigBee标准和 ZigBee PRO 栈配置文件的 ZigBee-2015 栈。本文还介绍了 Z3.0 的附加功能以及这些功能如何兼容 Z3.0 或传统设备的方法。

## **1.3 术语及其定义 (Definitions, Abbreviations and Acronyms)**

 | 术语          | 解析                                              |
 | :------------ | :------------------------------------------------ |
 | AF            | 应用程序框架                                      |
 | AES           | 高级加密标准                                      |
 | AIB           | 应用支持子层信息库                                |
 | API           | 应用程序接口                                      |
 | APS           | 应用支持子层                                      |
 | APSDE         | 应用支持子层数据实体                              |
 | APSME         | 应用支持子层管理实体                              |
 | ASDU          | 应用支持子层服务数据报单元                        |
 | BDB           | 基本设备行为                                      |
 | BSP           | 板级支持包—— HAL&OSAL 通常认为是一个 BSP        |
 | CCM*          | 增强型 CBC-MAC 模式运算器                         |
 | EPID          | 扩展的个域网标识符                                |
 | GP            | 绿色能源                                          |
 | GPD           | 绿色能源设备                                      |
 | HAL           | 硬件抽象层                                        |
 | MSG           | 消息                                              |
 | MT            | Z-Stack 协议栈的监测和测试层                      |
 | NHLE          | 下一个更高层的实体                                |
 | NIB           | 网络基本信息                                      |
 | NWK           | 网络                                              |
 | OSAL          | Z-Stack 协议栈的操作系统抽象层                    |
 | OTA           | 空中下载                                          |
 | PAN           | 个域网                                            |
 | RSSI          | 接收信号强度指示                                  |
 | SE            | 智能能源                                          |
 | Sub-Device    | Zigbee 设备应用端点中的独立设备功能               |
 | TC            | 信任中心                                          |
 | TCLK          | 信任中心链接密钥                                  |
 | ZCL           | ZigBee 群集库                                     |
 | ZDO           | ZigBee 设备对象                                   |
 | ZHA           | ZigBee 家居自动化                                 |
 | ZC            | ZigBee 协调器                                     |
 | ZR            | ZigBee 路由                                       |
 | ZED           | ZigBee 终端                                       |

## **1.4 参考文档 (Reference Documents)**

1. Texas Instruments document SWRA195, Z-Stack API
2. Texas Instruments document SWRA194, Z-Stack OSAL API
3. Texas Instruments document SWRU354, Z-Stack 3.0 Sample Application User’s Guide.
4. Texas Instruments document SWRA353, Z-Stack OTA Upgrade User’s Guide.
5. ZigBee document 05-3474-21 ZigBee ZigBee Specification
6. ZigBee document 07-5123-06 ZigBee Cluster Library Specificiation
7. ZigBee document 13-0402-13 ZigBee Base Device Behavior
8. ZigBee document 14-0563-16 ZigBee Green Power specification

# **2. ZigBee**

ZigBee 网络是一种由一些使用电池供电的设备连结成的多跳网络，这意味着两个设备在 ZigBee 网络中交换数据可能需要依赖其他的中间设备才能完成。ZigBee 网络的这种合作性质，要求网络中的设备都应

1. 具有执行特定网络的功能。
2. 可以配置某些参数为特定值。

设备所执行的网络功能决定其在网络中的角色，这称为设备类型。需要配置成特定值的一些参数以及这些参数的值被称为栈配置文件。

## **2.1 设备类型 (Device Types)**

ZigBee 网络中有三种逻辑设备类型：

1. 协调器 (Coordinator)
2. 路由器 (Router)
3. 终端设备 (End-device)

ZigBee 网络由一个具有组网能力的设备(协调器或路由器)、多个路由器和终端设备组成。  

Note：  
设备类型不会限制在特定设备上运行的应用程序的类型。

![Figure 1](https://raw.githubusercontent.com/Shanyaoxing12/zigbee-doc-cn/master/pic/20180421-1.png)

Figure 1 是一个简单的 ZigBee 网络示意图，其中黑色的设备为协调器，红色的设备为路由器，白色的设备为终端设备。

### **2.1.1 协调器 (Coordinator)**

协调器是具有组网能力的设备，但它没有加入网络的能力，这意味着它只能创建自己的网络，而不能加入现有的网络。在创建网络时，协调器会先扫描现有的射频环境(RF environment)并选择一个信道和一个网络标识符(PAN ID)，然后启动网络。在 Z3.0 中，协调器会创建一个集中式的安全网络，并且被授权为该网络的信任中心，这意味着协调器是该网络的安全管理者，并且是唯一能够分发密钥并允许其它设备加入其创建的网络的设备。  

协调器也可以(可选)用来协助绑定网络中的应用程序级。  

协调器的主要任务是启动网络和管理密钥，除此之外，它的行为与路由器相似。需要注意的是，其它设备的入网和退网过程都必须有协调器的参与，因此协调器不能离开自己创建的网络。  

想进一步了解安全相关的内容，请参阅 第 10 章。

### **2.1.2 路由器 (Router)**

路由器具有以下能力：

1. 允许其它设备加入网络；
2. 多跳路由；
3. 协助其子设备通信。

在 Z3.0 中，路由器被授予组网能力，允许其创建分布式的安全网络。这种组网能力允许路由器创建没有安全管理者的网络，这意味着路由器一旦创建网络后，其在该网络中就没有任何特殊的作用。  

更多详细内容，请参阅 第 10 章。  

一般来说，路由器被要求是随时活跃的，因此路由器应该使用电源供电。

### **2.1.3 终端设备 (End-device)**

终端设备没有任何具体的维护和建设网络的责任，因此它可以选择进入休眠或是唤醒状态，并且通常可以使用电池对其进行供电。  

一般而言，终端设备对内存的要求较低。  


Notes：  
在 Z-Stack 中，设备类型通常在编译的时候通过编译选项(ZDO_COORDINATOR and
RTR_NWK)确定。所有的应用示例都提供了单独的项目文件以构建不同的设备类型。

## **2.2 栈配置文件 (Stack Profile)**

需要配置为特定值的栈参数集以及上述设备类型值被称为栈配置文件，这些参数和值由 ZigBee 联盟定义。  

在网络中的所有设备的栈配置文件都必须一致(即网络中的所有设备都必须具有栈配置文件且参数和值必须相同)。  

应用开发者可以将设备的栈配置文件设置成其它的值(非 ZigBee 标准的值)，但这样做的话，这个设备将不能与那些遵循 ZigBee 标准的设备进行互操作。这些不遵循 ZigBee 标准的设备搭建的网络被称为封闭网络(closed networks)，其栈配置文件被称为特定网络(network-specific)栈配置文件。  

设备的栈配置文件标识符存在于该设备的发送信标中，这使设备能够在加入网络前就可以确定网络的栈配置文件。其中：

1. 特定网络的栈配置文件的 ID 为 0；
2. 传统 ZigBee 的栈配置文件的 ID 为 1；
3. ZigBee PRO 的栈配置文件(被用在 Z3.0)的 ID 为 2。

栈配置文件标识符可以通过 **nwk_globals.h** 文件下的 **STACK_PROFILE_ID** 参数进行配置。值为 3 的标识符是为绿色能源设备保留的，它出现在各自的框架中。

# **3. 地址 (Addressing)**

## **3.1 地址类型 (Address types)**

ZigBee 设备中有两种类型的地址：

* 64 位的 IEEE 地址(也称 MAC 地址或扩展地址)
* 16 位的网络地址(也称逻辑地址或短地址)

64 位地址是一种全球性的唯一的地址，一经分配便伴随设备的一生。它通常由制造商或被安装时设置，并且由 IEEE 组织进行维护和分配。  

有关如何获取这些地址块的更多信息，请访问 http://standards.ieee.org/regauth/oui/index.shtml.  

16 位地址在设备加入网络时被分配，并且被使用在网络中。它在网络中是唯一的，可以用于网络中的设备识别和发送数据。

## **3.2 网络地址分配 (Network address assignment)**

### **3.2.1 随机编址 (Stochastic Addressing)**

ZigBee PRO 使用随机(random)编址的方案来分配网络地址。该编址方案随机地将短地址分配给新的设备，并且该短地址确保与网络中的其它设备地址不重复。  

当一个设备加入时，它将获得其父设备随机生成的地址，随后向网络中的其它设备发出“设备声明(Device Announce)”(宣告包含该设备的短地址和扩展地址)。如果有其它设备具有相同的短地址，则网络中的设备(路由器)将向整个网络发出广播“网络状态——地址冲突(Network Status – Address Conflict)”，并且所有具有冲突地址的设备将更改其短地址。在冲突设备改变它们的地址后，它们会发出各自的“设备声明”检查它们的新地址是否在网络中发生冲突。  

终端设备不参与“地址冲突”，其父设备会为其处理这个事件。如果终端设备上发生“地址冲突”，其父设备会向其发送“重新加入响应(Rejoin Response)”，以更改其短地址。在更新地址后，终端设备会发出“设备声明”以检查其新地址在网络中是否在冲突。  

当收到“设备声明”时，关联表和绑定表将被更新为新的短地址，路由表信息不会被更新(必须建立新的路由)。如果父设备确定“设备声明”属于其子设备下的一个子设备，而不是其直接的子设备，则父设备会认为该子设备已经迁移到另一个父设备。

## **3.3 Z-Stack寻址 (Addressing in Z-Stack)**

通常使用 **AF_DataRequest()** 函数将数据发送给ZigBee网络上的设备。 **afAddrType_t** (在 **ZComDef.h** 文件中定义)为数据包发送的目标设备的类型。

    typedef struct
    {
        union
        {
            uint16      shortAddr;
            ZLongAddr_t extAddr;
        } addr;
        afAddrMode_t    addrMode;
        byte            endPoint;
    } afAddrType_t;

Note:  
除了网络地址外，还需要指定寻址模式。目标寻址模式可以选择一个以下的值(AF寻址模式在 **AF.h** 文件中定义)：

    typedef enum
    {
        afAddrNotPresent = AddrNotPresent,
        afAddr16Bit      = Addr16Bit,
        afAddr64Bit      = Addr64Bit,
        afAddrGroup      = AddrGroup,
        afAddrBroadcast  = AddrBroadcast
    } afAddrMode_t;

寻址模式是必要的，因为在 ZigBee 网络中，数据包可以通过单播(unicast)、组播(multicast)或广播(broadcast)的模式发送。单播模式下，数据包会被发送到一台设备上；组播模式下，数据包会被发送到设备组上；广播模式下，数据包通常被发送到网络中的所有设备上。

### **3.3.1 单点寻址/单播 (Unicast)**

这是一种常规的寻址模式，该模式下可以将数据包发送到已知网络地址的当个设备上。使用该模式发送数据包，需要将 **addrMode** 设置成 **Addr16Bit** ，并且将目标设备的网络地址加载到数据包中。  

### **3.3.2 间接寻址 (Indirect)**

当不知道数据包的最终目的地的时，可以使用该寻址模式，该模式不需要指定目标地址，因为它会从发送设备的栈中的“绑定表(binding table)”中查找目标。这也被称为源绑定(Source binding)，详细内容请参阅后文与绑定有关的内容。使用该模式发送数据包，需要将 **addrMode** 设置成 **AddrNotPresent** 。  

当数据包被发送到栈时，目标地址和端点将从绑定表中被查找和使用。如果在绑定表中找到多个目标设备，则会将数据包的副本发送给这些设备。如果找不到绑定条目，则数据包将不会被发送。

### **3.3.3 广播寻址/广播 (Broadcast)**

当需要向网络中的所有设备发送数据包时，可以使用该寻址模式。使用该模式发送数据包，需要将 **addrMode** 设置成 **AddrBroadcast** ，并且目标地址可以设置为以下的广播地址之一：

1. **NWK_BROADCAST_SHORTADDR_DEVALL** (0xFFFF) – 消息将被发送到网络中的所有设备(包括休眠设备)。对于休眠设备，消息保留在其父设备，直到休眠设备轮询或消息超时( **f8wConfig.cfg** 文件中的 **NWK_INDIRECT_MSG_TIMEOUT** )
2. **NWK_BROADCAST_SHORTADDR_DEVRXON** (0xFFFD) – 消息将被发送到空闲时接收器打开的所有设备( **RXONWHENIDLE** )，即除了休眠设备外的所有设备
3. **NWK_BROADCAST_SHORTADDR_DEVZCZR** (0xFFFC) – 将消息发送给所有路由器(包括协调器)

### **3.3.4 组寻址/组播 (Group Addressing)**

当希望将数据包发送给一组设备时，可以使用该寻址模式。使用该模式发送数据包，需要将 **afAddrGroup** 和 **addr.shortAddr** 设置成组标识符。在使用该模式前，必须在网络中定义组(参阅 Z-Stack API[1] 文档中的 **aps_AddGroup()** )。  

Note：  
组寻址可以与间接寻址结合使用，在绑定表中的目标地址可以是单播地址或组播地址。另外，广播寻址只是提前设置好群组的一种组寻址的特例。  

将设备添加到标识符为 1 的组中，示例代码：

    aps_Group_t group;

    // Assign yourself to group 1
    group.ID = 0x0001;
    group.name[0] = 6; // First byte is string length
    osal_memcpy( &(group.name[1]), “Group1”, 6);
    aps_AddGroup( SAMPLEAPP_ENDPOINT, &group );

## **3.4 重要设备地址 (Important Device Addresses)**

应用程序可能需要知道自身的地址和父设备的地址。  

使用下列函数可以获取本设备的地址(在 Z-Stack API[1] 文档中定义)：

* **NLME_GetShortAddr()** – 返回本设备的 16 位网络地址
* **NLME_GetExtAddr()** – 返回本设备的 64 位扩展地址

使用下列函数可以获取父设备的地址(在 Z-Stack API[1] 文档中定义，这些函数中的术语“Coord”不是指协调器，而是指设备的父设备)：

* **NLME_GetCoordShortAddr()** – 返回父设备的 16 位网络地址
* **NLME_GetCoordExtAddr()** – 返回父设备的 64 位扩展地址

# **4. 绑定 (Binding)**

绑定是一种应用程序之间(两个或多个)消息流的控制机制。在所有设备中实施的绑定机制，称为源绑定。  

绑定允许应用程序在不知道目标地址的情况下发送数据包，APS 层会从其绑定表中确定目标地址，然后将消息转发到应用目标(或多个应用目标)或应用组上。

## **4.1 建立绑定表 (Building a Binding Table)**

有 4 种方法建立绑定表：

1. ZigBee 设备对象绑定请求(ZigBee Device Object Bind Request) – 启动工具可以告诉设备制作一个绑定记录
2. ZigBee 设备对象终端设备绑定请求(ZigBee Device Object End Device Bind Request) – 两个设备可以把它们想要设置的绑定表记录告诉协调器，协调器将对它们进行匹配并创建绑定表条目
3. 设备应用程序(Device Application) – 设备上的应用程序可以建立或管理绑定表
4. 在发起设备的启动过程中查找和绑定(Finding and Binding commissioning process for initiator devices)

### **4.1.1 ZigBee设备对象绑定请求 (ZigBee Device Object Bind Request)**

任何设备或应用都可以向其它设备(over the air)发送 ZDO 消息，以便为网络中的其它设备创建绑定记录，这称为协助绑定，发送消息的设备将创建绑定条目。

#### **4.1.1.1 启动应用 (The Commissioning Application)**

应用程序可以通过调用 **ZDP_BindReq()** [在 **ZDProfile.h** 中定义]并在绑定记录中包含 2 个 applications (地址和端点)来完成这个操作。第一个参数(target **dstAddr** )为绑定源地址的短地址(绑定记录将存储在该地址中)。调用 **ZDP_UnbindReq()** 并传入参数可以删除绑定记录。  

目标设备会返回ZigBee设备对象绑定(ZigBee Device Object Bind)或解绑(Unbind Response)的响应信息，协调器上的 ZDO 代码会通过调用 **ZDApp_ProcessMsgCBs()** 将返回的操作状态解析并通知 **ZDApp.c** 。  

响应绑定时，协调器返回的状态将会是 **ZDP_SUCCESS** 、 **ZDP_TABLE_FULL** 、 **ZDP_INVALID_EP** 或 **ZDP_NOT_SUPPORTED** 。  

响应解绑时，协调器返回的状态将会是 **ZDP_SUCCESS** 、 **ZDP_NO_ENTRY** 、 **ZDP_INVALID_EP** 或**ZDP_NOT_SUPPORTED** 。

#### **4.1.1.2 ZigBee设备对象终端设备绑定请求 (ZigBee Device Object End Device Bind Request)**

该机制是在超时时间内，通过对选定的设备使用按钮按压或其它类似的动作来进行绑定。协调器在超时时间内收集终端设备的绑定请求消息，并根据配置文件 ID (profile ID )和 簇 ID (cluster ID)的协定生成绑定表条目。默认的终端绑定超时时间( **APS_DEFAULT_MAXBINDING_TIME** )为 16 秒 ( **nwk_globals.h** 中定义)，如果将其添加到 **f8wConfig.cfg** 中或作为编译标志，则可以对其进行更改。  

在终端设备的绑定过程中，协调器会注册 **ZD_RegisterForZDOMsg()** 以接收终端设备绑定请求， **ZDApp_RegisterCBs()** 中的绑定和解绑 ZDO 消息在 **ZDApp.c** 上定义。当收到这些消息时，这些消息会被发送到 **ZDApp_ProcessMsgCBs()** 中进行解析和处理。  

终端设备绑定是一个切换过程(toggle process)，这意味着在你初次执行这个过程时，它就会在请求设备中创建一个绑定条目，当你再次执行这个过程，它就会删除请求设备中的绑定。这就是为什么在后面的示例中，它会发送解绑请求，然后等待解绑结果，如果成功，则本来已存在绑定条目，否则它会发送绑定请求以创建条目。  

当协调器接收到 2 个匹配的终端设备的绑定请求时，它将启动在请求设备中创建源绑定条目的流程。如果在 ZDO 终端设备中发现匹配请求，协调器会执行以下步骤：

1. 向第一个设备发送 ZDO 解绑请求。终端设备绑定是切换过程，因此首先发送解除绑定以删除现有的绑定条目。
2. 等待 ZDO 解绑响应。如果响应状态为 **ZDP_NO_ENTRY** ，则发送 ZDO 绑定请求以在源设备中创建绑定条目；如果响应状态为 **ZDP_SUCCESS** ，则转到第一个设备的簇 ID (解除绑定删除条目 – 切换(the unbind removed the entry – toggle))。
3. 等待 ZDO 绑定响应。收到响应后，转到第一个设备的下一个簇 ID。
4. 第一个设备完成后，对第二个设备执行相同的过程。
5. 第二个设备完成后，将 ZDO 终端设备绑定响应消息发送给两个设备。

### **4.1.2 设备应用程序绑定管理器 (Device Application Binding Manager)**

在设备上输入绑定条目的另一种方法是让应用程序管理自己的绑定表，这意味着应用程序将通过调用以下绑定表管理函数对本地绑定表条目进行增删，参阅 Z-Stack API[1] 文档 - 绑定表管理章节：

* bindAddEntry() – 向绑定表中添加条目
* bindRemoveEntry() – 从绑定表中删除条目
* bindRemoveClusterIdFromList() – 从现有的绑定表中删除一个簇 ID
* bindAddClusterIdToList() – 添加一个簇 ID 到现有的绑定表中
* bindRemoveDev() – 通过地址引用删除所有条目
* bindRemoveSrcDev() – 通过源地址引用删除所有条目
* bindUpdateAddr () – 更新条目为另一个地址
* bindFindExisting () – 查找一个绑定表条目
* bindIsClusterIDinList() – 检查绑定表中现有的簇 ID
* bindNumBoundTo() – 具有相同地址的条目数(源或目标)
* bindNumOfEntries() – 表中的条目数量
* bindCapacity() – 允许最大的条目量
* BindWriteNV() – 在 NV 中更新表

### **4.1.3 查找和绑定 (Finding and binding)**

基础设备行为中定义了一种称为查找和绑定的启动方法，其过程依赖于识别簇和 ZDO 消息来允许启动设备查找具有匹配应用簇的设备。这种机制通常由用户触发，指定那些设备需要彼此“查找和绑定”，以便这些设备可以更高效地进行通信。更多详细，请参阅 15.7.2 节有关此方法的信息。  

## **4.2 配置源绑定 (Configuring Source Binding)**

要启用设备的源绑定，需要在 **f8wConfig.cfg** 中包含 **REFLECTOR** 编译标志和考虑 2 个绑定配置项( **NWK_MAX_BINDING_ENTRIES** & **MAX_BINDING_CLUSTER_IDS** )。 **NWK_MAX_BINDING_ENTRIES** 是绑定表中条目的最大数量， **MAX_BINDING_CLUSTER_IDS** 是每个绑定条目中簇 ID 的最大数量。绑定表保持在静态 RAM(未分配)中，因此每个条目的数量和条目的簇 ID 数量会影响 RAM 的使用量。每个绑定表条目的大小为 6 字节加上( **MAX_BINDING_CLUSTER_IDS** \* 2 个字节)。除了对 RAM 的使用量有影响外，绑定配置项还会影响地址管理器中的条目数。

# **5. 路由 (Routing)**

## **5.1 概述 (Overview)**

网状网络被描述成这样的网络：通信的过程由各个分布式的对等路由协作完成。(A mesh network is described as a network in which the routing of messages is performed as a decentralized, cooperative process involving many peer devices routing on each others’ behalf.)  

路由对应用层是完全透明的，应用程序只需将需要发送的数据发送到栈中，栈会负责查找路径。这样，应用程序便不知道它事实上是在多跳网络中运行。  

路由还可以实现 ZigBee 网络的“自愈(self healing)”性质。即便一个无线链路断开了，路由功能也能找到一条避开已断开链路的新路径。这极大地提高了无线网络的可靠性，这是 ZigBee 的关键特性之一。  

多对一(Many-to-one)路由是一种特殊的路由方式，被用在处理涉及集中式流量的场景。该方式是 ZigBee PRO 功能集的一部分，可以极大程度地减少流量，特别是当网络中的所有设备都将数据包发送到网关或数据集中器时。详细描述请参阅 5.4 节。  

## **5.2 路由协议 (Routing protocol)**

ZigBee 使用基于 AODV(无线自组网按需平面距离向量路由协议(Ad-hoc On-demand Distance Vector))的专用路由协议。为了在传感网络中的使用简易，ZigBee 路由协议促进了环境的能力，可以有效地减少链路故障和数据包丢失，并且支持设备移动。  

邻居路由器是指彼此在同一无线网络中的路由器。每个路由器在“邻居表(neighbor table)”中跟踪其邻居，并在路由器收到来自邻居路由器的(单播，广播或信标)任何消息时更新“邻居表”。  

当路由器接收到其应用程序或其它设备的单播数据包时，NWK 层会按照以下过程转发数据包：

* 如果目标地址是路由器(包含其子设备)的邻居之一，则数据包将直接传送到目标设备上。否则路由器将检查其路由表，以查找一个与数据包目标地址相对应的路由条目。
* 如果有活动的目标地址对应的路由条目，数据包将被中继到存储在路由表条目中的下一跳地址。
* 如果单次传输尝试失败，NWK 层将重复传输数据包并等待确认传输过程的结果，最多重复 **NWK_MAX_DATA_RETRIES** (在 **f8wconfig.cfg** 中配置)次。
* 如果路由表中找不到活动的条目或最大重试次数后失败，则会启动路由发现，并且缓存数据包，直到该过程完成。

ZigBee终端设备不执行任何路由功能。希望向任何设备发送数据包的终端设备只需将数据包转发给其父设备，父设备会为其行使路由功能。同样地，当任何设备希望将数据包发送给终端设备并发起路由发现时，终端设备的父设备会代表其进行响应。  

Note：  
ZigBee 树状寻址(非 PRO)分配方案可以根据其地址派生出到任何目标地址的路径。在 Z-Stack中，若常规路由过程无法启动(通常由于缺少路由表空间)，则会使用此机制进行自动回退。  

在 Z-Stack 中，路由应用已被优化存储的路由表。通常地，每个目标设备都需要一个路由表条目。但是通过将特定父级的终端设备的所有条目和该父级设备的条目相合并，可以实现优化存储而不丢失任何功能。  

ZigBee 路由器(包括协调器)执行以下路由功能：

1. 路由发现和选择
2. 路由维护
3. 路由过期

### **5.2.1 路由发现和选择 (Route Discovery and Selection)**

路由发现是网络设备合作寻找和确立网络路径的过程。路由发现可以由任何路由器设备发起，并始终针对特定的目标设备执行。路由发现机制会搜索源设备和目标设备之间的所有可行的路由，并尝试选择最佳的路由。  

路由选择是选择出可行的最低开销的路径。每个设备和相邻设备的连接都有一个“连接开销(link costs)”，连接开销通常与接收信号强度相关。通过将路线上所有的连接开销相加，就可以得到整条路线的“路由开销(route cost)”。路由算法会尝试选择最低开销的路由。  

路由发现通过使用请求/响应包实现。源设备通过向其邻居广播请求(RREQ)包来请求目标地址的路由。当设备收到 RREQ 包时，它将转播 RREQ 包。在转播前，设备会将新的连接开销更新到 RREQ 包的开销字段中，并在其路由发现表(5.3.2)中添加条目。这样，RREQ 包就携带了它遍历的所有链路的开销成本总和。这个过程会一直重复，直到 RREQ 包到达目标设备。多个 RREQ 包将通过不同的路线到达目标设备，这些 RREQ 包中都包含了各个路线的开销成本。目标设备会选择最佳的 RREQ 包，并将路由响应(RREP)包发送回源设备。  

RREP 包会沿着原来的中间设备，返回到发出请求的源设备中。当 RREP 包返回到源设备时，中间设备更新其路由表以指示到目标设备的路由。每个中间设备中路由发现表被用来确定 RREP 包的下一跳返回源(即原 RREQ 的传播路径)，并将条目添加进路由表中。  

一旦创建了路由，就可以发送数据包。当一个设备丢失了它的一个下一跳连接(设备发送数据包时没有收到 MAC ACK)时，它会发送 RREP 包到所有可能接收到该包的设备上，并将丢失的连接标记成坏的(使其路由表失效)。在收到 RREQ、RREP 或 RERR 包后，设备将更新其路由表。

### **5.2.2 路由维护 (Route maintenance)**

网状网络提供路由维护和自愈能力。中间设备会沿着连接追踪链路上的失败传输。如果(相邻的)链路被确认为坏的，则上游设备将启动所有使用该链路的路由的路由修复。通过发起路由的再发现，直到下一次数据包到达该设备时，路由修复完成。如果路由的再发现无法启动，或因某种原因导致再发现失败，则设备会将路由错误(RERR)包发送回源设备，然后负责启动新的路由发现。无论如何，路线都会自动重新建立。

### **5.2.3 路由过期 (Route expiry)**

路由表维护那些已建立的路由条目。如果一段时间内没有数据包沿该路由发送，该路由将会被标记为过期。过期的路由不会被删除，除非存储空间不足。路由的自动过期时间可以在 **f8wconfig.cfg** 中配置。 **ROUTE_EXPIRY_TIME** 可以配置以秒为单位的过期时间，配置为 0 时会关闭路由过期的功能。

## **5.3 表存储 (Table storage)**

路由功能要求路由器维护一些表。

### **5.3.1 路由表 (Routing table)**

每个 ZigBee 路由器(包括协调器)都包含一个路由表，其存储了该设备参与的路由的必要信息。每个路由表条目都包含目标地址，下一跳设备和链路状态。所有发送到目标地址的数据包都会通过下一跳设备进行路由。此外，路由表中的条目可能会过期，以便回收表的空间。  

路由表容量指示设备路由表可存放的总条目数。路由表的大小可以通过 **f8wconfig.cfg** 中的 **MAX_RTG_ENTRIES** 进行配置(默认值为 40)。有关路由过期的详细信息，请参阅路由过期部分。

### **5.3.2 路由发现表 (Route discovery table)**

路由设备参与路由发现，并维护路由发现表。路由发现表用于路由发现进行时的临时信息存储。表中存储的条目只在其路由发现操作期间有效，一旦临时条目到期，它就可以被用于另一个路由发现操作。因此，路由发现表的最大条目值决定了可以在网络中同时执行的路由发现的最大数量。该值通过 **f8wconfig.cfg** 中的 **MAX_RREQ_ENTRIES** 进行配置。

## **5.4 多对一路由协议 (Many-to-One Routing Protocol)**

以下解释了多对一和源路由的过程，以便用户更好地理解 ZigBee 路由协议。事实上，所有的路由都在网络层进行处理，对应用程序来说是透明的。由应用程序决定发出多对一的路由发现和路由维护。

### **5.4.1 多对一路由概述 (Many-to-One Routing Overview)**

在 ZigBee PRO 中采用多对一路由可以帮助最大限度地减少流量，特别是在涉及集中式流量的场景时。低功耗无线网络通常具有充当网关或数据集中器的设备。网络中的所有设备至少应该维护一条到中心设备的有效路由，为了实现这一点，所有设备都必须依赖现有的(基于 ZigBee AODV的)路由解决方案，启动集中器的路由发现。路由的请求广播将会加在一起并在网络上产生巨大的影响。为了更好地优化路由解决方案，采用多对一路由以允许数据集中器利用单个路由发现来建立来自网络中所有设备的路由并且将路由发现广播风暴最小化。  

源路由时多对一路由的一部分，为集中器发送响应或确认信息回目标设备提供了一种有效的方式。集中器将从其到目标设备的完整路由信息放入需要传输的数据帧中。它最大限度地减少了网络中的路由表大小和路由发现流量。

### **5.4.2 多对一路由发现 (Many-to-One Route Discovery)**

下图显示了多对一路由的发现过程。为了发起多对一路由发现，集中器向整个网络广播多对一路由请求。一旦收到路由请求，每个设备都添加一个路由表条目到集中器并存储，将请求中继到下一跳地址的单跳邻居。该过程不会生成路由应答。

![Figure 2](https://raw.githubusercontent.com/Shanyaoxing12/zigbee-doc-cn/master/pic/20180421-2.png)

多对一路由请求命令类似于具有相同命令 ID 和 负荷帧格式的单播路由请求命令。路由请求中的选择字段是多对一的，并且目标地址为 0xFFFC。以下 Z-Stack API 可以用于集中器发送多对一的路由请求(有关此 API 的详细用法，请参阅 Z-Stack API[1] 文档)：

    ZStatus_t NLME_RouteDiscoveryRequest( uint16 DstAddress, byte options, uint8 radius ) 

选择字段是一个位掩码，用于指定路由请求的选项，可以是以下的值：

 | 值   | 描述                                         |
 | :--- | :------------------------------------------- |
 | 0x00 | 单播路由发现                                 |
 | 0x01 | 路由缓存的多对一路由发现(集中器没有内存限制) |
 | 0x03 | 非路由缓存的多对一路由发现(集中器有内存限制) |

 当选项字段的值为 0x01 或 0x03 时， **DstAddress** 字段将被多对一的目标地址 0xFFFC 覆盖。因此，在多对一路由请求的情况下，用户可以将任何值传递给 **DstAddress** 。

### **5.4.3 路由记录命令 (Route Record Command)**

上述的多对一路由发现过程建立了从所有设备到集中器的路由。逆向路由(从集中器到其它设备)通过路由记录命令完成。源路由的过程如图 3 所示。R1 通过先前建立起的多对一路由向集中器发送数据包 DATA，并期望返回确认。为了提供路由给集中器发回 ACK，R1 会将路由记录命令随数据包一并发送，命令将记录数据包经过的路由，并向集中器提供一个逆向路由来发回 ACK。

![Figure 3](https://raw.githubusercontent.com/Shanyaoxing12/zigbee-doc-cn/master/pic/20180421-3.png)

一旦接收到路由记录命令，中继路径上的设备会把它们自己的网络地址附加到路由记录命令的负荷帧的中继列表中。在路由记录命令达到集中器时，它将包含完整的路由路径(数据包中继到集中器所经过的路径)。当集中器将 ACK 发回 R1 时，它应该在数据包的网络层包头中包含源路由(中继列表)。所有接收数据包的设备都应该根据源路由将数据包中继到下一跳设备中。对于没有内存限制的集中器，它可以存储它收到的所有路由记录条目，并使用它们将数据包发送给源设备，所以设备只需要发送一次路由记录命令。但是，对于没有源路由缓存能力的集中器，设备总是需要将路由记录命令随数据包一并发送。集中器会将源路由临时存储在内存中，在使用后丢弃。  

简而言之，当网络中的大多数设备都将流量汇集到单个设备时，多对一路由可以有效地增强常规的 ZigBee 单播路由。作为多对一路由的一部分，源路由仅在某些情况下使用。首先，它在集中器响应源设备发起的请求时使用。其次，如果内存充足，集中器应该存储所有设备的源路由信息。否则，每当设备向集中器发出请求时，它们都需要发送路由记录。

### **5.4.4 多对一路由维护 (Many-to-One Route Maintenance)**

如果在设备转发多对一路由帧时遇到链路故障(请注意，多对一路由帧自身与常规单播数据包没有什么区别，但其路由表条目中有一个字段是用以指向集中器的)，设备将生成一个表示“多对一路由失败(Many-to-one route failure)”的代码的网络状态命令。网络状态命令将通过随机的邻居中继到集中器，并且希望该邻居仍有一个到集中器的有效路由。当集中器收到路由失败时，应用程序将决定是否重新发出多对一路由请求。  

当集中器收到指示多对一路由故障的网络状态命令时，它将指示传递给 ZDO 层，并调用 **ZDApp.c** 中的 ZDO 回调函数：

    void ZDO_ManytoOneFailureIndicationCB()

默认情况下，此函数会重启多对一路由发现以恢复路由。你可以修改这个函数，以适应更复杂的过程。

## **5.5 路由设置快速参考 (Routing Settings Quick Reference)**

 |                        |                                                             |
 | :--------------------- | :---------------------------------------------------------- |
 | 路由表大小(必须大于 4) | 配置 **MAX_RTG_ENTRIES** ，详情参见 5.3.1                   |
 | 路由过期时间           | 配置 **ROUTE_EXPIRY_TIME** ，详情参见 5.2.3                 |
 | 路由发现表大小         | 配置　**MAX_RREQ_ENTRIES** ，详情参见 5.3.2                 |
 | 集中器使能             | 配置 **CONCENTRATOR_ENABLE** ，详情参见 **ZGlobals.h**      |
 | 集中器的路由缓存       | 配置 **CONCENTRATOR_ROUTE_CACHE** ，详情参见 **ZGlobals.h** |
 | 源路由表大小           | 配置 **MAX_RTG_SRC_ENTRIES** ，详情参见 **ZGlobals.h**      |
 | 集中器默认的广播半径   | 配置 **CONCENTRATOR_RADIUS** ，详情参见 **ZGlobals.h**      |

## **5.6 路由器离网关联清理 (Router Off-Network Association Cleanup)**

如果 ZigBee 路由器长时间离网，它的子设备将会尝试加入到另一个父设备下。当路由器重新入网时，其原本的子设备仍然会出现在其子设备表中，这样会阻碍出口流量正确地路由给子设备。  

为了避免这种情况，建议容易离网的并且在网络上的路由器将 **zgRouterOffAssocCleanup** 标记配置成 **TRUE** (映射到 NV 项：**ZCD_NV_ROUTER_OFF_ASSOC_CLEANUP** )

    uint8 cleanupChildTable = TRUE;
    zgSetItem( ZCD_NV_ROUTER_OFF_ASSOC_CLEANUP, sizeof(cleanupChildTable), &cleanupChildTable );

启用后，离网路由器的过期终端设备条目将从其子设备表中被移除(如果原子设备的流量已被其它父设备路由)。

# **6. ZDO 消息请求 (ZDO Message Requests)**

ZDO 模块提供发送 ZDO 服务发现请求消息和接收 ZDO 服务发现响应消息的功能。下面的流程图阐明了功能调用需要发出一个 IEEE 地址请求并接收应用程序的 IEEE 地址响应。

![Figure 4](https://raw.githubusercontent.com/Shanyaoxing12/zigbee-doc-cn/master/pic/20180421-4.png)

在下面的示例中，应用程序想知道(任何)新设备何时加入到网络中。

![Figure 5](https://raw.githubusercontent.com/Shanyaoxing12/zigbee-doc-cn/master/pic/20180421-5.png)

# **7. 便携式设备 (Portable Devices)**

终端设备通过轮询(MAC 数据请求)失败和/或数据消息失败检测到父设备没有响应。失败敏感度(连续错误量)的设置办法为：  

1. 定义一个 **zstack_sysConfigWriteReq_t** 类型变量
2. 通过变量的结构成员 **has_pollFailureRetries = true** 和 **pollFailureRetries**(数值越高 - 敏感度越低，重新加入所需的时间越长) 设置失败次数
3. 将变量传到 **Zstackapi_sysConfigWriteReq()** 中并调用

当网络层检测到终端设备的父设备没有响应时，它会通知应用程序他已经通过 BDB 接口(参阅 15.3)丢弃了它的父设备，然后应用程序负责使用 BDB API **bdb_ZedAttemptRecoverNwk()** (在[1]中描述)去管理设备的重连，这将触发设备启动信道扫描过程以便搜索另一台合适的父设备。建议：一旦终端设备失去其父设备，它应该尝试恢复。如果恢复失败，设备应该在短暂延迟后再次尝试。如果任然失败，则应该在更长的等待期内定期重试。这种做法可以更好地利用电源，并且不会干扰(可能)位于同一信道上的其它网络。  

在安全的网络中，假设设备已经有一个密钥，并且新的密钥没有分发给设备。  

终端设备从旧的父设备下转移到新的父设备下时，短地址会被保留。设备的路由会被自动重新建立。

# **8. 端到端确认 (End-to-end acknowledgements)**

对于非广播消息，基本上有两种类型的信息重试：端到端确认(APS ACK)和单跳确认(MAC ACK)。MAC ACK 始终是默认的，通常足以保证网络具有高度的可靠性。为了提供额外的可靠性，并且为了使发送设备能够确认数据包已经被传送到目标地址，可以使用 APS 确认。  

APS 确认在 APS 层完成的，是一种从目标设备到源设备的确认系统。发送设备将保留消息，直到目标设备发送指示其收到该消息的 APS ACK 消息。这种特性可以通过调用 **AF_DataRequest()** 发送消息时，通过传入的 **options** 字段开启/禁用。 **options** 字段是一个位映射的选项，只需将其与 **AF_ACK_REQUEST** 相或(或运算)就可以开启 APS ACK。重试消息的次数以及重试间的超时时间可以在 **f8wConfig.cfg** 中配置：

* **APSC_MAX_FRAME_RETRIES** 是 APS 层在放弃之前没有收到的 APS ACK 的情况下发送消息的重试次数
* **APSC_ACK_WAIT_DURATION_POLLED** 是重试间的超时时间

# **9. 杂项 (Miscellaneous)**

## **9.1 信道配置 (Configuring channel)**

每个 Z3.0 设备都有一个主通道掩码配置( **BDB_DEFAULT_PRIMARY_CHANNEL_SET** )和一个辅助通道掩码配置( **BDB_DEFAULT_SECONDARY_CHANNEL_SET** )。对于被指示创建网络的具有组网能力的设备，会使用这些通道掩码去扫描具有最少噪声的信道以创建网络。对于被指示加入网络的具有入网能力的设备，会使用这些通道掩码扫描现有的网络以加入网络。设备会首先尝试主通道掩码中定义的所有通道，如果不成功(网络未创建或没有找到加入的网络)，则使用辅助通道掩码。这两个通道掩码可以根据需要通过应用程序配置。将掩码值设置为 0 可以将禁用相应的通道扫描阶段(主要或次要)。主通道掩码默认定义为 **DEFAULT_CHANLIST** (在 **f8wConfig.cfg** 中)，次要通道掩码定义为所有其它通道(即 **DEFAULT_CHANLIST** ^ 0x07FFF800)。第 15 节 提供更多关于启动方法的细节。

## **9.2 PAN ID 配置和加入网络 (Configuring the PAN ID and network to join)**

这是一个可选的配置项，用于控制 ZigBee 路由器或终端设备将加入哪个网络。它也可以用来预先设置协调器或路由器创建的新网络的 PAN ID。 **f8wConfig.cfg** 中的 **ZDO_CONFIG_PAN_ID** 参数可以设置一个值(介于 1 和 0xFFFE 之间)。当指示创建网络时，协调器或组网路由器将使用该值作为网络的 PAN ID。路由器或终端设备将只加入与此参数相匹配的 PAN ID 的网络中。可以将该参数值设置为 0xFFFF 以关闭此功能。关闭此功能的情况下，新创建的网络将具有随机的 PAN ID，并且加入设备将能够加入任何网络，而无需考虑其 PAN ID。  

网络发现过程由网络导向启动过程管理，如 15.5 所述。它允许通过使用 **bdb_RegisterForFilterNwkDescCB()** 函数注册回调来过滤发现的网络，应用程序接收到的网络描述符列表为每次扫描尝试中找到的网络(首先是主要频道，然后是辅助频道)。应用程序可以通过使用 **bdb_nwkDescFree()** 释放网络描述符，跳过尝试去加入特定的网络。有关这些 API 的详细信息，请查阅 [1]。  

为了进一步控制加入的过程，应该在 **ZDApp.c** 中修改 **ZDO_NetworkDiscoveryConfirmCB** 函数。调用 **NLME_NetworkDiscoveryRequest()** 开始，网络层完成网络发现过程时，会调用 **ZDO_NetworkDiscoveryConfirmCB()** 。详细介绍在 Z-Stack API [1] 中。

## **9.3 最大有效载荷大小 (Maximum payload size)**

应用程序的最大有效载荷大小取决于几个因素。MAC 层提供一个恒定的有效载荷长度 116 (可在 **f8wConfig.cfg** 中更改 **MAC_MAX_FRAME_SIZE** )。NWK 层要求有一个固定的头部大小，一个大小是安全的，一个大小是不安全的。APS 层有一个必要的但可变的头部大小，其具体根据各种关联设置(包括 ZigBee 协议版本，APS 帧控制设置等)。最后，用户不必使用上述的说明的因素计算最大有效载荷大小。AF 模块提供了一个 API 允许用户查询堆栈的最大有效载荷大小或最大传输单元(MTU)。用户可以调用 **afDataReqMTU()** (参阅 AF.h)函数，该函数将返回 MTU 或最大有效载荷大小。

    typedef struct
    {
        uint8 kvp;
        APSDE_DataReqMTU_t aps;
    } afDataReqMTU_t;
    uint8 afDataReqMTU( afDataReqMTU_t* fields )

目前，应该在 **afDataReqMTU_t** 结构中设置的唯一字段为 **kvp** ，并且应该将此字段设置为 FALSE。 **aps** 字段保留供以后使用。

## **9.4 离开网络 (Leave Network)**

ZDO 管理实现了提供对  “NLME-LEAVE.request” 进行原始访问的函数 **ZDO_ProcessMgmtLeaveReq()** 。“NLME-LEAVE.request” 允许设备从网络中移除或移除远程设备。 **ZDO_ProcessMgmtLeaveReq()** 根据提供的 IEEE 地址来移除设备。当设备自行移除时，它将等待 **LEAVE_RESET_DELAY** (默认 5 秒)，然后重置。当设备移除子设备时，它也会从本地“关联表”中删除设备。NWK 地址只能在子设备是 ZigBee 终端设备的情况下重新使用。 在子设备是 ZigBee 路由器的情况下，NWK 地址将不会被覆盖使用。  

如果子设备的父设备离开了网络，则子设备将留在网络上。  

在 ZigBee PRO 规范的 R21 版本中，路由器可以配置“NWK 离开请求”的处理。应用程序可以通过设置 **zgNwkLeaveRequestAllowed** 变量的值为 TRUE(默认) 或 FALSE 来控制此功能，以在接收到 “NWK 离开请求”时允许/禁止路由器离开网络。 **zgNwkLeaveRequestAllowed** (在 **ZGlobals.c** 中定义和初始化)， 对应 NV 项 **ZCD_NV_NWK_LEAVE_REQ_ALLOWED** (在 **ZComDef.h** 中定义)。处理这些命令取决于逻辑设备类型的变化：协调器不处理离开命令，路由器处理离开网络中任何设备的命令(如果上述被允许)，并且终端设备仅处理来自其父设备的离开命令。  

在基础设备行为规范中还规定，如果任何设备接收到重新加入设置为 FALSE(意味着该设备不应重新加入网络)的离开请求，则该设备被强制执行恢复出厂设置。在这种情况下，Z-Stack 将清除所有 ZigBee 持久性数据，而 NV 中的相关应用程序数据则由应用程序决定是否清除。

## **9.5 描述符 (Descriptors)**

ZigBee 网路中的所有设备都具有描述设备及其应用类型的描述符。该信息可被网络中的其它设备发现。  

配置项在 **ZDConfig.c** 和 **ZDConfig.h** 中设置和定义。这两个文件还包含节点，功耗描述符和默认用户描述符。确保更改这些描述符来定义您的设备。

## **9.6 非易失性存储项 (Non-Volatile Memory Items)**

### **9.6.1 非易失性存储全局配置 (Global Configuration Non-Volatile Memory)**

全局设备配置项存储在 **ZGlobal.c** 中，这些项包括 PAN ID，密钥信息，网络设置等。大多数这些项的默认值在 **f8wConfig.cfg** 中指定。这些项在启动时加载到 RAM 中，以便在 Z-Stack 操作期间可以快速访问。要初始化非易失性内存区域以存储这些项，必须在项目中启用编译标志 NV_INIT (它在示例应用程序中默认启用)。

### **9.6.2 网络层非易失性存储 (Network Layer Non-Volatile Memory)**

ZigBee 设备有很多状态信息需要存储在非易失性内存中，以便在意外重置或断电时恢复。否则，它将无法重新加入网络或有效运作。  

通过包含 **NV_RESTORE** 编译选项开启此功能，此功能默认启用。此功能必须始终在真正的 ZigBee 网络中启用，禁用功能仅用于开发阶段。  

ZDO 层负责保存和恢复网络层的重要信息，BDB 层定义何时恢复这些信息或何时将设备以“出厂设置状态”启动。这包括网络信息库(NIB - 管理设备网络层所需的属性)；子设备和父设备列表以及包含应用程序绑定的表。这也用于安全地存储帧计数器和密钥。  

设备以任何方式重启，如果设备不打算设置为出厂设置状态，则设备将使用该信息来复原。  

在初始化之后，BDB 层将检查属性 **bdbNodeIsOnANetwork** 以知道这个设备是否被一个网络启动。如果它被一个网络启动，并且它被指示在同一网络中恢复运行，那么 BDB 层将调用 **ZDOInitDeviceEx()** ，它将根据状态和逻辑设备类型来处理恢复的运作。

### **9.6.3 应用非易失性存储 (Application Non-Volatile Memory)**

通常，设备必须启用非易失性内存才能进行认证，因为它必须记住其网络配置。除了堆栈内部数据外， NVM 还可以用于存储应用程序数据。  

要将变量保存到 NVM，必须为该变量创建一个项 ID。为应用程序保留的 ID 范围从 0x0401 到 0x0FFF。有关这些 ID 的完整列表，请参阅 ZComDef.h 文件。  

在项 ID 被第一次选用时，必须使用 **osal_nv_item_init()** 进行初始化。该函数接受项 ID，要存储的变量长度以及初始值。  

要将项写入 NVM，使用 **osal_nv_write()** 。该函数接受项 ID，项的索引偏移量，要写入的数据长度以及要写入的变量。  

要从 NVM 中读取项，使用 **osal_nv_read()** 。该函数接受项 ID，项的索引偏移量，要读取的数据长度以及要读取的变量。  

这些函数可以在 **OSAL_Nv.c** 文件中找到。

## **9.7 异步链接 (Asynchronous Links)**

当一个设备可以从另一个设备接收数据包但它不能将数据包发送到该设备时，会发送异步链接。每当发送这种情况，这个链路就不是路由数据包的好链路。  

在 ZigBee PRO 中，通过使用网络链路状态消息可以解决这个问题。ZigBee PRO 网络中的每个路由器都会发送一个周期性的链路状态消息。该消息是包含发送设备的邻居列表的单跳广播消息。原理是这样的：如果你收到邻居的链路状态，并且你从邻居列表中丢失或者你的接收成本太低(在列表中)，你可以假定你和这个邻居之间的链路是异步链路，你不应该使用它进行路由。  

要更改链接状态消息之间的时间，可以更改编译标志 **NWK_LINK_STATUS_PERIOD** ，该标志用于初始化 **\_NIB.nwkLinkStatusPeriod** 。你可以直接更改 **\_NIB.nwkLinkStatusPeriod** 。请记住，只有 PRO 路由器发送链接状态消息，并且网络中的每个路由器必须具有相同的链接状态时间周期。  

**\_NIB.nwkLinkStatusPeriod** 包含链接状态消息之间的秒数。  

影响链接状态消息的另一个参数是 **\_NIB.nwkRouterAgeLimit** (默认为 **NWK_ROUTE_AGE_LIMIT** )。这表示路由器可以在设备邻居列表中保留的链路状态周期的数量，并且在表中的链路状态未过期前不会从该设备中接收链路状态。如果路由器在( **\_NIB.nwkRouterAgeLimit * \_NIB.nwkLinkStatusPeriod** )内没有收到来自邻居的链接状态消息，它会将邻居过期并假定该设备丢失或是异步链接而不使用它。

## **9.8 多播消息 (Multicast Messages)**

该特性是 ZigBee PRO 的专有特性(必须将 **ZIGBEEPRO** 作为编译标志)。该特性与发送 APS 群组类似，但它是在网络层中。  

多播消息作为 MAC 广播消息从设备发送到组中。接收设备将确定它是否是该组的一部分：如果它不是该组的一部分，则它将递减非成员半径并重播; 如果它是该组的一部分，则它将首先恢复组半径，然后重播该消息。如果半径递减到 0，则消息不会重播。  

多播和 APS 组消息的区别只能在超大型网络中看出，非成员半径将限制群组的跳跃距离。  

**_NIB.nwkUseMultiCast** 被网络层用以使能所有群组消息的多播(如果 **ZIGBEEPRO** 被定义，则会默认为 TRUE)，如果该字段为 FALSE，则 APS 组消息会被当作普通广播网络消息发送。  

**zgApsNonMemberRadius** 是组半径和非成员半径的值。该变量应该由应用程序控制以控制广播的分配。如果该值过高，其效果将与 APS 群组消息相同。该变量在 **ZGlobals.c** 中定义， **ZCD_NV_APS_NONMEMBER_RADIUS** (在 **ZComDef.h** 中定义)是 NV 项。

## **9.9 分片 (Fragmentation)**

消息分片是一个过程：一个过大的 APS 包在被发送时会被分拆成多个较小的分片，并传输。接收设备将分片重组回原本的 APS 包。  

要打开 Z-Stack 项目中的 APS 分片特性，请包含 **ZIGBEE_FRAGMENTATION** 编译标志。默认情况下，定义了 **ZIGBEEPRO** 的所有项目都包含分片特性，不需要单独添加 **ZIGBEE_FRAGMENTATION** 编译标志。所有使用分片的应用程序都将包含 APS 分片任务： **APSF_Init()** 和 **APSF_ProcessEvent()** 。如果你有一个现有的应用程序，请确保代码中的 **OSAL_xxx.c** 文件中包含该头文件：

    #if defined ( ZIGBEE_FRAGMENTATION )
    #include "aps_frag.h"
    #endif

并且 **tasksArr[]** 中有 **APSF_ProcessEvent()** 条目，如下例所示：

    const pTaskEventHandlerFn tasksArr[] = {
        macEventLoop,
        nwk_event_loop,
    #if (ZG_BUILD_RTR_TYPE)
        gp_event_loop,
    #endif
        Hal_ProcessEvent,
    #if defined( MT_TASK )
        MT_ProcessEvent,
    #endif
        APS_event_loop,
    #if defined ( ZIGBEE_FRAGMENTATION )
        APSF_ProcessEvent,
    #endif
        ZDApp_event_loop,
    #if defined ( ZIGBEE_FREQ_AGILITY ) || defined ( ZIGBEE_PANID_CONFLICT )
        ZDNwkMgr_event_loop,
    #endif
        zcl_event_loop,
        bdb_event_loop,
        xxx_ProcessEvent        /* Where xxx is your application’s name */
    };

并且 **osalInitTasks()** 函数中调用了 **APSF_Init()** ，如下例所示：

    void osalInitTasks( void )
    {
        uint8 taskID = 0;
        tasksEvents = (uint16 *)osal_mem_alloc( sizeof( uint16 ) * tasksCnt);
        osal_memset( tasksEvents, 0, (sizeof( uint16 ) * tasksCnt));
        macTaskInit( taskID++ );
        nwk_init( taskID++ );
    #if (ZG_BUILD_RTR_TYPE)
        gp_Init( taskID++ );
    #endif
        Hal_Init( taskID++ );
    #if defined( MT_TASK )
        MT_TaskInit( taskID++ );
    #endif
        APS_Init( taskID++ );
    #if defined ( ZIGBEE_FRAGMENTATION )
        APSF_Init( taskID++ );
    #endif
        ZDApp_Init( taskID++ );
    #if defined ( ZIGBEE_FREQ_AGILITY ) || defined ( ZIGBEE_PANID_CONFLICT )
        ZDNwkMgr_Init( taskID++ );
    #endif
        zcl_Init( taskID++ );
        bdb_Init( taskID++ );
        xxx_Init( taskID );     /* Where xxx is your application’s name */
    }

打开 APS 分片时，发送数据请求的有效载荷大于正常的数据请求的有效载荷时将自动触发分片。  

分片参数位于结构体 **afAPSF_Config_t** 中，该结构体时 **AF.h** 中定义端点描述符列表 **epList_t** 的一部分。调用 **afRegister()** 时，使用这些参数的默认值来注册应用程序的端点描述符，该端点描述符会调用 **afRegisterExtended()** ，默认值 **APSF_DEFAULT_WINDOW_SIZE** 和 **APSF_DEFAULT_INTERFRAME_DELAY** 在 **ZGlobals.h** 中定义：

* **APSF_DEFAULT_WINDOW_SIZE** - 使用分段时的Tx窗口的大小。这是在预期APS分段ACK之前发送的分段数量。因此，如果消息被分解为10个片段，并且最大窗口大小为5，则在接收到5个片段后，接收设备将发送ACK。如果没有收到窗口大小的一个数据包，则不发送ACK，并且重新发送(在该窗口内的)所有数据包。
* **APSF_DEFAULT_INTERFRAME_DELAY** - 窗口内片段之间的延迟。这由发送设备使用。

这些值可以通过分别调用 **afAPSF_ConfigGet()** 和 **afAPSF_ConfigSet()** 来读取和设置。  

建议应用程序/配置文件通过 **ZDConfig.c** 中的 **ZDConfig_UpdateNodeDescriptor()** 更新 ZDO 节点描述符的 **MaxInTransferSize** 和 **MaxOutTransferSize** 。这些字段用 **MAX_TRANSFER_SIZE** (在 **ZDConfig.h** 中定义)初始化。这些值不会在 APS 层中用作最大值，它们只是信息。

### **9.9.1 快速参考 (Quick Reference)**

 |                             |                                                       |
 | :-------------------------- | :---------------------------------------------------- |
 | 编译标志以激活该特性        | ZIGBEE_FRAGMENTATION                                  |
 | 窗口中的最大片段默认值      | APSF_DEFAULT_WINDOW_SIZE (defined in ZGlobals.h)      |
 | 帧间延迟默认值              | APSF_DEFAULT_INTERFRAME_DELAY (defined in ZGlobals.h) |
 | 应用/配置文件最大缓冲区大小 | MAX_TRANSFER_SIZE (defined in ZDConfig.h)             |


## **9.10 扩展的 PAN ID (Extended PAN IDs)**

Z-Stack中有两个扩展的PAN ID：

* **zgApsUseExtendedPANID** ：这是要加入或组建网络的 64-bit PAN 标识符。 对应 **ZCD_NV_APS_USE_EXT_PANID** NV项。
* **zgExtendedPANID** ：这是设备要加入的网络的 64-bit 扩展 PAN ID。如果它的值为 0x0000 0000 0000 0000，那么设备没有连接到网络。对应 **ZCD_NV_EXTENDED_PAN_ID** NV项。

如果设备具有组建能力并且被指示组建网络，则如果 **zgApsUseExtendedPANID** 是非零值时，设备将使用 **zgApsUseExtendedPANID** 组建网络。如果 **zgApsUseExtendedPANID** 是零值，则设备将使用其 64-bit 扩展地址形成网络。

## **9.11 以预启动的网络参数重新加入网络 (Rejoining with Pre-Commissioned Network parameters)**

在之前的 ZigBee 栈中，重新加入设备可能使用预先配置的网络地址。到目前为止，基础设备行为规范并没有解决这个问题(无论是否允许)。TI 鼓励使用第 15 节中介绍的基本设备行为启动方法来重新加入网络。

## **9.12 子管理 (Child management)**

R21(ZigBee 规范修订版 21，AKA ZigBee 2015)引入了子管理特性，旨在允许终端设备的流动性，同时允许父设备从其子设备表中清除过期的子设备。当终端设备加入/重新加入时，它会发送一个 EndDeviceTimeout 网络命令，该命令告诉其父设备后，若在一定周期后设备未发送保持活动消息，则可以将其从关联表中删除。父设备会回答并响应这个网络命令，声明它支持哪些方法接收保持活动信息。在该版本发布时，仅指定了一种保持活动的方法，即标准 MAC 轮询。如果传统设备加入 R21 或更高版本的父设备，则父设备将分配默认超时以在该传统设备无法及时轮询时终止该设备。此外，如果父设备由不是子设备的终端设备轮询(由于过期或根本不是其子设备)，则父设备必须请求该终端设备离开网络并将重入网络设置为 TRUE，这样这个设备就可以重新加入网络并找到一个新的父设备(可能是同一个路由器或另一个)。

### **9.12.1 配置父设备的子管理 (Configuring child management for parent device)**

通过修改 **NWK_END_DEV_TIMEOUT_DEFAULT** ，可以在父设备中定义默认终端设备的超时(对于旧版和 R21 终端设备)。如果终端设备使用 EndDeviceTimeout 命令声明自己的超时时，则该超时将被覆盖。  

父设备必须保持跟踪需要发送离开请求的设备，这些设备可能是过期或由于未知原因轮询父设备的设备。为此，父设备必须将离开请求列队在 mac 层中。 **MAX_NOT_MYCHILD_DEVICES** 定义可以同时保持跟踪的设备数量。将在 **NWK_END_DEVICE_LEAVE_TIMEOUT** 定义的时间段内对设备进行跟踪。所有的这些参数都在 **ZGlobals.h** 中定义。

### **9.12.2 配置子设备的子管理 (Configuring child management for child devices)**

子设备可以向父设备表面其超时，定义为 **END_DEV_TIMEOUT_VALUE** ，并且建议至少比 MAC 轮询的时间大三倍以避免终端设备在轮询时出现干扰而过期。

### **9.12.3 父设备 Annce (Parent Annce)**

子管理功能包括由父设备广播的父设备 Annce ZDO 消息的使用，并且包含父设备的关联表中所有终端设备的 64-bit IEEE 地址。此消息仅在网络组建或重置的 10 秒再加上一个随机抖动后发送。如果此消息由不同的父设备接收，它将检查是否有任何报告的子设备也在其关联表中列出。如果发现任何匹配，则该父设备将回复该消息的发起者，指示哪些子设备不再是其子设备。以下示例可以说明此消息的用法：

1. 父设备'A'有一个子设备'c'
2. 父设备'A'被重新启动
3. 子设备'c'找到父设备'B'并加入它
4. 当父设备'A'恢复其网络参数时，它启动一个定时器以发送父设备 Annce 消息(10 秒加上随机抖动)
5. 然后父设备'A'广播包含子设备'c'的 IEEE 地址的父设备 Annce 消息
6. 父设备'B'发现与其子设备的匹配，并以包含子设备'c'的 IEEE 地址的父设备 Annce 消息来响应
7. 父设备从其表中移除子设备项'c'

# **10. 安全 (Security)**

## **10.1 概述 (Overview)**

ZigBee 的安全性建立在 AES 分组加密和 CCM* 操作模式作为基础安全原语上。AES/CCM* 安全算法由ZigBee联盟以外的外部研究人员开发，也广泛用于其他通信协议。ZigBee 规范基于这些网络使用的安全模式定义了两种类型的网络：集中式安全网络和分布式安全网络。在默认情况下，网络对于新的设备来说是封闭的。在这两种类型的网络中，网络一次只能开放最多 254 秒，之后会封闭起来，不允许加入。Z3.0 网络不能无限期地保持开放。对于哪些设备可以尝试加入网络的持续时间被反映在所有现有的网络响应发送到连接设备的信标请求的信标数据包中。  

ZigBee 提供以下的安全特性：

* 基础架构安全
* 网络访问控制
* 应用数据安全(仅用于集中式安全网络)

## **10.2 配置 (Configuration)**

要使用网络层安全，所有设备的映像构建的时候都必须将预处理标志 **SECURE** 设置为 1。这可以在 **f8wConfig.cfg** 文件中找到，并且在所有的项目中默认是开启的，因为它在 Z3.0 中是强制的。  

用于网络层加密的默认密钥(在 **nwk_globals.c** 中定义的 **defaultKey** )可以在所有加入/组建网络的设备上预先配置，也可以在设备加入网络时通过空中传输分发。这是通过 **ZGlobals.c** 中的 **zgPreConfigKeys** 选项选择的。如果它设置为 TRUE，则每个设备的默认密钥都必须预先配置(完全一致的密钥值)。如果它设置为 FALSE，那么仅需要在组建网络的设备上设置默认密钥参数。该 **defaultKey** 使用 **f8wConfig.cfg** 中的宏定义 **DEFAULT_KEY** 进行初始化。如果它在初始化时设置为 0，则会生成一个随机密钥。在 Z3.0 中，这个密钥通过 APS 层加密，空中传输到加入设备。

## **10.3 集中式安全网络 (Centralized security network)**

这种网络类型由协调器设备组成，其中协调器负责担任信任中心(TC)的角色。在这种类型的网络中，只有信任中心可以分发网络密钥给加入设备并允许它们成为网络的一部分。协调器可以配置不同的信任中心策略以控制网络的安全级别，这些策略将在 10.3.1 节中介绍。当设备直接执行与信任中心的关联时，信任中心会鉴定和验证设备是否允许加入网络。当设备通过路由器设备加入时，其父设备通过 APS 更新设备命令通知信任中心，然后通过相同的信任中心策略验证加入设备。如果设备通过验证，信任中心将通过一个直接的 APS 传输密钥命令或一个 APS Tunnel 将网络密钥发给加入设备：Transport Key 命令取决于设备加入的拓扑结构。如果加入设备没有通过验证，将通过网络离开命令将其踢出网络。  

同样要注意，如果信任中心不可用(开关机循环或不在网络中),新设备将无法加入网络，因为其他设备不允许分发网络密钥或验证信任中心策略。

### **10.3.1 信任中心策略 (Trust center policies)**

#### **10.3.1.1 zgAllowRemoteTCPolicyChange**

如果此策略设置为 TRUE，则网络中的其他设备可以修改信任中心的许可加入策略，从而允许其他设备加入网络。如果设置为FALSE，则远程设备将无法更改协调器上的许可加入策略，这将导致信任中心不分发网络密钥，并且将任何只具有局部许可的设备通过中间路由踢出网络。

#### **10.3.1.2 bdbJoinUsesInstallCodeKey**

如果此策略设置为 TRUE，则网络密钥仅分发给那些具有关联的安装代码的加入设备。如果为 FALSE，则加入的设备可以使用安装代码。10.5.2 节描述了安装代码的用法。

#### **10.3.1.3 bdbTrustCenterRequireKeyExchange**

如果此策略设置为 TRUE(在 **bdb_interface.h** 中默认设置为此值)，则所有加入的设备都必须执行信任中心链接密钥交换过程。在 **bdbTrustCenterNodeJoinTimeout** 秒(默认为 15)后，不执行该过程的设备将被踢出网络。如果为 FALSE，则加入的设备可以不执行该过程，当然也可以执行。该过程在第 10.6.1 节中描述。需要注意的是，传统设备(R20 或之前)将无法执行该过程，因此该策略设置为 TRUE 时，传统设备将无法加入此网络。

### **10.3.2 密钥更新 (Key Updates)**

信任中心可以自行更新通用网络密钥。一种策略是定期更新网络密钥，另一种是在用户输入时(如按下按钮)更新网络密钥。ZDO 安全管理器的 **ZDSecMgr.c** API 通过 **ZDSecMgrUpdateNwkKey()** 和 **ZDSecMgrSwitchNwkKey()** 提供该功能。 **ZDSecMgrUpdateNwkKey()** 允许信任中心将新的网络密钥发送到网络上的 **dstAddr** 。此时，如果 **dstAddr** 不是单播地址，则新的网络密钥将作为备用密钥存储在目标设备(集)中。一旦信任中心使用目标设备(集)的 **dstAddr** 调用 **ZDSecMgrSwitchNwkKey()** ，所有的目标设备(集)将使用其备用密钥。  

在 ZigBee 规范的 R21 修订版中，网络帧计数器要求在出厂新复位时保持不变，但在下列情况下可将其重置为 0：如果网络帧计数器大于其最大值(0x8000000)的一半，在执行网络密钥更新之前，执行更新会将帧计数器重置为 0。

## **10.4 分布式安全网络 (Distributed security network)**

该网络类型可以由具有组网能力的路由器设备组建。在这种网络拓扑中，所有节点都有能力加入网络，并且任何路由器设备都可以将网络密钥分发给加入设备。网络密钥将在 APS 层使用默认的分布式全局密钥进行加密，请参阅第 10.5.3 节。该网络密钥通过 APS 传输密钥命令传递，其中信任中心地址会被设置为 0xFFFF FFFF FFFF FFFF，这将使加入设备知道其在分布式安全网络中。应用程序可以查询 **AIB_apsTrustCenterAddress** 的值以查看是否已加入到分布式网络中。需要注意，在分布式网络组建后，网络密钥不能更新，因为没有定义的方法在该拓扑网络中安全地分发网络密钥。

## **10.5 链接密钥类型 (Link Key types)**

每个节点必须支持一个使用以下链接密钥类型的方法：

1. 默认全局信任中心链接密钥(由 Z-Stack 自动使用)
2. 分布式安全全局链接密钥(由 Z-Stack 自动使用)
3. 安装代码派生的预配置链接密钥(请参阅 Z-Stack API 以启用设置)
4. touchlink 预配置链接密钥(如果启用了 touchlink)

### **10.5.1 默认全局信任中心链接密钥 (Default global Trust Center link key)**

所有设备共享一个默认全局信任中心链接密钥。这是一个 APS 层密钥，并且是加入网络时使用的第一个密钥，如果没有指定其他链接密钥。如果需要与其他 Z3.0 设备的互通，则不能修改此密钥。

    Default global Trust Center link key = 0x5a 0x69 0x67 0x42 0x65 0x65 0x41
    (0:15)                                 0x6c 0x6c 0x69 0x61 0x6e 0x63 0x65
                                           0x30 0x39 

### **10.5.2 安装代码派生的信任中心链接密钥 (Install Code Derived Trust Center Link Key)**

安装代码是一个 16 字节序列，后面跟着 2 个字节的 CRC。生成一个唯一的 TCLK 需要一个完整的 18 字节序列。在 Z3.0 中定义的安装代码的使用被添加到允许一个广义的带外密钥交付方法来进行网络调试。它的工作原理如下：

1. TC 获取安装代码和设备的 64 位 IEEE 地址，该设备将通过任何用户界面(串行、显示和开关等)使用此安装代码来连接。安装代码必须在物理上提供连接设备。
2. TC 验证引入的安装代码的 CRC。如果这是有效的，则将 TCLK 条目与派生密钥和相应设备的地址一起添加到 TC 中。
3. 加入设备被指示使用其安装代码生成相应的 TCLK。
4. 网络以任何方式开放。
5. 加入设备执行关联，信任中心通过安装代码派生的密钥在 APS 层中提供加密的网络密钥。
6. 在此之后，连接设备必须按照BDB规范的要求执行其TCLK的更新。

有关如何生成安装代码的详细信息，请参阅基本设备规范[7]。这只支持 R21 或后来的修订，因此为了允许向后兼容性，应用程序必须有一种不使用安装代码的方法来尝试连接网络。

### **10.5.3 分布式安全全局链接密钥 (Distributed security global link key)**

当设备加入到分布式安全网络(无信任中心)时，网络密钥将由父路由器设备通过分布式安全全局链接密钥在 APS 层加密传递.如果需要与其他 Z3.0 设备的互操作性，则不能修改此密钥。

    Distributed Trust Center link key = 0xd0 0xd1 0xd2 0xd3 0xd4 0xd5 0xd6
    (0:15)                              0xd7 0xd8 0xd9 0xda 0xdb 0xdc 0xdd
                                        0xde 0xdf

### **10.5.4 Touchlink 预配置链接密钥 (Touchlink preconfigured Link Key)**

该密钥用于开发，当一个设备使用 Touchlink 启动程序加入网络时。

    Touchlink preconfigured link key = 0xc0 0xc1 0xc2 0xc3 0xc4 0xc5 0xc6 0xc7
    (0:15)                             0xc8 0xc9 0xca 0xcb 0xcc 0xcd 0xce 0xcf 

## **10.6 非安全入网 (Unsecure join to a network)**

基础设备行为定义了设备通过出厂设置状态启动并加入网络的过程；这个过程涉及到加入设备如何在多个信道中发现可用网络，以及如何回退以发现其余信道中的其他网络，这在 15.5 节中描述。一旦设备选择了合适的网络，加入设备将执行不安全的关联(这个术语是指加入设备没有网络密钥)，加入设备将等待接收网络密钥，加入设备将通过网络密钥确定它是否加入了集中式安全网络或分布式安全网络。这些网络使用不同的密钥来加密包含网络密钥的 APS 传输命令，如上所述。加入这些类型的安全网络的具体安全程序将在以下小节中解释。
