 ***Z-Stack 应用程序接口 (Z-Stack API)*** 
 =========================================================


 | 版本 | 描述                                                                                        | 日期       |
 | :--- | :------------------------------------------------------------------------------------------ | :--------- |
 | 1.0  | 首次发行                                                                                    | 2006/12/11 |
 | 1.1  | 添加 ZDO 设备网络启动                                                                       | 2007/03/07 |
 | 1.2  | 更改 ZDO 接口                                                                               | 2007/08/07 |
 | 1.3  | 添加频率捷变和 PAN ID 冲突接口                                                              | 2007/12/18 |
 | 1.4  | 添加多对一路由                                                                              | 2008/01/23 |
 | 1.5  | 添加 Inter-PAN 传输                                                                         | 2008/04/09 |
 | 1.6  | 添加 afIncomingMSGPacket_t的接收数据描述                                                    | 2009/03/19 |
 | 1.7  | 更新 APIs                                                                                   | 2009/03/30 |
 | 1.8  | 确定 ZMacSetTransmitPower()，添加 ZMacLqiAdjustMode()                                       | 2010/07/25 |
 | 1.9  | 确定 StubAPS_RegisterApp() 原型描述，更新缩写；添加 afAPSF_ConfigGet() & afAPSF_ConfigSet() | 2011/05/31 |
 | 1.10 | 在 AF_DataRequest() 中添加 AF_SUPRESS_ROUTE_DISC_NETWORK 选项字段                           | 2012/10/19 |
 | 1.11 | 包含 Z3.0 API；添加 BDB 部分及其函数；添加 GP 部分及其存根(stubs)的接口                     | 2016/11/15 |
 | 1.12 | 添加 bdb_StopInitiatorFindingBinding 到 BDB 接口                                            | 2017/05/10 |



# **1. 引言(Introduction)**



# **2. 层次概述(Layer Overview)**

本节概述本文中涉及的各个层。

## **2.1 BDB(基本设备行为)**

基础设备行为层指定在 ZigBee-PRO 栈上运行的基础设备的 environment（环境）、initialization（初始化）、commissioning 和 operating procedures（操作过程），以确保 profile（配置文件）的互操作性。Z-Stack BDB 提供了数据结构和接口，应用开发者需要遵守其规范。它还为应用程序提供了一个 reporting attributes（报告属性）的通用实现，其支持 reportable
attributes（可报告属性）的 clusters（群集）。

ps：带括号解释的词语在后文将只使用英文表达以确保其准确性，此处使用括号解释是为了提供一个大概的意思。后文可能出现同样的情况，如无特殊说明，一般与此处性质一致。

## **2.2 ZDO(ZigBee 设备对象)**

ZigBee 设备对象层提供管理 ZigBee 设备的功能。ZDO API 为应用程序 endpoints（端点）提供了接口，以管理 ZigBee Coordinators（协调器）、Routers（路由器）或 End Devices（终端设备）的功能，包括：创建、发现和连接 ZigBee 网络；绑定应用程序 endpoints；安全管理。

## **2.3 AF(应用程序框架)**

应用程序框架接口支持底层栈的 Endpoints（包括ZDO）接口。Z-Stack AF 提供了数据结构和帮助函数，开发者需要构建一个 device
description （设备描述符），并且其是用于传入消息的 endpoint multiplexor（端点多路复用器）。

## **2.4 APS(应用支持子层)**

应用支持子层 API 提供了一套通用的支持服务，这些服务用在 ZDO 和制造商定义的应用程序对象上。

## **2.5 NWK(网络层)**

ZigBee网络层为 higher layer（高层）组件提供管理和数据服务。

## **2.6 Green Power(绿色能源)**

绿色能源层数据服务允许 higher layer 发送或接收来自 Green Power stubs（存根）的数据。这些 stubs 用于与 commissioning 或在网络中正常运行的绿色能源设备进行交互。

## **2.7 ZMAC(ZigBee 物理层)**

ZMAC 层提供 802.15.4 MAC 和 ZigBee NWK 层之间的接口。



# **3. 应用程序接口(Application Programming Interface)**

本节提供了 Z-Stack 中实现的常用数据结构的概要，以及用于访问指定层提供的关键功能的 API。

## **3.1 基础设备行为(BDB)**

本节列举了 BDB 层提供的所有功能函数的调用，其是实现 BDB 中定义的所有 commands（命令）和 responses（响应）所必需的，以及确保不同 ZigBee 设备之间的互操作性的功能。所有的 BDB API 函数按照常规和安全配置函数以及可由应用程序在运行时调用的函数进行分类。每个类别在下面的小节中讨论。

### **3.1.1 概述(Overview)**

BDB 描述了一般的 ZigBee 设备将如何进入并在 ZigBee 网络中运行，且确保设备间的 profile 的互操作性。更具体地说，BDB 规范定义了以下的功能：

* 初始化程序（The initialization procedures）
* commissioning 程序（The commissioning procedures）
* 复位程序（The reset procedures）
* 安全程序（The security procedures）
* 报告属性（Reporting attributes）

所有的这些程序都是通过使用 ZDO、ZCL、NWK 和 APS 等层的现有的 API 来执行的。

### **3.1.2 BDB 在网络上的一般配置和使用(BDB General Configuration and usage on a network)**

所有的 BDB API 都包含在 **bdb_interface.h** 这个头文件中。基于 BDB 功能和在头文件中定义的方法，此 API 函数在以下小节中提供：

* 应用程序必须使用以配置 BDB 参数的函数
* 应用程序使用以配置 BDB 的 security- specific 参数的函数
* 应用程序在启动 BDB Commission 后和在应用程序运行时调用的函数
* BDB 提供的用在 BDB Commissioning procedure 某一部分的以通知事件或执行自定义应用程序代码的回调函数

#### **3.1.2.1 bdb_SetIdentifyActiveEndpoint()**

设置将执行查找和绑定的 endpoint（目标或发起者）。

    // @ Param：
    //   activeEndpoint - 用以执行查找和绑定的活动 endpoint
    //                    如果设置为 0xFF，将尝试所有带有 Identify（标识）的应用程序 endpoints
    // @ Return：(ZStatus_t)
    //   ZComDef.h 中 ZStatus_t 定义的状态值
    ZStatus_t bdb_SetIdentifyActiveEndpoint( uint8 activeEndpoint );

#### **3.1.2.2 bdb_setChannelAttribute()**

设置发现或构建程序的主要或次要信道。默认情况下，主要信道设置为 DEFAULT_CHANLIST，次要信道设置为(DEFAULT_CHANLIST ^ 0x07FFF800)。

    // @ Param：
    //   isPrimaryChannel – True 为设置主信道， False 为设置次信道
    //   channel – 包含用于扫描此请求的信道的位掩码。信道的定义包含在 f8wConfig.cfg 中
    // @ Return：
    //   None
    void bdb_setChannelAttribute( bool isPrimaryChannel, uint32 channel );

#### **3.1.2.3 bdb_RegisterIdentifyTimeChangeCB()**

注册应用程序的 Identify Time change 回调函数，以便在 identify 激活或不激活时让它告知应用程序。

    // @ Param：
    //   pfnIdentifyTimeChange – 当 identify 激活或不激活时，用以告知应用程序的应用程序回调函数
    // @ Return：
    //   None
    void bdb_RegisterIdentifyTimeChangeCB( bdbGCB_IdentifyTimeChange_t pfnIdentifyTimeChange );

#### **3.1.2.4 bdb_RegisterBindNotificationCB()**

注册应用程序的通知回调函数，以便当有新绑定添加到绑定表时，告知应用程序。该回调将包括创建绑定的远程设备的地址、应用程序 endpoint 和 cluster。

    // @ Param：
    //   pfnBindNotification – 当一个新绑定添加到绑定表时，用以告知应用程序的应用程序回调函数
    // @ Return：
    //   None
    void bdb_RegisterBindNotificationCB( bdbGCB_BindNotification_t pfnBindNotification );

#### **3.1.2.5 bdb_RegisterCommissioningStatusCB()**

注册回调，其将报告 BDB commissioning 过程中的程序状态。它还会尝试报告剩下的 commissioning 模式。

    // @ Param：
    //   bdbGCB_CommissioningStatus – 应用程序回调函数，其将报告 BDB commissioning 过程中的程序状态
    // @ Return：
    //   None
    void bdb_RegisterCommissioningStatusCB( bdbGCB_CommissioningStatus_t bdbGCB_CommissioningStatus );

#### **3.1.2.6 bdb_setCommissioningGroupID()**

通过随后调用查找&绑定 commissioning 方法作为发起者，设置将添加到匹配 clusters 的组 ID。

    // @ Param：
    //   groupID – Commissioning 将添加到匹配 clusters 的组 ID。如果设置为 0xFFFF（默认），那么查找&绑定不使用组
    // @ Return：
    //   None
    void bdb_setCommissioningGroupID( uint16 groupID );

#### **3.1.2.7 bdb_RepAddAttrCfgRecordDefaultToList()**

为 Reportable Attribute 添加默认配置值。当为指定的一对 Cluster-Endpoint 中的 attribute 创建绑定时，将使用此配置。如果没有为 reportable attribute 定义配置，那么将使用默认配置，该配置可以在 **bdb_interface.h** 中定义。栈默认将该 attribute 设置为不定期 reporting。

    // @ Param：
    //   endpoint – Reportable Attribute 记录的 endpoint ID，以配置其默认值
    //   cluster – Reportable Attribute 记录的 cluster ID，以配置其默认值
    //   attrID – Reportable Attribute 记录的 attribute ID，以配置其默认值
    //   minReportInt – Reportable Attribute 记录的最小 reportable 间隔默认值
    //   maxReportInt – Reportable Attribute 记录的最大 reportable 间隔默认值
    //   reportableChange – 包含 attribute 值缓冲区，其将是触发 report 所需的增量变化
    // @ Return：(ZStatus_t)
    //   ZInvalidParameter - 在应用程序定义的简单描述符中找不到给定的 endpoint、cluster 和 attrID
    //   ZFailure - 没有内存分配条目
    //   ZSuccess - 默认条目保存成功
    ZStatus_t bdb_RepAddAttrCfgRecordDefaultToList( uint8 endpoint, uint16 cluster, uint16 attrID,
                                                    uint16 minReportInt, uint16 maxReportInt, 
                                                    uint8* reportableChange );

#### **3.1.2.8 bdb_RegisterForFilterNwkDesc()**

注册回调，其应用程序从主动扫描中获得网络描述符列表。使用 bdb_nwkDescFree 释放不感兴趣的网络描述符，并保留要尝试连接的网络描述符。例如过滤网络中与制造商不匹配的扩展 PAN ID。

    // @ Param：
    //   bdbGCB_FilterNwkDesc – 应用程序回调函数，其获取从主动扫描获取的网络描述符列表
    // @ Return：
    //   None
    void bdb_RegisterForFilterNwkDesc( bdbGCB_FilterNwkDesc_t bdbGCB_FilterNwkDesc );

#### **3.1.2.9 bdb_TouchlinkSetAllowStealing()**

常规函数：当执行 Touchlink 作为目标时，允许其抢断。

    // @ Param：
    //   allow – 允许为 TRUE，否则为 FALSE
    // @ Return：
    //   None
    void bdb_TouchlinkSetAllowStealing( bool allow );

#### **3.1.2.10 bdb_RegisterTouchlinkTargetEnableCB()**

注册应用程序的 使能/禁用 回调函数。参考 touchLinkTarget_EnableCommissioning 以 使能/禁用 TL 作为目标。

    // @ Param：
    //   pfnTargetEnableChange – 当 使能/禁用 TL 作为目标时，Touchlink 过程调用的回调函数
    // @ Return：
    //   None
    void bdb_RegisterTouchlinkTargetEnableCB( tlGCB_TargetEnable_t pfnTargetEnableChange );

### **3.1.3 BDB 安全配置(BDB Security Configuration)**

本节中定义了用以配置加入设备和 Trust Center（信任中心）所使用的安全参数（例如：设置安装代码、信任中心策略或验证安装代码）的 API。

#### **3.1.3.1 bdb_GenerateInstallCodeCRC()**

这是一个通用函数，用于计算传递的安装代码的 CRC 值。这意味着它被用于调试 和/或 验证通过制造商制定方法引入设备的 CRC。

    // @ Param：
    //   installCode – 大小为 16 字节的缓冲区，其中需包含将生成 CRC 的安装代码
    // @ Return：(uint16)
    //   CRC - 从引入的安装代码所生成的 CRC
    uint16 bdb_GenerateInstallCodeCRC( uint8 *installCode );

#### **3.1.3.2 bdb_setJoinUsesInstallCodeKey()**

该函数设置在 BDB 规范中定义的 BDB attribute：bdbJoinUsesInstallCodeKey。其仅用于 Trust Center 设备。

    // @ Param：
    //   set – 如果为 TRUE，则设备只能通过 TC 注册的安装代码入网；否则设备可以或不使用安装代码入网
    // @ Return：
    //   None
    void bdb_setJoinUsesInstallCodeKey( bool set );

#### **3.1.3.3 bdb_setTCRequireKeyExchange()**

设置 bdb_setTCRequireKeyExchange attribute，此设置可用于控制是否允许 legacy 设备（Zigbee PRO R20 之前）连接到网络。仅用于 TC 设备。

    // @ Param：
    //   isKeyExchangeRequired – 如果为 True，TC 将移除在 bdbTrustCenterNodeJoinTimeout 之后不执行密钥交换的设备；否则不移除。
    // @ Return：
    //   None
    void bdb_setTCRequireKeyExchange( bool isKeyExchangeRequired );

#### **3.1.3.4 bdb_addInstallCode()**

该函数允许 TC 为特定的加入设备添加一个预配值的密钥。密钥的格式通过编译标志 BDB_INSTALL_CODE_USE 定义，其定义了安装代码是 16 字节的安装代码加 2 字节的 CRC 还是 16 字节的纯文本密钥。这仅用于 TC 设备，加入设备必须参考 3.1.3.6 小节的 bdb_setActiveCentralizedLinkKey()。

    // @ Param：
    //   pInstallCode – 数组缓冲区，以包含 安装代码/纯文本 格式的安装代码
    //   pExt - 与安装代码相关联的扩展地址
    // @ Return：(ZStatus_t)
    //   ZInvalidParameter - pInstallCode 或 pExt 为空，或 CRC 错误
    //   ZSuccess -  正确地添加 APS TC 链接密钥
    //   ZApsTableFull - APS TC 链接密钥已满
    ZStatus_t bdb_addInstallCode( uint8* pInstallCode, uint8* pExt );

#### **3.1.3.5 bdb_RegisterTCLinkKeyExchangeProcessCB()**

注册一个回调以接收连接设备上的通知和它在 TC 链接密钥交换中状态。

    // @ Param：
    //   bdbGCB_TCLinkKeyExchangeProcess – 应用程序回调函数，以接收连接设备上的通知和它在 TC 链接密钥交换中状态
    // @ Return：
    //   None
    void bdb_RegisterTCLinkKeyExchangeProcessCB( bdbGCB_TCLinkKeyExchangeProcess_t bdbGCB_TCLinkKeyExchangeProcess );

#### **3.1.3.6 bdb_setActiveCentralizedLinkKey()**

该函数设置被使用的活跃集中式密钥，全局的或安装代码派生的。密钥的格式通过编译标志 BDB_INSTALL_CODE_USE 定义，其定义了安装代码是 16 字节的安装代码加 2 字节的 CRC 还是 16 字节的纯文本密钥。仅用于 TC 设备。

    // @ Param：
    //   useGlobal – 如果为 TRUE，使用默认的 TC 链接密钥；否则，使用 pBuf 作为 安装代码密钥派生输入的源
    //   pBuf - 数组缓冲区，以包含 安装代码/纯文本 格式的安装代码
    // @ Return：(ZStatus_t)
    //   ZFailure - BDB_INSTALL_CODE_USE 无效时
    //   ZInvalidParameter - 安装代码缓存区为空时
    ZStatus_t bdb_setActiveCentralizedLinkKey( bool useGlobal, uint8* pBuf );

#### **3.1.3.7 bdb_RegisterCBKETCLinkKeyExchangeCB()**

注册一个回调，在该回调中，应用程序将执行TC链接密钥交换过程。该运行结果必须通过使用 bdb_CBKETCLinkKeyExchangeAttempt 接口来通知。如果未注册回调，或 TC 链接密钥交换过程被报告为失败，则将执行常规的 TC 链接密钥交换过程。

    // @ Param：
    //   bdbGCB_CBKETCLinkKeyExchange – 应用程序回调函数，以执行 TC 链接密钥交换
    // @ Return：
    //   None
    void bdb_RegisterCBKETCLinkKeyExchangeCB( bdbGCB_CBKETCLinkKeyExchange_t bdbGCB_CBKETCLinkKeyExchange );

