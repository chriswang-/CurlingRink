<template>
    <div class="container" ref="container" :style="{ width: laneWidthInPixel + 'px' }">
        <svg ref="trajectorySVG" :width="svgWidth" :height="svgHeight">
            <g ref="canvas">
                <curling-stone v-for="index in 2" :key="index" :ref="'curlingStone' + (index - 1)" :radius="8" color="#ff00f0" :hogLine1="hogLine1" :hogLine2="hogLine2" @zoom="dealZoom" @frameEnd="dealFrameEnd"></curling-stone>
            </g>
        </svg>
    </div>
</template>

<script>
import * as d3 from 'd3';
import CurlingStone from './CurlingStone.vue'


export default {
    components: {
        CurlingStone
    },
    props: {
        refName: {
            type: String,
            required: true
        },
        curlingNumer: {
            type: Number,
            required: true
        },
        settingLaneWidthInPixel: {
            type: Number,
            required: false
        },
        cameraEnable: {
            type: Boolean,
            required: true
        }
    },
    data() {
        return {
            shouldZoomIn: false,
            shouldZoomOut: false,
            // 场地信息, 单位米
            laneLengthInMeter: 44.5,
            laneWidthInMeter: 4.75,
            svgWidth: 0,
            svgHeight: 0,
            laneLengthInPixel: 0,
            laneWidthInPixel: 0,
            hogLine1: 0,
            hogLine2: 0,
        };
    },
    mounted() {
        this.trajectorySVG = d3.select(this.$refs.trajectorySVG)
        this.canvas = d3.select(this.$refs.canvas)

        this.calculateLaneDimensions();
        this.initSvg();
        this.drawLane();
    },
    methods: {

        calculateLaneDimensions() {

            // 设置了宽度参数就是常规模式, 宽度等于参数设定, 长度按照冰壶场地实际尺寸进行缩放
            if (this.settingLaneWidthInPixel) {
                this.laneWidthInPixel = this.settingLaneWidthInPixel
                this.laneLengthInPixel = this.laneWidthInPixel * (this.laneLengthInMeter / this.laneWidthInMeter);
            } else { // 没设置宽度参数就是预览模式, 缩略图, 长度等于100h, 宽度按照冰壶场地实际尺寸进行缩放
                this.laneLengthInPixel = this.$refs.container.clientHeight;
                this.laneWidthInPixel = this.laneLengthInPixel * (this.laneWidthInMeter / this.laneLengthInMeter);
            }

            this.hogLine1 = this.yScale(10); // hogLine 距离底部的距离 10米
            this.hogLine2 = this.laneLengthInPixel - this.yScale(10); // hogLine 距离底部的距离
        },
        initSvg() {
            this.svgWidth = this.laneWidthInPixel
            this.svgHeight = this.$refs.container.clientHeight;
            this.trajectorySVG.attr("viewBox", `0 0 ${this.svgWidth} ${this.svgHeight}`);
        },
        xScale(value) {
            return d3.scaleLinear().domain([0, this.laneWidthInMeter]).range([0, this.svgWidth])(value);
        },
        yScale(value) {
            return d3.scaleLinear().domain([0, this.laneLengthInMeter]).range([0, this.laneLengthInPixel])(value);
        },
        drawLane() {
            this.canvas.attr("class", "canvas")
                .attr("transform", `translate(${this.svgWidth}, ${this.svgHeight}) scale(-1, -1)`);

            const rect = this.canvas.insert("rect", ":first-child")
                .attr("fill", "#e9e9e9")
                .attr("x", 0)
                .attr("y", 0)
                .attr("stroke", "#333")
                .attr("width", this.laneWidthInPixel) // 设置矩形的宽度
                .attr("height", this.laneLengthInPixel); // 设置矩形的高度

            // Hog Line 1
            this.canvas.insert("line", () => rect.node().nextSibling)
                .attr("x1", 0)
                .attr("y1", this.hogLine1)
                .attr("x2", this.svgWidth)
                .attr("y2", this.hogLine1)
                .attr("stroke", "red")
                .attr("stroke-width", 1);

            // Hog Line 2
            this.canvas.insert("line", () => rect.node().nextSibling)
                .attr("x1", 0)
                .attr("y1", this.hogLine2)
                .attr("x2", this.svgWidth)
                .attr("y2", this.hogLine2)
                .attr("stroke", "green")
                .attr("stroke-width", 1);
        },

        // 被websocket接口回调
        playFrame(point, speed) {
            const pointTrans = { ...point }
            pointTrans.x = this.xScale(point.x)
            pointTrans.y = this.yScale(point.y)
            const curlingStone = this.$refs['curlingStone' + point.TagID]
            if (curlingStone) {
                curlingStone[0].interpolatePlayFrame(pointTrans, speed, null)
            }
        },

        // 用于轨迹回放
        replay(trajectoryData, speed) {
            console.log(this.refName, 'is replaying...')
            const tagIDs = trajectoryData.map(point => Number(point.TagID));
            const maxTagID = Math.max(...tagIDs);
            for (let i = 0; i < maxTagID + 1; i++) {
                const curlingTrajectoryData = trajectoryData.filter(point => point.TagID === String(i));
                const transformedTrajectoryData = curlingTrajectoryData.map(point => ({
                    ...point,
                    x: this.xScale(point.x),
                    y: this.yScale(point.y)
                }));
                const curlingStone = this.$refs['curlingStone' + i]
                if (curlingStone) {
                    curlingStone[0].replay(transformedTrajectoryData, speed)
                } else {
                    console.warn("坐标中指定的冰壶, 在页面中未被初始化!")
                }
            }

        },

        dealZoom(status) { // status= in , out
            if (!this.cameraEnable) return

            if (status == 'in') {
                this.canvas.attr("transform", `translate(${this.svgWidth - this.svgWidth / 4}, ${this.svgHeight / 2}) scale(-0.5, -0.5)`);
            } else {
                this.canvas.attr("transform", `translate(${this.svgWidth}, ${this.svgHeight}) scale(-1, -1)`);
            }
        },

        dealFrameEnd(stage, point) { // stage = inHogLines, beforeHogLine1, afterHogLine2
            if (!this.cameraEnable) return

            if (stage == 'inHogLines') {
                this.trajectorySVG.attr("viewBox", `0 ${-(point.y / 2)} ${this.svgWidth} ${this.svgHeight}`);
            } else if (stage == 'beforeHogLine1') {
                this.trajectorySVG.attr("viewBox", `0 0 ${this.svgWidth} ${this.svgHeight}`);
            } else {
                this.trajectorySVG.attr("viewBox", `0 ${this.svgHeight - this.laneLengthInPixel} ${this.svgWidth} ${this.svgHeight}`);
            }
        }
    }
};
</script>

<style scoped>
#app {
    display: flex;
    margin: 0;
}

.container {
    width: 100%;
    height: 100%;
    border: 1px dashed #9e9e9e;
}
</style>