### ***hostloc新帖推送机***

###### 简介：

迫于每次有活动都喝不上汤，特意搞了一个自动监视脚本，推送新帖到telegram的机器人，稍后有空补上推送到微信（微信已废，懒得修改了）。

目前已开通了推送频道，可自行点击查看推送效果：https://t.me/hostloc2tg

更新说明：
	1. 修改了获取了网站内容的方式
	2. 推送内容采用了markdown语法

###### 使用说明：

脚本基于python3，依赖环境requests，lxml，torequests，机器人每15秒更新一次（可自行修改）

需自行修改代码内容：第59行bot api需要改为自己bot api，115行修改推送id

**需要注册tg机器人，若要推送到频道，请将机器人添加到频道，并给予管理员权限**

直接nohup python3 hostloc2tg.py & 运行脚本

###### ht.sh文件说明：

**非必选项**

由于hostloc有时开启防御模式，导致部分国外ip无法访问hostloc，getupdate错误导致掉线，后台运行一个自动重新连接脚本（目前已解决update更新错误问题，但是由于用数组存储数据，比如存储标题，网页内容，还会存在不稳定掉线情况，大约2-3周出现一次）

使用方法：linux添加定时任务(小白建议宝塔面板计划任务，简单粗暴），**ht.sh存放在root目录下**，注意，ht脚本里的里需要修改为你的hostloc2tg.py的路径（**务必修改为你的文件路径**）

~~~
*/30 * * * * /root/ht.sh
~~~
后台运行脚本内容：

~~~
#!/bin/bash
# 30分钟判断一次进程是否存在，如果不存在就启动它
# python3请使用全路径，否则可能出现无法启动
PIDS=`ps -ef |grep hostloc2tg |grep -v grep | awk '{print $2}'`
if [ "$PIDS" != "" ]; then
	echo "myprocess is running!"
else
	echo "未发现程序后台运行，正在重启中！"
	/usr/bin/python3 /root/hostloc2tg.py &
fi
~~~

效果图：
![](https://s1.ax1x.com/2020/06/23/NNCgxS.jpg)


