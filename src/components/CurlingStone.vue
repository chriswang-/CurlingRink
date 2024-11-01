<template>
    <g>
        <circle ref="ball" :cx="x" :cy="y" :r="radius" :fill="color" />
    </g>
</template>

<script>
import * as d3 from 'd3';

export default {
    name: "CurlingStone",
    props: {
        x: {
            type: Number,
            required: true
        },
        y: {
            type: Number,
            required: true
        },
        radius: {
            type: Number,
            default: 8
        },
        color: {
            type: String,
            default: "#ff6347"
        },
        hogLine1: {
            type: Number,
            required: true,
        },
        hogLine2: {
            type: Number,
            required: true,
        },
    },
    mounted() {
        this.trajectoryDataCache = []
        this.ball = d3.select(this.$refs.ball)
            .attr("cx", (this.x))
            .attr("cy", (this.y))

        this.path = d3.select(this.ball.node().parentNode).append("path")
            .attr("fill", "none")
            .attr("stroke", this.color)
            .attr("stroke-width", 2);

        this.line = d3.line()
            .x(d => (d.x))
            .y(d => (d.y));
    },
    methods: {

        interpolatePlayFrame(point, replayCallback) {
            const previousPoint = this.trajectoryDataCache.at(-1);
            const interval = 30; // 每 20 ms 生成一个新位置点
            const steps = previousPoint ? Math.ceil((point.time - previousPoint.time) / interval) : 1;
            let i = 1;
            const interpolatePlayFrameCallback = () => {
                if (i > steps) {
                    if (replayCallback) replayCallback();
                    return;
                }
                const t = i / steps;
                const interpolatedX = d3.interpolate(previousPoint ? previousPoint.x : point.x, point.x)(t);
                const interpolatedY = d3.interpolate(previousPoint ? previousPoint.y : point.y, point.y)(t);
                i++;

                // 使用 playFrame 播放帧，并传递 interpolatePlayFrameCallback 继续循环
                this.playFrame({
                    x: interpolatedX,
                    y: interpolatedY,
                    time: previousPoint ? (previousPoint.time + 20 * i) : point.time,
                }, interpolatePlayFrameCallback);
            };

            // 开始启动插值动画
            interpolatePlayFrameCallback();
        },

        playFrame(point, callback) {

            console.log(point.x, point.y, point.time)
            const previousPoint = this.trajectoryDataCache.at(-1);
            let duration = 0;
            const delay = 13; // delay 8 个毫秒, 是的动画更加平顺

            if (previousPoint) {
                duration = point.time - previousPoint.time;
            }
            this.trajectoryDataCache.push(point);

            if (this.shouldZoomIn) {
                this.shouldZoomIn = false;
                this.$emit("zoom", "in")
            }
            if (this.shouldZoomOut) {
                this.shouldZoomOut = false;
                this.$emit("zoom", "out")
            }

            if ((point.y) > this.hogLine1 && (point.y) < this.hogLine2) {
                this.shouldZoomIn = true;
                this.ball
                    .transition()
                    .delay(delay)
                    .duration(duration - delay)
                    .ease(d3.easeCubicInOut)
                    .attr("cx", (point.x))
                    .attr("cy", (point.y))
                    .on("end", () => {
                        this.path
                            .datum(this.trajectoryDataCache).attr("d", this.line);

                        //视口往下跑, 坐标负数和小球应该相反
                        this.$emit("frameEnd", "inHogLines", point)

                        if (callback) callback();
                    });
            } else {
                this.shouldZoomOut = true;
                this.ball
                    .transition()
                    .delay(delay)
                    .duration(duration - delay)
                    .ease(d3.easeCubicInOut)
                    .attr("cx", (point.x))
                    .attr("cy", (point.y))
                    .on("end", () => {
                        this.path
                            .datum(this.trajectoryDataCache).attr("d", this.line);

                        //视口往下跑, 坐标负数和小球应该相反
                        if ((point.y) <= this.hogLine1) {
                            this.$emit("frameEnd", "beforeHogLine1")

                        } else {
                            this.$emit("frameEnd", "afterHogLine2")

                        }
                        if (callback) callback();
                    });
            }
        }
    }
};
</script>

<style scoped></style>
