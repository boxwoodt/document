# 有线网络和 4G 网络自动切换

## 背景

在 OpenWRT 系统的路由器上，当同时接入 4G 网络和有线网络时，如果其中一个网络断开，则另一个网络无法自动切换。此问题通常是由于未正确设置网络接口的 metric 参数。

## 解决方法

通过在接口的网络配置文件中设置 4G 和有线网络的 metric 参数，可以实现网络的自动切换。

## 步骤

1. **配置有限网络接口**

   在 `/etc/config/network` 中找到有线网络接口（通常为 `wan`），并为其添加 `metric` 参数。例如：

   ```sh
   config interface 'wan'
       option device 'eth0'
       option proto 'dhcp'
       option metric '0' # 新增
   ```

2. **配置 4G 网络接口**

   如果使用的是 4G 网络接口（例如 `wan_4g`），则需要为其设置不同的 `metric` 参数。例如：

   ```sh
   config interface 'wan_4g'
       option proto 'dhcp'
       option device 'usb0'
       option metric '1' # 新增
   ```

**说明**

- `metric` 参数为路由指定所需的跃点数（范围是 1 ~ 9999）。它用于在路由表中选择与转发包的目标地址最匹配的路由。被选中的路由具有最少的跃点数。
- `metric` 的值越小，优先级越高。如果两个网络接口的 `metric` 值相同，可能会导致优先级冲突，最终导致一个接口无法正常工作。

## 默认配置

1. **有线网络接口配置**

	当接口为`wan`时，设置`metric`为`0`:

	```sh
		dhcp)
			# fixup IPv6 slave interface if parent is a bridge
			[ "$type" = "bridge" ] && device="br-$1"

            # 新增加开始
			[ "$1" = "wan" ] && {
				uci -q batch <<-EOF
					set network.$1.metric='0'
				EOF
			}
            # 新增加结束

			uci set network.$1.proto='dhcp'
			[ -e /proc/sys/net/ipv6 ] && {
				uci -q batch <<-EOF
					delete network.${1}6
					set network.${1}6='interface'
					set network.${1}6.device='$device'
					set network.${1}6.proto='dhcpv6'
				EOF
			}
		;;
	```

2. **4G 网络接口配置**

	修改 `package/base-files/files/bin/config_generate` 文件中`generate_4g_network()` 函数来设置 `metric` 为 `1`，其中 `generate_4g_network` 函数是参考《使用 EC20 无线网卡模块上网》文档中增加：

	```sh
	generate_4g_network() {
		uci -q batch <<-EOF
			delete network.wan_4g
			set network.wan_4g='interface'
			set network.wan_4g.proto='dhcp'
			set network.wan_4g.device='usb0'
			set network.wan_4g.metric='1'     # 新增加
		EOF
	}
	```	

通过以上步骤，可以确保当有线网络或 4G 网络断开时，系统能够自动切换到另一个可用的网络连接。
