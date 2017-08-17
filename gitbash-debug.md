##### Windows安装git之后闪退
使用Windows的cmd工具测试git bash查看报错：fatal:open /dev/null or dup failed:No such file or directory
1、将git bash所在路径添加到环境变量中。
2、进入git目录下的bin目录执行rebase -b 0x76000000 msys-1.0.dll语句。或者rebase -b 0x30000000 msys-1.0.dll；重启电脑。
3、重装git程序。
4、重启或启动null设备（右键我的电脑-> 管理 -> 设备管理器 -> 更多操作 -> 查看 -> 显示隐藏设备 -> 非即插即用驱动程序 -> null），重启电脑，解决问题。


