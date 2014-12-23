Realtek ALC AppleHDA - 解决睡眠唤醒后无声的问题
============

有些情况下，在10.9.2以后的系统（包括10.10）里，睡眠唤醒后会发生声音丢失的现象。这个问题首次出现于10.9.2系统下，讽刺的是，这正是苹果尝试修复原生硬件无声问题的时候（更多信息请看下面的**详细内容**）。有些用户相信是因为补丁才造成了这个故障，对此我(toleda)想声明的是，我的patch没有改动它一行编码(意思是不是我的责任)。相反，通过配置这个补丁使得音频解码可以支持AppleHDA要求。这个激活的AppleHDA解码引擎将不会再被支持，而且，同样，可能会被移除。解决这个问题将会变得不太可能。

###	详细内容
-	[Mavericks: No Audio - Realtek ALC AppleHDA \[Guide\] - Page 73](http://www.tonymacx86.com/audio/112461-mavericks-no-audio-realtek-alc-applehda-guide-73.html#)
	1.	credit: TimeWalker75a #721

###	解决方法
>	一个个地尝试，如果不行、先撤回前一次的工作、然后再尝试其他的方法)

A.	[Dolnor/EAPD-Codec-Commander](https://github.com/Dolnor/EAPD-Codec-Commander)
	1.	credit: TimeWalker75a #20, [No sound after waking from sleep](http://www.insanelymac.com/forum/topic/299166-no-sound-after-waking-from-sleep/?p=2073415)
	2.	set boot flag: darkwake=8
B.	[Releases · cliffom/appleHDAReset · GitHub](https://github.com/cliffom/appleHDAReset/releases)
	1.	credit: cliffom #92, [Realtek ALC 892 No sound after sleep \[10.9.2\]](http://www.tonymacx86.com/audio/127038-realtek-alc-892-no-sound-after-sleep-10-9-2-a-10.html#post852331)
C. [No OnBoard Audio After Wake From Sleep?](http://www.tonymacx86.com/audio/146465-no-onboard-audio-after-wake-sleep.html)
	1. credit: shilohh
D. AppleHDA prior to Apple "fix" (select patched or native AppleHDA
method)
	1. Install patched AppleHDA
		a. Mavericks 10.9.1/AppleHDA.kext_v2.5.3/MultiBeast 6.1.0
			i. [Downloads - tonymacx86.com](http://www.tonymacx86.com/downloads.php?do=file&id=208)
		b. Mavericks 10.9/AppleHDA.kext_v2.5.2/MultiBeast 6.0.1
			i. [Downloads - tonymacx86.com](http://www.tonymacx86.com/downloads.php?do=file&id=206)
	2. Install native AppleHDA (10.9 or 10.9.1, select one method)
		a. [toleda/audio_RealtekALC](https://github.com/toleda/audio_RealtekALC)
		b. [toleda/audio_CloverALC](https://github.com/toleda/audio_CloverALC)
E. Onboard audio substitutes
	1. PCIe
	2. USB
	3. HDMI

### Problem Reporting
A. No Support, contact developers

### [toleda](https://github.com/toleda/audio_realtekALC)