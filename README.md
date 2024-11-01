# binghu3

## Project setup
```
npm install
npm install d3
npm run serve
```

## 播放一整条轨迹

 <CurlingRink ref="curlingRink" rinkWidthInPixel="300"></CurlingRink>
this.$refs.curlingRink.replay(trajectory)

## 接收websocket消息, 每次收到一个坐标点

 <CurlingRink ref="curlingRink" rinkWidthInPixel="300"></CurlingRink>
this.$refs.curlingRink.payFrame(point)