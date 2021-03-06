# 跨阿里云账号迁移RDS实例

数据传输服务DTS（Data Transmission Service）支持将另一个阿里云账号下的RDS实例数据迁移至当前阿里云账号，本文将介绍跨阿里云账号数据迁移配置流程及注意事项。

## 前提条件

目标实例的存储空间需大于源实例的已使用存储空间。

## 费用说明

|迁移类型|链路配置费用|公网流量费用|
|----|------|------|
|结构迁移和全量数据迁移|不收费。|通过公网将数据迁移出阿里云时将收费，详情请参见[产品定价]()。|
|增量数据迁移|收费，详情请参见[产品定价]()。|

## 迁移账号权限要求

|实例类型|结构迁移|全量迁移|增量迁移|
|:---|:---|:---|:---|
|源RDS实例|读写权限|读写权限|读写权限|
|目标RDS实例|读写权限|读写权限|读写权限|

## 准备工作

在源实例所属云账号中配置RAM授权，将目标实例所属云账号作为授信云账号，允许通过数据传输服务访问源实例所属云账号的相关云资源，详情请参见[跨阿里云账号数据迁移或同步时如何配置RAM授权](/intl.zh-CN/RAM授权管理/跨阿里云账号数据迁移或同步时如何配置RAM授权.md)。

## 操作步骤

1.  使用目标RDS MySQL实例所属的阿里云账号登录[数据传输控制台](https://dts-intl.console.aliyun.com/)。
2.  在左侧导航栏，单击**数据迁移**。
3.  在迁移任务列表页面顶部，选择迁移的目标实例所属地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2767559951/p50439.png)

4.  单击页面右上角的**创建迁移任务**。
5.  配置迁移任务的**源库及目标库**信息。

    |配置|说明|
    |--|--|
    |任务名称|DTS会自动生成一个任务名称，建议配置具有业务意义的名称（无唯一性要求），便于后续识别。|
    |源库信息|    -   实例类型：选择**RDS实例**。
    -   实例地区：选择源RDS实例所在地域。

**说明：** 源和目标RDS实例地区可以不同。

    -   在RDS实例ID选择框后方，单击**其他阿里云账号下的RDS实例**。
    -   角色名称：填入源实例所属云账号配置的角色名称，详情请参见[跨阿里云账号数据迁移或同步时如何配置RAM授权](/intl.zh-CN/RAM授权管理/跨阿里云账号数据迁移或同步时如何配置RAM授权.md)。
    -   RDS实例ID：选择源RDS实例的实例ID。
    -   数据库账号：填入源RDS实例数据库的账号，权限要求请参见[迁移账号权限要求](#section_lcj_kcb_mhb)。
    -   数据库密码：填入该数据库账号的密码。 |
    |目标库信息|    -   实例类型：选择**RDS实例**。

**说明：** 目标和源RDS实例地区可以不同。

    -   实例地区：选择目标RDS实例所在地域。
    -   RDS实例ID：选择目标RDS实例的实例ID。
    -   数据库账号：填入目标RDS实例数据库的账号，权限要求请参见[迁移账号权限要求](#section_lcj_kcb_mhb)。
    -   数据库密码：填入该数据库账号的密码。
    -   连接方式：根据需求选择**非加密连接**或**SSL安全连接**，本案例选择**非加密连接**。

**说明：** 选择**SSL安全连接**时，需要提前开启RDS实例的SSL加密功能，详情请参见[设置SSL加密](~~96120~~)。 |

    ![源实例及目标实例配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8897549951/p44991.png)

6.  配置迁移任务的**源库及目标库**信息。

    |配置|说明|
    |:-|:-|
    |任务名称|DTS会自动生成一个任务名称，建议配置具有业务意义的名称（无唯一性要求），便于后续识别。|
    |源实例信息|    1.  在实例ID选择框后方，单击**其他阿里云账号下的RDS实例**。
    2.  配置源实例信息。
        -   实例类型：选择**RDS实例**。
        -   RDS所属阿里云账号ID：填入源实例所属云账号ID。

**说明：** 使用源实例所属的云账号登录[账号管理](https://account.console.aliyun.com/#/secure)页面，即可获取云账号ID。

        -   角色名称：填入源实例所属云账号配置的角色名称，详情请参见[跨阿里云账号数据迁移或同步时如何配置RAM授权](/intl.zh-CN/RAM授权管理/跨阿里云账号数据迁移或同步时如何配置RAM授权.md)。
        -   实例地区：选择源RDS实例所在地域。
        -   RDS实例ID：选择源RDS实例的实例ID。
        -   数据库账号：填入源RDS实例数据库的账号，权限要求请参见[迁移账号权限要求](#section_lcj_kcb_mhb)。
        -   数据库密码：填入该数据库账号的密码。 |
    |目标实例信息|    -   实例类型：选择**RDS实例**。
    -   实例地区：选择目标RDS实例所在地域。
    -   RDS实例ID：选择目标RDS实例的实例ID。
    -   数据库账号：填入目标RDS实例数据库的账号，权限要求请参见[迁移账号权限要求](#section_lcj_kcb_mhb)。
    -   数据库密码：填入该数据库账号的密码。
    -   连接方式：根据需求选择**非加密连接**或**SSL安全连接**，本案例选择**非加密连接**。

**说明：** 选择**SSL安全连接**时，需要提前开启RDS实例的SSL加密功能，详情请参见[设置SSL加密](~~96120~~)。 |

7.  配置完成后，单击页面右下角的**授权白名单并进入下一步**。

    **说明：** 此步骤会将DTS服务器的IP地址自动添加到源RDS实例和目标RDS实例的白名单中，用于保障DTS服务器能够正常连接RDS实例。

8.  选择迁移对象及迁移类型。

    ![选择迁移类型和迁移对象](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4944979951/p47745.png)

    |配置|说明|
    |:-|:-|
    |迁移类型|    -   如果只需要进行全量迁移，则同时勾选**结构迁移**和**全量数据迁移**。
    -   如果需要进行不停机迁移，则同时勾选**结构迁移**、**全量数据迁移**和**增量数据迁移**。
**说明：** 如果没有勾选**增量数据迁移**，为保障数据一致性，数据迁移期间请勿在源库中写入新的数据。 |
    |迁移对象|在迁移对象框中单击待迁移的对象，然后单击![向右小箭头](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8502659951/p40698.png)将其移动至已选择对象框。

**说明：**

    -   迁移对象选择的粒度为库、表、列。若选择的迁移对象为表或列，其他对象（如视图、触发器、存储过程）不会被迁移至目标库。
    -   默认情况下，迁移对象在目标库中的名称与源库保持一致。如果您需要改变迁移对象在目标库中的名称，需要使用对象名映射功能，详情请参见[库表列映射](/intl.zh-CN/数据迁移/迁移任务管理/库表列映射.md)。
    -   如果使用了对象名映射功能，可能会导致依赖这个对象的其他对象迁移失败。 |
    |源、目标库无法连接重试时间|默认重试12小时，您也可以自定义重试时间。如果DTS在设置的时间内重新连接上源、目标库，迁移任务将自动恢复。否则，迁移任务将失败。**说明：** 由于连接重试期间，DTS将收取任务运行费用，建议您根据业务需要自定义重试时间，或者在源和目标库实例释放后尽快释放DTS实例。 |

9.  单击页面右下角的**预检查并启动**。

    **说明：**

    -   在迁移任务正式启动之前，会先进行预检查。只有预检查通过后，才能成功启动迁移任务。
    -   如果预检查失败，单击具体检查项后的![提示](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8502659951/p47468.png)图标，查看失败详情。根据提示修复问题后，重新进行预检查。
10. 预检查通过后，单击**下一步**。
11. 在购买配置确认页面，选择**链路规格**并选中**数据传输（按量付费）服务条款**。
12. 单击**购买并启动**，迁移任务正式开始。
    -   全量数据迁移

        请勿手动结束迁移任务，否则可能导致数据不完整。您只需等待迁移任务完成即可，迁移任务会自动结束。

    -   增量数据迁移

        迁移任务不会自动结束，您需要手动结束迁移任务。

        **说明：** 请选择合适的时间手动结束迁移任务，例如业务低峰期或准备将业务切换至目标实例时。

        1.  观察迁移任务的进度变更为**增量迁移**，并显示为**无延迟**状态时，将源库停写几分钟，此时**增量迁移**的状态可能会显示延迟的时间。
        2.  等待迁移任务的**增量迁移**再次进入**无延迟**状态后，手动结束迁移任务。

            ![无延迟](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6767559951/p47604.png)


