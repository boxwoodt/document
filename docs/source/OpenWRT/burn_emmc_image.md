# 基于 SD 卡烧录 eMMC 固件

本文介绍通过 SD 卡启动 OpenWRT 系统，将固件烧录到 eMMC 设备上，并以 eMMC 方式启动。

## 烧录 uboot 固件

1. 使用 `balenaEtcher` 软件烧录固件到 SD 卡，并通过 SD 卡启动 OpenWrt 系统。

2. 将 U-Boot 固件拷贝到运行中的 OpenWRT 系统。可以通过 scp 命令方式，其中 192.168.6.102 为开发板地址：

    ```shell
    cd bin/targets/imx/cortexa7/u-boot-mx6ull_atk_mmc
    scp u-boot.imx root@192.168.6.102:/root
    ```

3. 设置 mmcblk1boot0 为读写模式。

    ```shell
    echo 0 > /sys/block/mmcblk1boot0/force_ro
    ```

4. 将 U-Boot 固件烧写至 eMMC 启动分区。

    ```shell
    dd if=u-boot.imx of=/dev/mmcblk1boot0 bs=1024 seek=1 conv=fsync
    ```

5.  烧写完成后，关闭启动分区的写功能。

    ```shell
    echo 1 >/sys/block/mmcblk1boot0/force_ro
    ```

## 删除 eMMC 原有分区

1. 登录终端（可通过 SSH 或串口）。

2. 删除 eMMC 设备上的所有现有分区：

    ```shell
    fdisk /dev/mmcblk1
    p # 查看现有分区
    d # 删除分区
    w # 保存更改并退出
    ```

3. 重启开发板：

    ```shell
    reboot
    ```

## 烧录固件到 eMMC

1. 等待开发板重启完成。

2. 通过SCP传输固件到开发板：

    ```shell
    # 传输固件到设备
    scp openwrt-23.05-snapshot-r23789-f7c771329e-imx-cortexa7-imx6ull-atk-mmc-squashfs-combined.bin root@192.168.6.101:/root
    ```

3. 开始烧录固件：

    ```shell
    # 进入SD卡启动，烧录镜像
    dd if=openwrt-23.05-snapshot-r23789-f7c771329e-imx-cortexa7-imx6ull-atk-mmc-squashfs-combined.bin of=/dev/mmcblk1 bs=1M conv=notrunc
    ```

## 系统运行

- 关闭电源，移除 SD 卡，并调整拨码开关为 eMMC 启动。

- 打开电源，系统将自动从 eMMC 运行。可以通过串口查看系统启动过程。
