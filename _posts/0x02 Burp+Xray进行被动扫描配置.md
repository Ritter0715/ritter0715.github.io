# Burp+Xray进行被动扫描配置

## 0x00 BurpSuite代理设置

BurpSuite手动测试配合xray做被动扫描，实际使用结果还不错，主要扫描出的漏洞集中在敏感信息泄露和xss一类的。

　　首先需要配置BurpSuite转发ip与端口：

　　流程：1、选择 user options 

　　　　　2、选择Upstream Proxy System

　　　　　3、添加ip与端口信息，第一行填 * 匹配任意字符，第二行填ip（这里的ip取决于你的xray服务所在的ip），第三行填端口

　　如图：

​						![image-20200722160937604](C:\Users\Ritt3r\AppData\Roaming\Typora\typora-user-images\image-20200722160937604.png)



## 0x01 Xray的证书和浏览器配置

打开xray(下载地址:[xray](https://github.com/chaitin/xray/releases))所在位置，运行：xray_windows_amd64.exe genca 生成证书，导入浏览器：

![img](https://img2020.cnblogs.com/blog/939362/202005/939362-20200521110031188-779604846.png)

点开火狐证书选项，点击导入，找到生成的ca.crt，然后勾选信任网站（这步跟burp导入证书一样）

![img](https://img2020.cnblogs.com/blog/939362/202005/939362-20200521110839370-221839088.png)

## 0x02 Xray开启监听

开启监听：xray_windows_amd64.exe webscan --listen 127.0.0.1:8989 --html-output result.html

![img](https://img2020.cnblogs.com/blog/939362/202005/939362-20200521111652909-1303748334.png)

完成监听后，burp上的操作都会被代理xray所监听到，进行被动扫描。然后去xray的文件目录下打开生成的result.html即可。

## 0x03 结束语

用了一段时间后（一周年白嫖的高级版），感觉xray的被动扫描出结果一般，不如其他的。但是备份文件、敏感配置文件、XSS效率挺高的。其他就那样。设置方式就这样，不想用xray的也可以使用其他被动扫描器。