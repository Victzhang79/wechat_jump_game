# 教你用Python来玩微信跳一跳

> 2017年12月28日下午，微信发布了 6.6.1 版本，加入了「小游戏」功能，并提供了官方 demo「跳一跳」。

[https://wangshub.github.io](https://wangshub.github.io)

[项目地址](https://github.com/wangshub/wechat_jump_game)

### **更新日志：**

> 2017-12-29 ： 增加更新自动化运行脚本，感谢github上的binderclip


## 游戏模式

这是一个 2.5D 插画风格的益智游戏，玩家可以通过按压屏幕时间的长短来控制这个「小人」跳跃的距离。可能刚开始上手的时候，因为时间距离之间的关系把握不恰当，只能跳出几个就掉到了台子下面。
玩法类似于《flappy bird》

![](https://ws1.sinaimg.cn/large/c3a916a7gy1fmxe4gnfhnj20hs0a0t8q.jpg)

**如果能精确测量出起始和目标点之间测距离，就可以估计按压的时间来精确跳跃？所以花2个小时写了一个python脚本进行验证**

希望不要把分数刷太高，容易没朋友的。。。

## 工具介绍

- Python 2.7
- Android 手机
- Adb 驱动
- Python Matplot绘图

如果你是`iOS`，请参考下面的配置：
- 使用真机调试wda，参考iOS 真机如何安装 [WebDriverAgent · TesterHome](https://testerhome.com/topics/7220)
- 安装[openatx/facebook-wda](https://github.com/openatx/facebook-wda)
- Python 3

## 依赖安装

``` bash
pip install -r requirements.txt
```

## 原理说明

1. 将手机点击到《跳一跳》小程序界面；
2. 用Adb 工具获取当前手机截图，并用adb将截图pull上来

```shell
    adb shell screencap -p /sdcard/1.png
    adb pull /sdcard/1.png .
```

3. 用matplot显示截图；
4. 用鼠标点击起始点和目标位置，计算像素距离；
5. 根据像素距离，计算按压时间；
6. 用Adb工具点击屏幕蓄力一跳；

```shell
    adb shell input swipe x y x y time
```

如果你是 `iOS`：
1. 运行安装好的 `WebDriverAgentRunner`
2. 将手机点击到《跳一跳》小程序界面
3. `python3 wechat_jump_iOS_py3.py`
4. 依次点击起始位置和目标位置，实现蓄力一跳
5. 打开 `python3 wechat_jump_iOS_py3.py`，根据蓄力一跳的精准情况更改其中的 `time_coefficient`，直到获得最佳取值

## 实验结果

![](https://ws1.sinaimg.cn/large/c3a916a7gy1fmxel5dkxvj20u01hcmzx.jpg)

## TODO 

可以对拉上来的图片进行颜色分割，识别小人和目标中心店，这样就不需要手动点击自动弹跳。
事实证明，机器人比人更会玩儿游戏。

