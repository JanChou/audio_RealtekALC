audio_realtekALC
============

### 瑞昱ALC声卡 - AppleHDA.kext补丁
此补丁通过`AppleHDA.kext`激活瑞昱ALC系列声卡的所有功能，包括板载音频、HDMI以及DP音响（详见***注A***）。该脚本会给音频解码二进制文件打补丁，并安装配置数据（接口配置），布局（音频设备）和平台（路线图）等文件。除了本补丁，无其他文件要求下载。


### 更新：
-	v3.4 - 支持BRIX/ALC269, BRIX Pro/ALC283 and NUC/ALC283, 详见***注F***
-	v3.3 - audio_realtekALC-100.sh (v1.0.3) release
-	v3.1：增加了对Yosemite下*x99*的补丁支持：`audio_alc_x99-hda-100_patch.command`。
-	v3：对Yosemite/10.10.x系统和Mavericks/10.9.x系统和Mountain Lion/10.8.x系统的支持
	-	注：audio_realtekALC-90_v2.command不支持
-	v2.1：对9系主板/EAPD的支持增加到ALC887,892,898,1150等型号，赞助者：kidalive
-	v2：更新脚本：无需下载，双击即可完成。


###	方法(在适当的位置打补丁)
1.	已打过补丁的`AppleHDA.kext` - ConfigData, layouts, Platforms and HDA binary patch
2.	原生`AppleHDA.kext`

###	安装步骤
A.	给`AppleHDA.kext`打补丁
	1.	找到audio_realtekALC-100.command.zip(见上)
	2.	下载
	3.	解压缩放到`~/Download`下，双击
	4.	输入密码
	5.	确认型号**Codec ALCxxx: 仅适用于(885, 887, 888, 889, 892, 898, 1150)**
	6.	是否为Current_v100302 (y/n): 仅适用于(887, 888 only)
	7.	是否激活HD4600 HDMI音频：	仅适用于(887, 892, 898, 1150)
B.	验证`AppleHDA.kext`是否已安装
	-	SLE目录下是否存在修改过的`AppleHDA.kext`
	-	点击查看版本号是否为`vx.x-toledaALCxxx`格式
C.	重启
D.	验证板载音频
	-	系统设置/声音/输出/选择音频设备


### 其他OSX系统瑞昱ALC系列声卡板载音频解决方案
1.	https://github.com/toleda/audio_pikeralphaALC
2.	https://github.com/toleda/audio_CloverALC


### 条件要求
A.	Chameleon/Chimera/Clover：
	-	可选择Clover补丁方式（无需DSDT）
	-	参考 https://github.com/toleda/audio_CloverALC
B.	OS X
	-	10.10或更新的
	-	10.9或更新的
	-	10.8或更新的
C.	原版`AppleHDA.kext`（若未安装或不存在，请先安装OSX系统）
D.	受支持的瑞昱板载音频解码型号
E.	音频ID注入，参考 https://github.com/toleda/audio_ALCinjection


### 要求信息（选择一种类型）
A.	Codec/ALC支援方式（自动侦测）
	1. 269 (BRIX only)
	2. 283 (BRIX Pro and NUC)
	3. 885
	4. 887
	5. 888
	6. 889
	7. 892
	8. 898
	9. 1150 (see Note F)
B.	Layout（接口布局）支援方式（定义详见***注B***）
	1. 269, 283. 885, 887, 888, 889, 892, 898, 1150
	2. 887, 888, 889, 892, 898, 1150
	3. 887, 888, 889, 892, 898


###	OS X不支持的芯片组
  A. 9系主板支持 (仅支持Mavericks系统, 详见***注D***)
  B. X99主板支持 (详见***注E***)


###	注
  A. HDMI/DP音频可能还要求
	1. 注入dsdt/ssdt
	2. 注入framebuffer
  B. Layout定义(Layout/Audio ID安装注入是分开的，参考 https://github.com/toleda/audio_ALCInjection)
	1 - 3/5/6 个接口的模拟音频输出
	2 - 3 个模拟音频输出接口
	3 - HD3000/HD4000 HDMI音频和模拟音频
  C. 建议
	1. 备份到桌面 Desktop/audio_ALCxxx-10.x.x
	   a. 原生的: AppleHDA-orig.kext
	   b. 打过补丁的: AppleHDA.kext
	2. 如果软件升级后造成音频失败
	   a. 参考上面的安装步骤 (再次运行脚本)
	   b. 如果新补丁失败，安装备份过的可以工作的打过补丁的`AppleHDA.kext`
  D. OS X/AppleHDA.kext/9系主板支持 (仅限于Mavericks，并只需从以下选择一种方法安装)
	1. 下载并安装`audio_alc_9series-hda-93_patch.command`
	2. 给ApppleHDAController`以二进制方式打补丁:
	   a. 查找: 20 8C
	   b. 替换 (会有四次): A0 8C
	   c. 保存
	   d. 重启
  E. OS X/AppleHDA.kext/x99主板支持 (暂时的方案, 并只需从以下选择一种方法安装)
	1. 下载并安装`audio_alc_x99-hda-100_patch.command`
	2. 给ApppleHDAController`以二进制方式打补丁:
	   a. 查找: 20 8C
	   b. 替换 (会有四次): 20 8D
	   c. 保存
	   d. 重启
  F. 对BRIX/ALC269, BRIX Pro/ALC283 以及 NUC/ALC283 的支持
	1. 安装方法
	   a. 将补丁文件`realtekALC`放到适当的位置
	2. 音频设备
	   a. ALC269 - BRIX/耳机和 SPDIF数字输出
	   b. ALC283 - BRIX Pro 和 NUC/耳机 (麦克风尚不支持)
	   c. HDMI 音频需要注入 dsdt 或 ssdt, 参考
	      i.  HD4600 - https://github.com/toleda/audio_hdmi_8series
	      ii. HD4000 - https://github.com/toleda/audio_hdmi_hd4000


###	工具
  A. IOReg (View Raw) - [点这里下载](https://github.com/toleda/audio_ALCInjection/blob/master/IORegistryExplorer_v2.1.zip)
  B. DPCIManger - http://sourceforge.net/projects/dpcimanager/
  C. audio_codecdetect.command (见上面的文件) - 侦测、确认以及安装音频解码
	2. 选择 audio_codecdetect.command 下载
	1. 放到 ~/Downloads/audio_codecdetect.command 位置双击安装
	2. 输入密码:


###	问题报告 (需包含以下信息)
  A. 音频问题的详细情况
	1. OS X 系统版本/主板型号/BIOS 版本/处理器/显卡
	2. 你的安装过程/你使用的是上面哪一种步骤/AppleHDA.kext 版本
	3. IOReg的导出文件 - IOReg_v2.1/点File/然后Save a Copy As…, 并验证文件 (并非是ioreg.txt)
	4. 安装过的 S/L/E/AppleHDA.kext
	5. AppleHDA(哪种型号).kext (例如, AppleHDA1150.kext, 如果你安装的是ALC1150的话)
	6. DPCIManager/Misc/Boot Log
	7. 系统信息/硬件/音频/的完整截图
	8. 控制台/所有消息/选择包含`kernel Sound assertions`的部分/保存为...
	9. 如果使用的是Chameleon/Chimera
	   a. Extra/org.chameleon.Boot.plist
	   b. Extra/dsdt.aml (如果有)
	   c. Extra/ssdt.aml (如果有)
	10. 如果使用的是Clover
	   a. EFI/CLOVER/config.plist
	   b. EFI/CLOVER/ACPI/Patched/dsdt.aml (如果有) 
	   c. EFI/CLOVER/ACPI/Patched/ssdt.aml (如果有)
  B. 到这些地方跟帖:
	1. http://www.tonymacx86.com/audio/112461-mavericks-no-audio-realtek-alc-applehda.html
	2. http://www.insanelymac.com/forum/topic/298819-yosemite-audio-realtek-alc-applehda/
	3. http://www.insanelymac.com/forum/topic/293001-mavericks-realtek-alc-applehda-audio/

Credit
bcc9, RevoGirl, PikeRAlpha, SJ_UnderWater, RehabMan, TimeWalker75a

toleda
https://github.com/toleda/audio_RealtekALC