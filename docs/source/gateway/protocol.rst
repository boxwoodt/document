.. _gw_protocol-label:

通讯协议
========================

介绍 TKB-320 双通道网关开发板的通讯协议，包括数据通道协议和远程管理协议，以方便用户通过数据主题下发和接收数据，通过管理主题下发配置信息。

协议格式
++++++++++++++++++++++++++++++++++++

通讯协议采用 MQTT 协议，通过 json 格式数据进行上下行通讯和远程配置。在通讯协议中，MQTT 客户端对网关下发数据到终端是下行通讯，网关转发终端的数据到 MQTT 服务器是上行通讯。支持通过 json 格式数据进行网关信息查询、参数配置和命令执行。远程 MQTT 客户端对网关主动下发命令，网关接收命令后，返回相应的消息。

订阅和发布主题介绍
------------------------------------------------

.. list-table:: 网关上下行数据订阅和发布主题示例
    :widths: 35 45 50
    :header-rows: 0

    * - 数据发布主题
      - 54393131-FF16504E-FFFF770F/msg/up 
      - 网关数据通过 MQTT 服务器转发到应用平台
    * - 数据订阅主题
      - 54393131-FF16504E-FFFF770F/msg/down 
      - 应用平台数据通过 MQTT 服务器转发到网关

.. list-table:: 网关远程管理订阅和发布主题示例
    :widths: 35 45 50
    :header-rows: 0

    * - 管理发布主题
      - 54393131-FF16504E-FFFF770F/mgr/up 
      - 网关管理通过 MQTT 服务器转发到应用平台
    * - 管理订阅主题
      - 54393131-FF16504E-FFFF770F/mgr/down 
      - 应用平台管理通过 MQTT 服务器转发到网关

.. attention:: ``msg`` ， ``up`` ， ``down`` 必须小写。 ``54393131-FF16504E-FFFF770F`` 为网关ID，必须大写。

.. note:: MQTT服务器默认地址为 **amqtt.taolink-tech.com** ，默认端口为 **1883** 。

关键字介绍
------------------------------------------------

在上下行协议中，存在以下关键字：

.. csv-table:: 关键字说明
    :header: "关键字", "类型", "说明"
    :widths: 20 10 40

    "chan", "数字",   "无线模块序号，参数范围 0，1。其中 0表示位号 U9 的无线模块，1表示位号为 U6 的无线模块。"
    "msg",  "字符串", "上下行数据，数据BASE64字符串，base64字符串最大长度为800。"
    "snr",  "数字",   "无线信号信噪比。"
    "rssi", "数字",   "无线信号强度。"

在远程管理协议中，存在以下关键字：

.. csv-table:: 关键字说明
    :header: "关键字", "说明"
    :widths: 20 40

    "get",      "获取参数功能。"
    "set",      "设置参数功能。"
    "run",      "执行命令功能。"
    "version",  "版本信息。"
    "network",  "网络信息。"
    "gateway",  "网关信息。"
    "turmass",  "无线模块。"
    "index",    "消息索引，关联发送和应答消息。"
    "status",   "状态信息，0：表示成功，其他表示失败。"

数据交互
++++++++++++++++++++++++++++++++++++

**数据上行示例**：

.. code-block:: 

    {
        "chan":	1,
        "snr":	18,
        "rssi":	-77,
        "msg":	"MDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBh"
    }

通过 `base64解析`_ ，可以得到原始数据：

.. code-block:: 

    0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a0102030405060708090a

.. _base64解析: https://www.toolhelper.cn/EncodeDecode/Base64


**数据下行示例**：

.. code-block:: 

    {
        "chan": 0,
        "msg": "MDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBhMDEwMjAzMDQwNTA2MDcwODA5MGEwMTAyMDMwNDA1MDYwNzA4MDkwYTAxMDIwMzA0MDUwNjA3MDgwOTBh"
    }

.. note:: 

    - 下发数据可以通过 base64 加密，示例中原始数据与上行示例中原始数据相同。

远程管理功能
++++++++++++++++++++++++++++++++++++

远程管理信息发布的主题为 `54393131-FF16504E-FFFF770F/mgr/up`, 订阅的主题为 `54393131-FF16504E-FFFF770F/mgr/down`. *54393131-FF16504E-FFFF770F* 为网关 ID 。

查询参数
------------------------------------------------

**查询版本信息**

查询网关版本信息，包括 MCU 固件和无线模块固件信息。

.. code-block:: JSON

    {
        "index": 1,
        "get": {
            "version": true
        }
    }

    // 返回信息
    {
        "index": 1,
        "status": 0,
        "get": {
            "version": {
                "mcu": "2.0.11",
                "tur1": "2.0.9",
                "tur2": "2.0.9"
            }
        }
    }

**查询网络信息**

查询网络信息，包括网络模式、本地IP、MQTT服务器地址和端口等信息。

.. code-block:: JSON

    {
        "index": 2,
        "get": {
            "network": true
        }
    }

    // 返回信息
    {
        "index": 2,
        "status": 0,
        "get": {
            "network": {
                "net_mode": "eth",
                "server_ip": "amqtt.taolink-tech.com",
                "server_port": 1883,
                "user_name": "taolink",
                "user_password": "www.taolink-tech.com",
                "dhcp_status": 2,
                "ip_addr": "192.168.100.56",
                "gw_addr": "192.168.100.1",
                "net_mask": "255.255.255.0",
                "dns": "192.168.100.1"
            }
        }
    }

.. note:: 在 dhcp_status 关键字中，0：表示 static ，1：表示 dhcp 。

**查询网关信息**

查询网关ID信息。

.. code-block:: JSON

    {
        "index": 3,
        "get": {
            "gateway": true
        }
    }

    // 返回信息
    {
        "index": 3,
        "status": 0,
        "get": {
            "gateway": {
            "id": "00390038-3430510C-33363230",
            "cun_time": "Thu Sep 26 13:50:24 2024\n",
            "run_time": "0d0h24m"
            }
        }
    }

**查询无线模块信息**

查询无线模块时隙等信息，时隙参数以下列顺序排列："数据类型", "时隙状态", "频点", "发送功率", "速率模式", "字节长度", "时间长度"。

.. code-block:: JSON

    {
        "index": 4,
        "get": {
            "turmass": {
                "chan": 0,
                "begin": 0,
                "number": 30
            }
        }
    }

    // 返回信息
    {
        "index": 4,
        "get": {
            "turmass": {
                "chan": 0,
                "begin": 0,
                "number": 30,
                "init": "0,0,202,1,6,1,3",
                "slot": "0,0,489200000,20,11,0,01,0,489200000,20,11,72,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,01,1,489200000,20,18,256,01,0,489200000,20,18,74,0"
            }
        }
    }

.. note:: 
    - *chan* 表示通道序号。
    - *begin* 表示起始时隙序号。
    - *number* 表示时隙数量，不超过 30 个。
    - *init* 表示无线模块初始化信息。
    - *slot* 表示时隙配置信息。

设置参数
------------------------------------------------

设置无线模块时隙等信息。

.. code-block:: JSON

    {
        "index": 5,
        "set": {
            "turmass": {
            "chan": 0,
            "begin": 0,
            "number": 5,
            "init": "0,0,5,1,6,1,3",
            "slot": "0,0,474200000,20,10,0,0;1,0,474200000,20,10,120,0;1,1,473200000,20,10,120,0;1,0,473200000,20,10,120,0;1,1,473200000,20,10,120,0"
            }
        }
    }

    // 返回信息
    {
        "index": 5,
        "status": 0
    }

.. note:: 
    - *chan* 表示通道序号。
    - *begin* 表示起始时隙序号。
    - *number* 表示时隙数量，不超过 30 个。
    - *init* 表示无线模块初始化信息。
    - *slot* 表示时隙配置信息。

网关重启
------------------------------------------------

用于远程重启网关。

.. code-block:: JSON

    {
        "index": 6,
        "run": {
            "restart": true
        }
    }

    // 返回信息
    {
        "index": 6,
        "status": 0
    }


网关升级
------------------------------------------------

网关固件升级。

.. code-block:: JSON

    {
        "index": 7,
        "run": {
            "mcu_upgrade": "http://download.taolink-tech.com:11280/alpha/slip/TKB-320_V2.0.2_High.rbl"
        }
    }

    // 返回信息
    {
        "index": 7,
        "status": 0
    }

无线模块升级
------------------------------------------------

无线模块固件升级。

.. code-block:: JSON

    {
        "index": 4,
        "run": {
            "tur1_upgrade": {
                "flag": 0,
                "url" : "http://download.taolink-tech.com:11280/alpha/slip/phy_slip.bin"
            }
        }
    }

    // 返回信息
    {
        "index": 4,
        "status": 0
    }

.. important::
    - tur1_upgrade：表示无线模块 1 的升级。
    - tur2_upgrade：表示无线模块 2 的升级。

.. note:: 
    - *flag* 表示擦除模块参数标志，0：表示不擦除，1：表示擦除。
    - *url* 表示升级文件地址。

网关上行通知
------------------------------------------------

当网关上线后，主动发布消息，通知服务器。

.. code-block:: JSON

    {
        "state": "online"
    }

网关离线通知
------------------------------------------------

当网关离线后，MQTT 服务器通过遗嘱主题通知订阅者。

.. code-block:: JSON

    {
        "state": "offline"
    }

