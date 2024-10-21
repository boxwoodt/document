.. _shell_cmd-label:

shell命令
===================================

shell指令是一套供用户在命令行调用的操作接口，主要用于调试和查看系统信息。它通过串口与PC机通信。

**串口配置**

- 波特率：921600
- 数据位：8
- 停止位：1
- 奇偶校验：无

Tk86xxGwGetBootMode
***********************************

- **功能描述**

用于获取启动模式。包括正常启动，GPIO唤醒，定时唤醒，无线唤醒。

.. note:: 0-正常启动，1-GPIO 唤醒，2-定时唤醒，3-无线唤醒

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1"
    :widths: 30 30

    "Tk86xxGwGetBootMode", "通道索引 [1]_"

.. [1] 通道索引：范围0~1

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwGetBootMode 0

    输出:
    Tk86xxGwGetBootMode 0
    Tk86xxGwGetBootMode:
    argv[0]: Tk86xxGwGetBootMode
    argv[1]: 0
    shell_Tk86xxGwGetBootMode: success
    bootMode: 0
    tshell>
    tshell>

Tk86xxGwInit
***********************************

- **功能描述**

用于PHY初始化。设置设备模式、时隙周期参数、中断配置等信息。

- **参数解释**

.. csv-table:: 
    :header-rows: 0
    :header: "命令", "参数1", "参数2", "参数3", "参数4", "参数5", "参数6", "参数7", "参数8"
    :widths: 30 30 30 30 30 30 30 30 30

    "Tk86xxGwInit", "通道索引 [1]_", "设备模式 [2]_", "时隙周期 [3]_", "时隙数", "中断掩码 [4]_", "引脚序号 [5]_", "触发类型 [6]_", "可选字段开关 [7]_"

.. [2] 设备模式：0-同步模式，1-异步模式
.. [3] 时隙周期：运行N个时隙周期后停止，0 表示不停止。
.. [4] 中断掩码：0-只开第一时隙中断，1-只开最后时隙中断，2-打开所有时隙中断
.. [5] 引脚序号：0-GPIO0，3-GPIO3
.. [6] 触发类型：0-下降沿，1-上升沿。持续1.8微秒
.. [7] 可选字段开关：Bit0-包长字段开关，Bit1-CRC16校验，其他保留

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwInit 0 0 0 3 0 0 1 0

    输出:
    Tk86xxGwInit 0 0 0 3 0 0 1 0
    Tk86xxGwInit:
    argv[0]: Tk86xxGwInit
    argv[1]: 0
    argv[2]: 0
    argv[3]: 0
    argv[4]: 3
    argv[5]: 0
    argv[6]: 0
    argv[7]: 1
    argv[8]: 0
    shell_Tk86xxGwInit: success
    tshell>
    tshell>

Tk86xxGwSetSlot
***********************************

- **功能描述**

用于设置时隙参数。包括时隙类型、时隙状态、频点、发射功率、速率模式、时隙长度。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1", "参数2", "参数3", "参数4"
    :widths: 30 30 30 30 30

    "Tk86xxGwSetSlot", "通道索引 [1]_", "起始时隙索引", "时隙数量", "`时隙配置信息`_"

.. note:: 
    :name: 时隙配置信息

    每个时隙配置需要7个参数，参数间使用 ``,`` 分隔，时隙间使用 ``;`` 分隔。时隙参数以下列顺序配置：
    "数据类型", "时隙状态", "频点", "发送功率", "速率模式", "字节长度", "时间长度"。

    - **数据类型**: 0-BCN，1-DATA 
    - **时隙状态**: 0-TX，1-RX，2-IDLE
    - **频点**: 470MHz~510MHz
    - **发送功率**: -40~20dBm
    - **速率模式**: 4~11、18、24
    - **字节长度**: DATA类型的字节数，BCN类型时字节数只能是0或者1，单位Byte
    - **时间长度**: 空闲时隙的时间长度，其他模式下无效，单位微秒


- **示例**

.. code-block:: 

    输入:
    Tk86xxGwSetSlot 0 0 3 0,0,473200000,20,11,0,0;1,0,473200000,20,11,200,0;1,1,473200000,20,11,10,0

    输出:
    Tk86xxGwSetSlot 0 0 3 0,0,473200000,20,11,0,0;1,0,473200000,20,11,200,0;1,1,473200000,20,11,10,0
    TK86xxGwSetSlot:
    argv[0]: Tk86xxGwSetSlot
    argv[1]: 0
    argv[2]: 0
    argv[3]: 3
    argv[4]: 0,0,473200000,20,11,0,0;1,0,473200000,20,11,200,0;1,1,473200000,20,11,10,0
    shell_Tk86xxGwSetSlot: success
    tshell>
    tshell>

Tk86xxGwGetChipInfo
***********************************

- **功能描述**

用于获取芯片信息。包括芯片版本号、芯片ID、SDK版本号、Flash大小。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1"
    :widths: 30 30

    "Tk86xxGwGetChipInfo", "通道索引 [1]_"

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwGetChipInfo 0

    输出:
    Tk86xxGwGetChipInfo 0
    Tk86xxGwGetChipInfo:
    argv[0]: Tk86xxGwGetChipInfo
    argv[1]: 0
    shell_Tk86xxGwGetChipInfo: success
    chipInfo.chipVer  : 96
    chipInfo.chipId   : 20293
    chipInfo.sdkVer   : 2.0.1
    chipInfo.flashSize: 512
    tshell>
    tshell>

Tk86xxGwGetVolt
***********************************

- **功能描述**

用于获取电压信息。单位为0.1V。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1"
    :widths: 30 30

    "Tk86xxGwGetVolt", "通道索引 [1]_"

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwGetVolt 0

    输出:
    Tk86xxGwGetVolt 0
    Tk86xxGwGetVolt:
    argv[0]: Tk86xxGwGetVolt
    argv[1]: 0
    shell_Tk86xxGwGetVolt: success
    Volt  : 33
    tshell>
    tshell>

Tk86xxGwGetTemp
***********************************

- **功能描述**

用于获取温度信息。单位为℃。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1"
    :widths: 30 30

    "Tk86xxGwGetTemp", "通道索引 [1]_"

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwGetTemp 0

    输出:
    Tk86xxGwGetTemp 0
    Tk86xxGwGetTemp:
    argv[0]: Tk86xxGwGetTemp
    argv[1]: 0
    shell_Tk86xxGwGetTemp: success
    Temp  : 28
    tshell>
    tshell>

Tk86xxGwOpenRadio
***********************************

- **功能描述**

用于打开射频开关。调用Tk86xxSetSlot设置时隙后，均需要打开射频开关。如果是再次打开射频开关，调用前需先调用关闭射频开关。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1"
    :widths: 30 30

    "Tk86xxGwOpenRadio", "通道索引 [1]_"

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwOpenRadio 0

    输出:
    Tk86xxGwOpenRadio 0
    Tk86xxGwOpenRadio:
    argv[0]: Tk86xxGwOpenRadio
    argv[1]: 0
    shell_Tk86xxGwOpenRadio: success
    tshell>
    tshell>


Tk86xxGwCloseRadio
***********************************

- **功能描述**

用于关闭射频开关。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1"
    :widths: 30 30

    "Tk86xxGwCloseRadio", "通道索引 [1]_"

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwCloseRadio 0

    输出:
    Tk86xxGwCloseRadio 0
    Tk86xxGwCloseRadio:
    argv[0]: Tk86xxGwCloseRadio
    argv[1]: 0
    shell_Tk86xxGwCloseRadio: success
    tshell>
    tshell>

Tk86xxGwSendData
***********************************

- **功能描述**

用于发送数据。当数据长度低于时隙长度时，通过自动补零方式使数据长度与时隙长度相等。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1", "参数2", "参数3"
    :widths: 30 30 30 30

    "Tk86xxGwSendData", "通道索引 [1]_", "指定发送时隙", "发送数据"

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwSendData 0 0 12345678

    输出:
    Tk86xxGwSendData 0 0 12345678
    Tk86xxGwSendData:
    argv[0]: Tk86xxGwSendData
    argv[1]: 0
    argv[2]: 0
    argv[3]: 12345678
    shell_Tk86xxGwSendData: success
    tshell>
    tshell>

Tk86xxGwSendBcnData
***********************************

- **功能描述**

用于发送BCN的负载数据。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1", "参数2", "参数3"
    :widths: 30 30 30 30

    "Tk86xxGwSendBcnData", "通道索引 [1]_", "时隙索引", "BCN数据"

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwSendBcnData 0 1 1

    输出:
    Tk86xxGwSendBcnData 0 1 1
    Tk86xxGwSendBcnData:
    argv[0]: Tk86xxGwSendBcnData
    argv[1]: 0
    argv[2]: 1
    argv[3]: 1
    shell_Tk86xxGwSendBcnData: success
    tshell>
    tshell>

Tk86xxGwWakeUp
***********************************

- **功能描述**

用于设置唤醒参数并发送唤醒信号。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1", "参数2", "参数3", "参数4", "参数5"
    :widths: 30 30 30 30 30 30

    "Tk86xxGwWakeUp", "通道索引 [1]_", "唤醒类型 [8]_", "唤醒ID [9]_", "唤醒频点 [10]_", "唤醒周期 [11]_"

.. [8] 唤醒类型：取值范围1-4
.. [9] 唤醒ID：取值范围0~127
.. [10] 唤醒频点：取值范围470000000~510000000，单位Hz
.. [11] 唤醒周期：取值范围1ms~24h，单位ms

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwWakeUp 0 4 1 473200000 1000

    输出:
    Tk86xxGwWakeUp 0 4 1 473200000 1000
    Tk86xxGwWakeUp:
    argv[0]: Tk86xxGwWakeUp
    argv[1]: 0
    argv[2]: 4
    argv[3]: 1
    argv[4]: 473200000
    argv[5]: 1000
    shell_Tk86xxGwWakeUp: success
    tshell>
    tshell>status.slotPeriodCnt: 1
    status.slotIdx      : 0
    status.slotIrq      : 3


Tk86xxGwScanChan
***********************************

- **功能描述**

用于侦听信道。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1", "参数2", "参数3", "参数4"
    :widths: 30 30 30 30 30

    "Tk86xxGwScanChan", "通道索引 [1]_", "频点", "扫描模式 [12]_", "扫描带宽 [13]_"

.. [12] 扫描模式：4-单次采样时间8ms，检测边界-112dbm
.. [13] 扫描带宽：0-检测带宽64K，1-检测带宽128K，2-检测带宽256K

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwScanChan 0 473000000 4 2

    输出:
    Tk86xxGwScanChan 0 473000000 4 2
    Tk86xxGwScanChan:
    argv[0]: Tk86xxGwScanChan
    argv[1]: 0
    argv[2]: 473000000
    argv[3]: 4
    argv[4]: 2
    shell_Tk86xxGwScanChan: success
    Rssi  : -106
    tshell>
    tshell>

Tk86xxGwGetSignalQuality
***********************************

- **功能描述**

用于获取当前信号质量。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1"
    :widths: 30 30

    "Tk86xxGwGetSignalQuality", "通道索引 [1]_"

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwGetSignalQuality 0

    输出:
    Tk86xxGwGetSignalQuality 0
    Tk86xxGwGetSignalQuality:
    argv[0]: Tk86xxGwGetSignalQuality
    argv[1]: 0
    shell_Tk86xxGwGetSignalQuality: success
    BCN Rssi  : 690
    BCN Snr   : 0
    BCN Cfo   : 0
    DATA Rssi : -94
    DATA Snr  : 0
    DATA Cfo  : 0
    tshell>
    tshell>

Tk86xxGwTestMode
***********************************

- **功能描述**

用于测试模式。包括单TONE信号发送模式。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1", "参数2", "参数3"
    :widths: 30 30 30 30

    "Tk86xxGwTestMode", "通道索引 [1]_", "频率 [14]_", "发送功率 [15]_"

.. [14] 频率：范围470000000~510000000Hz 
.. [15] 发送功率：范围-40~20dBm

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwTestMode 0 473200000 20

    输出:
    Tk86xxGwTestMode 0 473200000 20
    Tk86xxGwTestMode:
    argv[0]: Tk86xxGwTestMode
    argv[1]: 0
    argv[2]: 473200000
    argv[3]: 20
    shell_Tk86xxGwTestMode: success
    tshell>
    tshell>

Tk86xxGwSetReg
***********************************

- **功能描述**

用于设置寄存器。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1", "参数2", "参数3"
    :widths: 30 30 30 30

    "Tk86xxGwSetReg", "通道索引 [1]_", "寄存器地址（十六进制）", "寄存器值（十六进制）"

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwSetReg 0 00080e10 00000200

    输出:
    Tk86xxGwSetReg 0 00080e10 00000200
    Tk86xxGwSetReg:
    argv[0]: Tk86xxGwSetReg
    argv[1]: 0
    argv[2]: 00080e10
    argv[3]: 00000200
    shell_Tk86xxGwSetReg: success
    tshell>
    tshell>

Tk86xxGwGetReg
***********************************

- **功能描述**

用于获取寄存器的值。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1", "参数1"
    :widths: 30 30 30

    "Tk86xxGwGetReg", "通道索引 [1]_", "寄存器地址（十六进制）"

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwGetReg 0 0008d008

    输出:
    Tk86xxGwGetReg 0 0008d008
    Tk86xxGwGetReg:
    argv[0]: Tk86xxGwGetReg
    argv[1]: 0
    argv[2]: 0008d008
    shell_Tk86xxGwGetReg: success
    addr: 0008d008, regValue  : 00000517
    tshell>
    tshell>

Tk86xxGwReset
***********************************

- **功能描述**

重启模块。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1"
    :widths: 30 30

    "Tk86xxGwReset", "通道索引 [1]_"

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwReset 0

    输出:
    Tk86xxGwReset 0
    Tk86xxGwReset:
    argv[0]: Tk86xxGwReset
    argv[1]: 0
    shell_Tk86xxGwReset: success
    tshell>
    tshell>

Tk86xxGwSetBaudRate
***********************************

- **功能描述**

用于设置模块波特率。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1", "参数2"
    :widths: 30 30 30

    "Tk86xxGwSetBaudRate", "通道索引 [1]_", "波特率"

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwSetBaudRate 0 115200

    输出:
    Tk86xxGwSetBaudRate 0 115200
    Tk86xxGwSetBaudRate:
    argv[0]: Tk86xxGwSetBaudRate
    argv[1]: 0
    argv[2]: 115200
    shell_Tk86xxGwSetBaudRate: success
    tshell>
    tshell>

Tk86xxGwSetGPIO
***********************************

- **功能描述**

用于配置无线模块GPIO状态。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1", "参数2", "参数3", "参数4", "参数5"
    :widths: 30 30 30 30 30 30

    "Tk86xxGwSetGPIO", "通道索引 [1]_", "引脚索引 [16]_", "输入输出 [17]_", "上拉下拉 [18]_", "输出电平 [19]_"

.. [16] 引脚索引：0-GPIO0，3-GPIO3
.. [17] 输入输出：0-输入模式，1-输出模式
.. [18] 上拉下拉：0-上拉模式，1-下拉模式，2-悬空模式
.. [19] 输出电平：0-低电平，1-高电平

- **示例**

.. code-block:: 

    输入:
    Tk86xxGwSetGPIO 0 0 1 0 0

    输出:
    Tk86xxGwSetGPIO 0 0 1 0 0
    Tk86xxGwSetGPIO:
    argv[0]: Tk86xxGwSetGPIO
    argv[1]: 0
    argv[2]: 0
    argv[3]: 1
    argv[4]: 0
    argv[5]: 0
    shell_Tk86xxGwSetGPIO: success
    tshell>
    tshell>


reboot
***********************************

- **功能描述**

网关重启。

- **参数解释**

无

- **示例**

.. code-block:: 

    输入:
    reboot

    输出:
    网关重启

ifconfig
***********************************

- **功能描述**

查询和配置网关网络信息。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1", "参数2", "参数3", "参数4", "参数5", "参数6"
    :widths: 30 30 30 30 30 30 30

    "ifconfig", "联网模式 [20]_", "地址分配方式 [21]_", "静态IP地址 [22]_", "静态网关地址 [23]_", "静态掩码 [24]_", "静态DNS [25]_"

.. [20] 联网模式：eth-以太网联网，cat-CAT模块联网
.. [21] 地址分配方式：dhcp-动态分配，static-静态分配
.. [22] 静态IP地址：静态IP地址，如：192.168.100.6
.. [23] 静态网关地址：静态网关地址，如：192.168.100.1
.. [24] 静态掩码：地址掩码，如：255.255.255.0
.. [25] 静态DNS：静态域名解析地址，如：114.114.114.114

.. warning:: 设置网络模式后，需要重启网关才能生效。

- **示例**

.. code-block:: 

    输入:
    ifconfig

    Cat1模式下输出:
    CAT1 IP: 10.223.35.241"
    以太网模式下输入：
    === W5500 NET CONF, DHCP mode ===
    MAC: 02:08:16:4E:77:0F
    SIP: 192.168.100.56
    GAR: 192.168.100.1
    SUB: 255.255.255.0
    DNS: 192.168.100.1

    输入
    ifconfig eth   // 切换为以太网联网
    ifconfig cat1  // 切换为CAT1联网
    ifconfig eth dhcp  // 切换为以太网联网，自动获取IP地址
    ifconfig eth static 192.168.100.3 192.168.100.1 255.255.255.0 114.114.114.114  // 切换为静态地址

printenv
***********************************

- **功能描述**

用于所有的显示环境变量。

- **参数解释**

无

- **示例**

.. code-block:: 

    输入:
    printenv

    输出:
    iap_need_copy_app=0
    iap_need_crc32_check=0
    iap_copy_app_size=0
    stop_in_bootloader=0
    baudrate_chan0=blob @0x000003D6 4bytes
    baudrate_chan1=blob @0x00000526 4bytes
    network_mode=blob @0x000005E2 1bytes

    mode: next generation
    size: 1507/4096 bytes.

resetenv
***********************************

- **功能描述**

用于初始化环境变量。

- **参数解释**

.. csv-table:: 
    :header: "命令", "参数1"
    :widths: 30 30

    "resetenv", "清空模式 [27]_"

.. [27] 清空模式： 0：清空参数，不包括无线模块串口波特率； 1：清空参数，包括无线模块串口波特率。

- **示例**

.. code-block:: 

    输入:
    resetenv 0
