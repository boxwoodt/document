网关 API
=======================

类型定义
~~~~~~~~~~~~~~~

APIRet
------------

.. code-block:: c
   :linenos:

    typedef enum {
        API_SUCCESS, // API调用成功
        API_FAILED,  // API调用失败
        API_TIMEOUT, // API调用超时
    } APIRet;

DeviceMode
------------

.. code-block:: c 
    :linenos:

    typedef enum {
        SYNC, // 同步模式
        ASYN, // 异步模式，只用配置一个时隙（数据时隙）
    } DeviceMode;

IrqMask
------------

.. code-block:: c 
    :linenos:

    typedef enum {
        IRQ_FIRST_SLOT, // 只开第一时隙中断
        IRQ_LAST_SLOT,  // 只开最后时隙中断
        IRQ_ALL_SLOT,   // 打开所有时隙中断
    } IrqMask;

SlotType
------------

.. code-block:: c
    :linenos:

    typedef enum {
        SLOT_BCN,  // BCN类型
        SLOT_DATA, // 数据类型
    } SlotType;

SlotState
------------

.. code-block:: c 
    :linenos:

    typedef enum {
        SLOT_TX,   // TX时隙
        SLOT_RX,   // RX时隙
        SLOT_IDLE, // 空闲时隙
    } SlotState;

TxPower
------------

.. code-block:: c
    :linenos:

    typedef enum {
        N40_DBM = -40, // -40dBm
        N39_DBM,       // -39dBm
        N38_DBM,       // -38dBm
        N37_DBM,       // -37dBm
        N36_DBM,       // -36dBm
        N35_DBM,       // -35dBm
        N34_DBM,       // -34dBm
        N33_DBM,       // -33dBm
        N32_DBM,       // -32dBm
        N31_DBM,       // -31dBm
        N30_DBM,       // -30dBm
        N29_DBM,       // -29dBm
        N28_DBM,       // -28dBm
        N27_DBM,       // -27dBm
        N26_DBM,       // -26dBm
        N25_DBM,       // -25dBm
        N24_DBM,       // -24dBm
        N23_DBM,       // -23dBm
        N22_DBM,       // -22dBm
        N21_DBM,       // -21dBm
        N20_DBM,       // -20dBm
        N19_DBM,       // -19dBm
        N18_DBM,       // -18dBm
        N17_DBM,       // -17dBm
        N16_DBM,       // -16dBm
        N15_DBM,       // -15dBm
        N14_DBM,       // -14dBm
        N13_DBM,       // -13dBm
        N12_DBM,       // -12dBm
        N11_DBM,       // -11dBm
        N10_DBM,       // -10dBm
        N9_DBM,        // -9dBm
        N8_DBM,        // -8dBm
        N7_DBM,        // -7dBm
        N6_DBM,        // -6dBm
        N5_DBM,        // -5dBm
        N4_DBM,        // -4dBm
        N3_DBM,        // -3dBm
        N2_DBM,        // -2dBm
        N1_DBM,        // -1dBm
        P0_DBM,        // 0dBm
        P1_DBM,        // 1dBm
        P2_DBM,        // 2dBm
        P3_DBM,        // 3dBm
        P4_DBM,        // 4dBm
        P5_DBM,        // 5dBm
        P6_DBM,        // 6dBm
        P7_DBM,        // 7dBm
        P8_DBM,        // 8dBm
        P9_DBM,        // 9dBm
        P10_DBM,       // 10dBm
        P11_DBM,       // 11dBm
        P12_DBM,       // 12dBm
        P13_DBM,       // 13dBm
        P14_DBM,       // 14dBm
        P15_DBM,       // 15dBm
        P16_DBM,       // 16dBm
        P17_DBM,       // 17dBm
        P18_DBM,       // 18dBm
        P19_DBM,       // 19dBm
        P20_DBM,       // 20dBm
    } TxPower;

RateMode
------------

.. code-block:: c
    :linenos:

    typedef enum {
        RATE_MODE_4  = 4,  // 速率模式4，数据类型时传输速率441bps
        RATE_MODE_5  = 5,  // 速率模式5，数据类型时传输速率934bps
        RATE_MODE_6  = 6,  // 速率模式6，数据类型时传输速率1868bps
        RATE_MODE_7  = 7,  // 速率模式7，数据类型时传输速率3736bps
        RATE_MODE_8  = 8,  // 速率模式8，数据类型时传输速率7472bps
        RATE_MODE_9  = 9,  // 速率模式9，数据类型时传输速率14946bps
        RATE_MODE_10 = 10, // 速率模式10，数据类型时传输速率29891bps
        RATE_MODE_11 = 11, // 速率模式11，数据类型时传输速率59783bps
        RATE_MODE_18 = 18, // 速率模式18，数据类型时传输速率85106bps
        RATE_MODE_24 = 24, // 速率模式24
    } RateMode;

SlotIrq
------------

.. code-block:: c
    :linenos:

    typedef enum {
        TX_DONE,     // 发送完成
        RX_DONE,     // 接收完成
        IDLE_DONE,   // 时隙结束，未产生收发操作
        WAKEUP_DONE, // 唤醒完成
    } SlotIrq;

WakeUpSrc
------------

.. code-block:: c
    :linenos:

    typedef enum {
        WAKEUP_GPIO,                // GPIO唤醒
        WAKEUP_TIMER,               // 定时唤醒
        WAKEUP_WIRELESS,            // 无线唤醒
        WAKEUP_GPIO_TIMER,          // GPIO和定时组合唤醒
        WAKEUP_GPIO_WIRELESS,       // GPIO和无线组合唤醒
        WAKEUP_TIMER_WIRELESS,      // 定时和无线组合唤醒
        WAKEUP_GPIO_TIMER_WIRELESS, // GPIO、定时和无线组合唤醒
    } WakeUpSrc;

ClkSrc
------------

.. code-block:: c
    :linenos:

    typedef enum {
        CLK_RC,
        CLK_OSC32K,
    } ClkSrc;

ScanMode
------------

.. code-block:: c
    :linenos:

    typedef enum {
        SCAN_MODE_4 = 4, // 单次采样时间8ms，检测边界-112dbm，检测带宽64K
    } ScanMode;

ScanBW
------------

.. code-block:: c
    :linenos:

    typedef enum {
        SCAN_BW_64K,  // 检测带宽64K
        SCAN_BW_128K, // 检测带宽128K
        SCAN_BW_256K, // 检测带宽256K
    } ScanBW;

TestMode
------------

.. code-block:: c
    :linenos:

    typedef enum {
        SINGLE_TONE, // 单TONE测试模式
    } TestMode;

CascadeSync
------------

.. code-block:: c
    :linenos:

    typedef enum {
        CASCADE_IN_EN,   // 级联信号输入使能
        CASCADE_OUT_EN,  // 级联信号输出使能
        CASCADE_IN_DIS,  // 级联信号输入禁能
        CASCADE_OUT_DIS, // 级联信号输出禁能
    } CascadeSync;


ICTCtrlMode
------------

.. code-block:: c
    :linenos:

    typedef enum {
        FREQ_OFFSET,  // 频率补偿
        POWER_OFFSET, // 功率补偿
    } ICTCtrlMode;

BaudRate
------------

.. code-block:: c
    :linenos:

    typedef enum {
        BAUD_RATE_57600   = 57600,
        BAUD_RATE_115200  = 115200,
        BAUD_RATE_230400  = 230400,
        BAUD_RATE_460800  = 460800,
        BAUD_RATE_921600  = 921600,
        BAUD_RATE_1000000 = 1000000
    } BaudRate;

PinDir
------------

.. code-block:: c
    :linenos:

    typedef enum {
        PIN_IN,  /*!< 引脚输入模式 */
        PIN_OUT, /*!< 引脚输出模式 */
    } PinDir;

PinPull
------------

.. code-block:: c
    :linenos:

    typedef enum {
        PIN_PULL_UP,   /*!< 引脚上拉模式 */
        PIN_PULL_DOWN, /*!< 引脚下拉模式 */
        PIN_PULL_NONE, /*!< 引脚悬空模式 */
    } PinPull;

PinLevel
------------

.. code-block:: c
    :linenos:

    typedef enum {
        PIN_LOW,  /*!< 引脚低电平 */
        PIN_HIGH, /*!< 引脚高电平 */
    } PinLevel;

IrqCb
------------

.. code-block:: c
    :linenos:

    typedef struct {
        UINT8 pinIdx;   // 引脚序号。取值0~7
        UINT8 trigType; // 触发类型。0-下降沿, 1-上升沿。持续1.8微秒
    } IrqCb;

InitCfg
------------

.. code-block:: c
    :linenos:

    typedef struct {
        DeviceMode deviceMode;    // 设备模式。0-同步模式，1-异步模式
        UINT32     slotPeriodNum; // 时隙周期数，异步模式无需配置。表明运行多少个时隙周期后停止，0 表示不停止，一直运行下去
        UINT8      slotNum;       // 时隙数，异步模式无需配置。表明一个时隙周期中包含的时隙个数
        IrqMask    irqMask;       // 中断掩码。0-只开第一时隙中断，1-只开最后时隙中断，2-打开所有时隙中断
        IrqCb      irqCb;         // 中断回调
        UINT8      addltFunc;     // 可选字段开关。Bit0-包长字段开关；Bit1-CRC16校验；其他保留
    } InitCfg;

SlotCfg
------------

.. code-block:: c
    :linenos:

    typedef struct {
        SlotType  slotType;  // 时隙类型，0-BCN，1-DATA
        SlotState slotState; // 时隙状态，0-TX，1-RX，2-IDLE
        UINT32    freq;      // 频点
        TxPower   txPower;   // 发射功率
        RateMode  rateMode;  // 速率模式
        UINT16    byteLen;   // DATA类型的字节数，BCN类型时字节数只能是0或者1，单位Byte
        UINT32    timeLen;   // 空闲时隙的时间长度，其他模式下无效，单位微秒
    } SlotCfg;

ChipInfo
------------

.. code-block:: c
    :linenos:

    typedef struct {
        UINT8  chipVer;   // 芯片版本。芯片内部硬件版本号，每次重新流片需更新硬件版本号。此信息储存在efuse中，只读。
        UINT32 chipId;    // 芯片ID。芯片识别码，每个芯片不同，储存在芯片内部efuse中，只读。
        UINT32 sdkVer;    // SDK版本，固件版本号。
        UINT16 flashSize; // Flash容量，单位KBytes。
    } ChipInfo;

Status
------------

.. code-block:: c
    :linenos:

    typedef struct {
        UINT32  slotPeriodCnt; // 时隙周期计数器，对于目前工作的时隙周期计数
        UINT8   slotIdx;       // 时隙序号，目前工作的时隙序号
        SlotIrq slotIrq;       // 时隙产生的中断类型
    } Status;

RcvData
------------

.. code-block:: c
    :linenos:

    typedef struct {
        UINT32 slotPeriodCnt;
        UINT8  slotIdx;
        UINT16 dataLen;
        UINT8  data[MAX_DATA_LENGTH];
    } RcvData;

GpioSrcCfg
------------

.. code-block:: c
    :linenos:

    typedef struct {
        UINT8 pinIdx;    // 引脚序号。取值0~7
        UINT8 trigLevel; // 触发电平。0-低电平, 1-高电平
    } GpioSrcCfg;


TimerSrcCfg
------------

.. code-block:: c
    :linenos:

    typedef struct {
        UINT32 timer;  // 定时时间（毫秒）
        ClkSrc clkSrc; // 时钟源类型。0-RC，1-OSC32K // todo:
    } TimerSrcCfg;

WORCfg
------------

.. code-block:: c
    :linenos:

    typedef struct {
        UINT8  mode;   // 无线唤醒类型，取值1~4，默认填充4 // todo:
        UINT8  id;     // 无线唤醒ID // todo:
        UINT32 freq;   // 无线唤醒频点
        UINT32 period; // 无线唤醒周期
    } WORCfg;

SleepCfg
------------

.. code-block:: c
    :linenos:

    typedef struct {
        WakeUpSrc   wakeUpSrc;   // 唤醒源
        GpioSrcCfg  gpioSrcCfg;  // GPIO唤醒的配置
        TimerSrcCfg timerSrcCfg; // 定时唤醒的配置
        WORCfg      wORCfg;      // 无线唤醒的配置
        IrqCb       wakeUpCb;    // 唤醒后中断回调
    } SleepCfg;

SignalQuality
-----------------

.. code-block:: c
    :linenos:

    typedef struct {
        int rssi; // 接收的信号强度
        int snr;  // 接收的信噪比
        int cfo;  // 接收的频偏
    } SignalQuality;

TestCfg
------------

.. code-block:: c
    :linenos:

    typedef union {
        struct {
            UINT32  freq;    // 频点
            TxPower txPower; // 发射功率
        } singleToneCfg;
    } TestCfg;


函数
~~~~~~~~~~~~~~~

Tk86xxGwGetBootMode
------------------------

.. c:function:: APIRet Tk86xxGwGetBootMode(UINT8 chanIdx, UINT8 *bootMode)

- **功能描述**

用于获取启动模式。包括正常启动，GPIO唤醒，定时唤醒，无线唤醒。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - OUT
      - UINT8 *
      - bootMode
      - 启动模式

- **返回值**

`APIRet`_

Tk86xxGwInit
------------------------

.. c:function:: APIRet Tk86xxGwInit(UINT8 chanIdx, InitCfg *initCfg)

- **功能描述**

用于PHY初始化。设置设备模式、时隙周期参数、中断配置等信息。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - `InitCfg`_ *
      - initCfg
      - 初始化配置信息

- **返回值**

`APIRet`_


Tk86xxGwSetSlot
------------------------

.. c:function:: APIRet Tk86xxGwSetSlot(UINT8 chanIdx, UINT8 beginSlotIdx, UINT8 slotNum, SlotCfg *slotCfg)

- **功能描述**

用于设置时隙参数。包括时隙类型、时隙状态、频点、发射功率、速率模式、时隙长度。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - UINT8
      - beginSlotIdx
      - 起始时隙索引
    * - IN
      - UINT8
      - slotNum
      - 起始时隙索引
    * - IN
      - `SlotCfg`_ *
      - slotCfg
      - 时隙配置信息

- **返回值**

`APIRet`_


Tk86xxGwGetChipInfo
------------------------

.. c:function:: APIRet Tk86xxGwGetChipInfo(UINT8 chanIdx, ChipInfo *chipInfo)

- **功能描述**

用于获取芯片信息。包括芯片版本号、芯片ID、SDK版本号、Flash大小。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - OUT
      - `ChipInfo`_ *
      - chipInfo
      - 芯片信息

- **返回值**

`APIRet`_


Tk86xxGwGetVolt
------------------------

.. c:function:: APIRet Tk86xxGwGetVolt(UINT8 chanIdx, UINT8 *volt)

- **功能描述**

用于获取电压信息。单位为0.1V。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - OUT
      - UINT8 *
      - volt
      - 芯片电压

- **返回值**

`APIRet`_


Tk86xxGwGetTemp
------------------------

.. c:function:: APIRet Tk86xxGwGetTemp(UINT8 chanIdx, UINT8 *temp)

- **功能描述**

用于获取温度信息。单位为℃。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - OUT
      - UINT8 *
      - temp
      - 芯片温度

- **返回值**

`APIRet`_


Tk86xxGwOpenRadio
------------------------

.. c:function:: APIRet Tk86xxGwOpenRadio(UINT8 chanIdx)

- **功能描述**

用于打开射频开关。调用Tk86xxSetSlot设置时隙后，均需要打开射频开关。如果是再次打开射频开关，调用前需先调用关闭射频开关。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引

- **返回值**

`APIRet`_


Tk86xxGwCloseRadio
------------------------

.. c:function:: APIRet Tk86xxGwCloseRadio(UINT8 chanIdx)

- **功能描述**

用于关闭射频开关。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引

- **返回值**

`APIRet`_


Tk86xxGwCheckStatus
------------------------

.. c:function:: UINT8  Tk86xxGwCheckStatus(UINT8 chanIdx, Status *status)

- **功能描述**

用于检查当前中断状态。包括发送完成、接收完成、唤醒完成等。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - OUT
      - `Status`_ *
      - status
      - 中断状态

- **返回值**

| 0: 未产生中断 
| 1: 产生中断


Tk86xxGwRcvData
------------------------

.. c:function:: UINT16 Tk86xxGwRcvData(UINT8 chanIdx, UINT8 *buf, UINT16 bufLen, SignalQuality *signalQuality)

- **功能描述**

用于接收数据。当BCN长度配置1字节时也可以接收BCN负载数据。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - OUT
      - UINT8 *
      - buf
      - 接收数据空间地址
    * - IN
      - UINT16
      - bufLen
      - 接收数据空间长度
    * - OUT
      - `SignalQuality`_ *
      - signalQuality
      - 接收数据质量

- **返回值**

| UINT16: 实际数据长度


Tk86xxGwSendData
------------------------

.. c:function:: APIRet Tk86xxGwSendData(UINT8 chanIdx, UINT8 slotIdx, UINT8 *data, UINT16 len)

- **功能描述**

用于发送数据。当数据长度低于时隙长度时，通过自动补零方式使数据长度与时隙长度相等。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - UINT8
      - slotIdx
      - 发送时隙索引
    * - IN
      - UINT8 *
      - data
      - 发送数据空间
    * - IN
      - UINT16
      - len
      - 发送数据长度

- **返回值**

`APIRet`_


Tk86xxGwSendBcnData
------------------------

.. c:function:: APIRet Tk86xxGwSendBcnData(UINT8 chanIdx, UINT8 slotIdx, UINT8 data)

- **功能描述**

用于发送BCN的负载数据。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - UINT8
      - slotIdx
      - 发送时隙索引
    * - IN
      - UINT8
      - data
      - 发送BCN数据

- **返回值**

`APIRet`_


Tk86xxGwSleep
------------------------

.. c:function:: APIRet Tk86xxGwSleep(UINT8 chanIdx, SleepCfg *sleepCfg)

- **功能描述**

用于设置休眠参数并进入休眠。设置包括唤醒源、唤醒源的配置、唤醒后的中断。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - `SleepCfg`_ *
      - sleepCfg
      - 休眠配置

- **返回值**

`APIRet`_


Tk86xxGwWakeUp
------------------------

.. c:function:: APIRet Tk86xxGwWakeUp(UINT8 chanIdx, WORCfg *wORCfg)

- **功能描述**

用于设置唤醒参数并发送唤醒信号。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - `WORCfg`_ *
      - wORCfg
      - 唤醒配置

- **返回值**

`APIRet`_


Tk86xxGwScanChan
------------------------

.. c:function:: APIRet Tk86xxGwScanChan(UINT8 chanIdx, UINT32 freq, ScanMode scanMode, ScanBW scanBW, int16_t *rssi)

- **功能描述**

用于侦听信道。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - UINT32
      - freq
      - 扫频频点
    * - IN
      - `ScanMode`_
      - scanMode
      - 扫频模式
    * - IN
      - `ScanBW`_
      - scanBW
      - 扫频带宽
    * - OUT
      - int16_t *
      - rssi
      - 扫频频点信号质量

- **返回值**

`APIRet`_


Tk86xxGwGetSignalQuality
---------------------------

.. c:function:: APIRet Tk86xxGwGetSignalQuality(UINT8 chanIdx, SignalQuality *bcnQuality, SignalQuality *dataQuality)

- **功能描述**

用于获取当前信号质量。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - OUT
      - `SignalQuality`_ *
      - bcnQuality
      - BCN 信号质量
    * - OUT
      - `SignalQuality`_
      - dataQuality
      - DATA 信号质量

- **返回值**

`APIRet`_


Tk86xxGwTestMode
---------------------------

.. c:function:: APIRet Tk86xxGwTestMode(UINT8 chanIdx, TestMode testMode, TestCfg *testCfg)

- **功能描述**

用于测试模式。包括单TONE信号发送模式。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - `TestMode`_
      - testMode
      - 测试模式
    * - IN
      - `TestCfg`_
      - testCfg
      - 测试参数

- **返回值**

`APIRet`_


Tk86xxGwCascadeSync
---------------------------

.. c:function:: APIRet Tk86xxGwCascadeSync(UINT8 chanIdx, UINT8 pinIdx, CascadeSync cascadeSync)

- **功能描述**

用于级联同步控制。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - UINT8
      - pinIdx
      - 引脚索引
    * - IN
      - `CascadeSync`_
      - cascadeSync
      - 级联控制

- **返回值**

`APIRet`_


Tk86xxGwSetReg
---------------------------

.. c:function:: APIRet Tk86xxGwSetReg(UINT8 chanIdx, UINT32 regAddr, UINT32 regValue)

- **功能描述**

用于设置寄存器。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - UINT32
      - regAddr
      - 寄存器地址
    * - IN
      - UINT32
      - regValue
      - 设置数据

- **返回值**

`APIRet`_


Tk86xxGwGetReg
---------------------------

.. c:function:: APIRet Tk86xxGwGetReg(UINT8 chanIdx, UINT32 regAddr, UINT32 *regValue)

- **功能描述**

用于获取寄存器的值。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - UINT32
      - regAddr
      - 寄存器地址
    * - OUT
      - UINT32 *
      - regValue
      - 获取寄存器值

- **返回值**

`APIRet`_


Tk86xxGwReset
---------------------------

.. c:function:: APIRet Tk86xxGwReset(UINT8 chanIdx)

- **功能描述**

用于重启无线模块。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引

- **返回值**

`APIRet`_


Tk86xxGwSetBaudRate
---------------------------

.. c:function:: APIRet Tk86xxGwSetBaudRate(UINT8 chanIdx, BaudRate baudRate)

- **功能描述**

用于配置无线模块波特率。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - `BaudRate`_
      - baudRate
      - 波特率值

- **返回值**

`APIRet`_


Tk86xxGwSetGPIO
---------------------------

.. c:function:: APIRet Tk86xxGwSetGPIO(UINT8 chanIdx, UINT8 pinIdx, PinDir pinDir, PinPull pinPull, PinLevel pinLevel)

- **功能描述**

用于配置无线模块GPIO状态。

- **参数解释**

.. list-table:: 
    :widths: 10 15 20 30
    :header-rows: 1

    * - IN/OUT
      - 类型
      - 参数名
      - 描述
    * - IN
      - UINT8
      - chanIdx
      - 无线通道索引
    * - IN
      - UINT8
      - pinIdx
      - 引脚索引
    * - IN
      - `PinDir`_
      - pinDir
      - 引脚输入输出
    * - IN
      - `PinPull`_
      - pinPull
      - 引脚上拉下拉
    * - IN
      - `PinLevel`_
      - pinLevel
      - 引脚输出电平

- **返回值**

`APIRet`_

