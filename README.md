# binghu3

## Project setup
```
npm install
npm install d3
npm run serve
```

## CurlingLane 冰壶赛道

1. 轨迹重放 speed为0, 将恢复轨迹最后状态
this.$refs.curlingLane.replay(trajectory, speed)

2. 接收websocket坐标点, 在websocket消息收听函数中调用下面API
this.$refs.curlingLane.playFrame(point, speed)

3. 标签说明
* curlingNumber 小球数量
* settingLaneWidthInPixel 轨道宽度设定, 轨道长度自动等比计算
* settingLaneWidthInPixel 如果不设置, 将会开启预览模式, 届时, 轨道长度等于100vh, 宽度自动等比计算
* 是否使用摄像头,进行小球跟踪和缩放等功能. 

<curling-lane ref="curlingLane0" refName="curlingLane0" :curlingNumer=16 :settingLaneWidthInPixel=300 :cameraEnable="true"></curling-lane>

