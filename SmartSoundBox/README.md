### 概述

### 集成准备
  [resource下载](https://pan.baidu.com/s/1eSCMlzG)
  resource内容：
  1.Scene_*.jar
  > 场景开发SDK
  
  2.led_state_config_roobo.csv
  > LED 灯效优先级配置表
  
 3.DecisionTree
 > LED配置文件生成工具

4.SmartSoundBoxDemo
> 智能音响Demo的Android Studio工程
5.Deploy
> 部署文件夹

### 集成步骤
#### 实现LEDService
 1. 新建App
 2. 导入Jar
  导入resource中
 3. 配置AndroidMainfest
 在Application 节点下添加以下代码
``` java
    <meta-data
            android:name="ROOBO_MODULE_NAME"
            android:value="LED"/>
    <meta-data
            android:name="ROOBO_MODULE_TYPE"
            android:value="service"/>
    <meta-data
            android:name="ROOBO_KEEP_ALIVE"
            android:value="true"/>
```

4.实现ILEDService.Stub接口
实现showState(),showEffect(),cancelEffect()方法(具体实现参考Demo中的 LEDService)。
State:
> State 包括 Power state和Action State。LEDState 是根据当前的Power state(只有一个)和Action State(会有多个)通过配置决策表来自定义当前LED 输出的State。
> Power state:
> 3种(Standby-唤醒模式,Asleep-休眠模式,DeepSleep-勿扰模式)
> Action State:
 RooboOS中从语音输入到场景响应整个流程中定义了不同的Action State。在同一时刻会存在多个Action State的情况，例如正在播放音乐的时候又和设备进行对话。

Effect:
>Effect是独立于State的。现在RooboOS中定义了四种Effect,如果自己增加场景，可以增加Effect。
 EFFECT_VOLUME:调节声音时候的灯效
 EFFECT_BOOT_COMPLETE：启动完成的灯效
 EFFECT_NETWORK_SETTING_SUCCESS:配置网络成功灯效
EFFECT_NETWORK_SETTING_FAILURE：配网网络失败灯效

注意：Effect的优先级要高于State

5. Application初始化
在Application 的onCreate方法中注册LEDService
```java
  public void onCreate() {
        super.onCreate();
        LEDService ledService = new LEDService(this);
        Communicator.initialize(this, ledService);
  }
```

#### LED灯效优先级配置
当前LED要显示什么State，是和PowerState和ActiveState两个因素有关。不同的音响产品要根据这两种State去决定显示具体的State。某一时刻PowerState只会有一个，ActivieState有一个或多个。

 1. Power State
 >Standby:当前处在唤醒模式中
 >Asleep-当前处在休眠模式
 >DeepSleep-当前处在勿扰模式
 
 2. Active State
 > Listening:正在拾音
 > Translating:拾音结束正在语音识别中
 > WaitingAI:语音识别完成，正在等待AI处理
 > AILoading：AI正在处理中
 > WaitingAction:AI处理完成，等待场景响应
 > tts_play：正在TTS
 > media_loading：正在加载多媒体
 > music_play：正在播放多媒体
 > net_config：正在配网
 
 3. 配置决策表
 在resource文件夹中led_state_config_roobo.csv是LED灯效的默认配置。
 如图：
只需要更改"输出"这一列,其他内容不要修改。根据自己产品的需求自定义各种State组合下输出的State。定义的State，一定要在LEDService的showState()中实现对应的LED灯效。
 决策表配置规则：
 > 1.每一行对应一种LED State
 > 2.每种State 可以输入的值为"Y","N",空三种值
 > 3.Y表示当前状态中必须有这种状态，N表示状态中必须没有这种状态，空表示状态中有没有这种状态都可以
 > 4.各种state是逻辑与的关系
 
 举例:
 原始配置文件中“media_playing”,表示的意思是:当前不是勿扰模式，并且不处于AI处理中、等待处理、正在加载多媒体、正在配网状态，并且正在播放多媒体。则显示"media_playing"灯效
 
 4. 生成决策文件
	 1.准备好python3的环境
	 2.复制led_state_config_roobo.csv到resource中的DecisionTree文件夹中，执行下面命令生成"led_state_decision_tree.json"文件
	 
```
 python3 generate.py led_state_config_roobo.csv  led_state_decision_tree.json
```
 
5.  push 文件到设备(配置文件名必须是"led_state_decision_tree.json")。

 ```java
 adb push led_state_decision_tree.json_path /sdcard/ros/configure/
```

### 安装部署