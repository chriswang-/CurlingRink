<template>
  <div id="app">
    <div id="preview">
      <curling-lane ref="curlingLane0" refName="curlingLane0" :curlingNumer=16 :settingLaneWidthInPixel=300 :cameraEnable="true"></curling-lane>
      <curling-lane ref="curlingLane1" refName="curlingLane1" :curlingNumer=16 :settingLaneWidthInPixel=300 :cameraEnable="true"></curling-lane>
      <curling-lane ref="curlingLane2" refName="curlingLane2" :curlingNumer=16 :settingLaneWidthInPixel=300 :cameraEnable="true"></curling-lane>
      <curling-lane ref="curlingLane3" refName="curlingLane3" :curlingNumer=16 :settingLaneWidthInPixel=300 :cameraEnable="true"></curling-lane>
      <curling-lane ref="curlingLane4" refName="curlingLane4" :curlingNumer=16 :cameraEnable="false"></curling-lane>
    </div>
    <div id="main"></div>
  </div>
</template>

<script>
import CurlingLane from './components/CurlingLane.vue'

export default {
  name: 'App',
  components: {
    CurlingLane
  },
  data() {
    return {
      trajectoryData: [{ "time": 100, "x": 2.376, "y": 0.499 }, { "time": 200, "x": 2.381, "y": 0.996 }, { "time": 300, "x": 2.388, "y": 1.491 }, { "time": 400, "x": 2.398, "y": 1.984 }, { "time": 500, "x": 2.41, "y": 2.475 }, { "time": 600, "x": 2.425, "y": 2.964 }, { "time": 700, "x": 2.441, "y": 3.451 }, { "time": 800, "x": 2.459, "y": 3.936 }, { "time": 900, "x": 2.477, "y": 4.419 }, { "time": 1000, "x": 2.497, "y": 4.9 }, { "time": 1100, "x": 2.517, "y": 5.379 }, { "time": 1200, "x": 2.537, "y": 5.856 }, { "time": 1300, "x": 2.556, "y": 6.331 }, { "time": 1400, "x": 2.575, "y": 6.804 }, { "time": 1500, "x": 2.592, "y": 7.275 }, { "time": 1600, "x": 2.607, "y": 7.744 }, { "time": 1700, "x": 2.621, "y": 8.211 }, { "time": 1800, "x": 2.632, "y": 8.676 }, { "time": 1900, "x": 2.64, "y": 9.139 }, { "time": 2000, "x": 2.646, "y": 9.6 }, { "time": 2100, "x": 2.648, "y": 10.059 }, { "time": 2200, "x": 2.647, "y": 10.516 }, { "time": 2300, "x": 2.642, "y": 10.971 }, { "time": 2400, "x": 2.634, "y": 11.424 }, { "time": 2500, "x": 2.622, "y": 11.875 }, { "time": 2600, "x": 2.607, "y": 12.324 }, { "time": 2700, "x": 2.587, "y": 12.771 }, { "time": 2800, "x": 2.565, "y": 13.216 }, { "time": 2900, "x": 2.538, "y": 13.659 }, { "time": 3000, "x": 2.509, "y": 14.1 }, { "time": 3100, "x": 2.476, "y": 14.539 }, { "time": 3200, "x": 2.441, "y": 14.976 }, { "time": 3300, "x": 2.402, "y": 15.411 }, { "time": 3400, "x": 2.362, "y": 15.844 }, { "time": 3500, "x": 2.32, "y": 16.275 }, { "time": 3600, "x": 2.276, "y": 16.704 }, { "time": 3700, "x": 2.231, "y": 17.131 }, { "time": 3800, "x": 2.185, "y": 17.556 }, { "time": 3900, "x": 2.138, "y": 17.979 }, { "time": 4000, "x": 2.092, "y": 18.4 }, { "time": 4100, "x": 2.046, "y": 18.819 }, { "time": 4200, "x": 2.001, "y": 19.236 }, { "time": 4300, "x": 1.957, "y": 19.651 }, { "time": 4400, "x": 1.914, "y": 20.064 }, { "time": 4500, "x": 1.874, "y": 20.475 }, { "time": 4600, "x": 1.836, "y": 20.884 }, { "time": 4700, "x": 1.801, "y": 21.291 }, { "time": 4800, "x": 1.769, "y": 21.696 }, { "time": 4900, "x": 1.74, "y": 22.099 }, { "time": 5000, "x": 1.715, "y": 22.5 }, { "time": 5100, "x": 1.694, "y": 22.899 }, { "time": 5200, "x": 1.677, "y": 23.296 }, { "time": 5300, "x": 1.665, "y": 23.691 }, { "time": 5400, "x": 1.656, "y": 24.084 }, { "time": 5500, "x": 1.653, "y": 24.475 }, { "time": 5600, "x": 1.654, "y": 24.864 }, { "time": 5700, "x": 1.66, "y": 25.251 }, { "time": 5800, "x": 1.671, "y": 25.636 }, { "time": 5900, "x": 1.687, "y": 26.019 }, { "time": 6000, "x": 1.707, "y": 26.4 }, { "time": 6100, "x": 1.732, "y": 26.779 }, { "time": 6200, "x": 1.762, "y": 27.156 }, { "time": 6300, "x": 1.796, "y": 27.531 }, { "time": 6400, "x": 1.834, "y": 27.904 }, { "time": 6500, "x": 1.877, "y": 28.275 }, { "time": 6600, "x": 1.923, "y": 28.644 }, { "time": 6700, "x": 1.972, "y": 29.011 }, { "time": 6800, "x": 2.025, "y": 29.376 }, { "time": 6900, "x": 2.081, "y": 29.739 }, { "time": 7000, "x": 2.14, "y": 30.1 }, { "time": 7100, "x": 2.201, "y": 30.459 }, { "time": 7200, "x": 2.264, "y": 30.816 }, { "time": 7300, "x": 2.329, "y": 31.171 }, { "time": 7400, "x": 2.395, "y": 31.524 }, { "time": 7500, "x": 2.463, "y": 31.875 }, { "time": 7600, "x": 2.531, "y": 32.224 }, { "time": 7700, "x": 2.599, "y": 32.571 }, { "time": 7800, "x": 2.667, "y": 32.916 }, { "time": 7900, "x": 2.735, "y": 33.259 }, { "time": 8000, "x": 2.801, "y": 33.6 }, { "time": 8100, "x": 2.867, "y": 33.939 }, { "time": 8200, "x": 2.932, "y": 34.276 }, { "time": 8300, "x": 2.994, "y": 34.611 }, { "time": 8400, "x": 3.055, "y": 34.944 }, { "time": 8500, "x": 3.113, "y": 35.275 }, { "time": 8600, "x": 3.169, "y": 35.604 }, { "time": 8700, "x": 3.221, "y": 35.931 }, { "time": 8800, "x": 3.271, "y": 36.256 }, { "time": 8900, "x": 3.317, "y": 36.579 }, { "time": 9000, "x": 3.36, "y": 36.9 }, { "time": 9100, "x": 3.399, "y": 37.219 }, { "time": 9200, "x": 3.434, "y": 37.536 }, { "time": 9300, "x": 3.465, "y": 37.851 }, { "time": 9400, "x": 3.492, "y": 38.164 }, { "time": 9500, "x": 3.515, "y": 38.475 }, { "time": 9600, "x": 3.533, "y": 38.784 }, { "time": 9700, "x": 3.547, "y": 39.091 }, { "time": 9800, "x": 3.557, "y": 39.396 }, { "time": 9900, "x": 3.562, "y": 39.699 }],
      trajectoryData1: [{ 'time': 100, 'x': 2.376, 'y': 0.499 },
      { 'time': 200, 'x': 2.388, 'y': 0.911 },
      { 'time': 300, 'x': 2.4, 'y': 1.324 },
      { 'time': 400, 'x': 2.412, 'y': 1.735 },
      { 'time': 500, 'x': 2.425, 'y': 2.148 },
      { 'time': 600, 'x': 2.437, 'y': 2.56 },
      { 'time': 700, 'x': 2.448, 'y': 2.966 },
      { 'time': 800, 'x': 2.461, 'y': 3.375 },
      { 'time': 900, 'x': 2.473, 'y': 3.794 },
      { 'time': 1000, 'x': 2.485, 'y': 4.196 },
      { 'time': 1100, 'x': 2.497, 'y': 4.61 },
      { 'time': 1200, 'x': 2.509, 'y': 5.026 },
      { 'time': 1300, 'x': 2.521, 'y': 5.43 },
      { 'time': 1400, 'x': 2.533, 'y': 5.828 },
      { 'time': 1500, 'x': 2.546, 'y': 6.238 },
      { 'time': 1600, 'x': 2.557, 'y': 6.663 },
      { 'time': 1700, 'x': 2.57, 'y': 7.073 },
      { 'time': 1800, 'x': 2.582, 'y': 7.45 },
      { 'time': 1900, 'x': 2.594, 'y': 7.879 },
      { 'time': 2000, 'x': 2.606, 'y': 8.294 },
      { 'time': 2100, 'x': 2.618, 'y': 8.678 },
      { 'time': 2200, 'x': 2.629, 'y': 9.105 },
      { 'time': 2300, 'x': 2.643, 'y': 9.489 },
      { 'time': 2400, 'x': 2.653, 'y': 9.893 },
      { 'time': 2500, 'x': 2.666, 'y': 10.335 },
      { 'time': 2600, 'x': 2.679, 'y': 10.742 },
      { 'time': 2700, 'x': 2.691, 'y': 11.127 },
      { 'time': 2800, 'x': 2.702, 'y': 11.544 },
      { 'time': 2900, 'x': 2.715, 'y': 11.946 },
      { 'time': 3000, 'x': 2.726, 'y': 12.322 },
      { 'time': 3100, 'x': 2.74, 'y': 12.732 },
      { 'time': 3200, 'x': 2.75, 'y': 13.145 },
      { 'time': 3300, 'x': 2.762, 'y': 13.551 },
      { 'time': 3400, 'x': 2.774, 'y': 13.945 },
      { 'time': 3500, 'x': 2.788, 'y': 14.363 },
      { 'time': 3600, 'x': 2.8, 'y': 14.763 },
      { 'time': 3700, 'x': 2.81, 'y': 15.197 },
      { 'time': 3800, 'x': 2.825, 'y': 15.549 },
      { 'time': 3900, 'x': 2.837, 'y': 15.988 },
      { 'time': 4000, 'x': 2.849, 'y': 16.384 },
      { 'time': 4100, 'x': 2.862, 'y': 16.783 },
      { 'time': 4200, 'x': 2.87, 'y': 17.178 },
      { 'time': 4300, 'x': 2.885, 'y': 17.57 },
      { 'time': 4400, 'x': 2.896, 'y': 18.004 },
      { 'time': 4500, 'x': 2.907, 'y': 18.406 },
      { 'time': 4600, 'x': 2.922, 'y': 18.809 },
      { 'time': 4700, 'x': 2.931, 'y': 19.206 },
      { 'time': 4800, 'x': 2.945, 'y': 19.589 },
      { 'time': 4900, 'x': 2.959, 'y': 20.013 },
      { 'time': 5000, 'x': 2.968, 'y': 20.402 },
      { 'time': 5100, 'x': 2.983, 'y': 20.8 },
      { 'time': 5200, 'x': 2.996, 'y': 21.169 },
      { 'time': 5300, 'x': 3.005, 'y': 21.583 },
      { 'time': 5400, 'x': 3.018, 'y': 21.961 },
      { 'time': 5500, 'x': 3.029, 'y': 22.409 },
      { 'time': 5600, 'x': 3.042, 'y': 22.764 },
      { 'time': 5700, 'x': 3.052, 'y': 23.188 },
      { 'time': 5800, 'x': 3.066, 'y': 23.601 },
      { 'time': 5900, 'x': 3.075, 'y': 23.973 },
      { 'time': 6000, 'x': 3.092, 'y': 24.393 },
      { 'time': 6100, 'x': 3.099, 'y': 24.802 },
      { 'time': 6200, 'x': 3.113, 'y': 25.19 },
      { 'time': 6300, 'x': 3.126, 'y': 25.591 },
      { 'time': 6400, 'x': 3.137, 'y': 25.974 },
      { 'time': 6500, 'x': 3.15, 'y': 26.383 },
      { 'time': 6600, 'x': 3.164, 'y': 26.786 },
      { 'time': 6700, 'x': 3.174, 'y': 27.142 },
      { 'time': 6800, 'x': 3.19, 'y': 27.566 },
      { 'time': 6900, 'x': 3.197, 'y': 27.927 },
      { 'time': 7000, 'x': 3.208, 'y': 28.366 },
      { 'time': 7100, 'x': 3.225, 'y': 28.739 },
      { 'time': 7200, 'x': 3.237, 'y': 29.118 },
      { 'time': 7300, 'x': 3.248, 'y': 29.507 },
      { 'time': 7400, 'x': 3.261, 'y': 29.905 },
      { 'time': 7500, 'x': 3.269, 'y': 30.327 },
      { 'time': 7600, 'x': 3.283, 'y': 30.695 },
      { 'time': 7700, 'x': 3.295, 'y': 31.109 },
      { 'time': 7800, 'x': 3.307, 'y': 31.505 },
      { 'time': 7900, 'x': 3.319, 'y': 31.896 },
      { 'time': 8000, 'x': 3.335, 'y': 32.279 },
      { 'time': 8100, 'x': 3.343, 'y': 32.689 },
      { 'time': 8200, 'x': 3.358, 'y': 33.082 },
      { 'time': 8300, 'x': 3.366, 'y': 33.47 },
      { 'time': 8400, 'x': 3.379, 'y': 33.841 },
      { 'time': 8500, 'x': 3.389, 'y': 34.238 },
      { 'time': 8600, 'x': 3.402, 'y': 34.645 },
      { 'time': 8700, 'x': 3.418, 'y': 35.017 },
      { 'time': 8800, 'x': 3.433, 'y': 35.417 },
      { 'time': 8900, 'x': 3.443, 'y': 35.796 },
      { 'time': 9000, 'x': 3.455, 'y': 36.189 },
      { 'time': 9100, 'x': 3.468, 'y': 36.592 },
      { 'time': 9200, 'x': 3.473, 'y': 36.969 },
      { 'time': 9300, 'x': 3.491, 'y': 37.372 },
      { 'time': 9400, 'x': 3.505, 'y': 37.76 },
      { 'time': 9500, 'x': 3.517, 'y': 38.147 },
      { 'time': 9600, 'x': 3.523, 'y': 38.531 },
      { 'time': 9700, 'x': 3.533, 'y': 38.921 },
      { 'time': 9800, 'x': 3.553, 'y': 39.311 },
      { 'time': 9900, 'x': 3.558, 'y': 39.699 }]
    }
  },
  mounted() {

    const unitedTrajectories = this.mergeTrajectories(this.trajectoryData, this.trajectoryData1)
    console.log(unitedTrajectories.time, unitedTrajectories.x, unitedTrajectories.y)
    this.$refs.curlingLane0.replay(unitedTrajectories, 1)
    this.$refs.curlingLane1.replay(unitedTrajectories, 0.001)
    this.$refs.curlingLane2.replay(unitedTrajectories, 2)
    this.$refs.curlingLane3.replay(unitedTrajectories, 0.5)
    this.$refs.curlingLane4.replay(unitedTrajectories, 1)
  },
  methods: {

    // 这是一个临时函数, 用于把两个不同的轨迹 merge 合并到一起
    mergeTrajectories(trajectory1, trajectory2) {
      const mergedTrajectory = [];

      const totalLength = Math.max(trajectory1.length, trajectory2.length);

      // 记录当前时间
      let currentTime = 0;
      for (let i = 0; i < totalLength; i++) {
        if (i < trajectory1.length) {
          currentTime += 50; 
          mergedTrajectory.push({ ...trajectory1[i], time: currentTime, TagID: '0' });
        }
        if (i < trajectory2.length) {
          currentTime += 50; 
          mergedTrajectory.push({ ...trajectory2[i], time: currentTime, TagID: '1' });
        }
      }

      return mergedTrajectory;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  display: flex;
  margin: 0;
}

#preview {
  height: 100vh;

  background-color: #f0f0f0;
  border-right: 2px solid #333;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

#main {
  flex: 1;
}
</style>
