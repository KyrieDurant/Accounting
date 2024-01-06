<!--
 * @Author       : DESKTOP-09EM7KP\yao
 * @Date         : 2023-06-16 15:46:06
 * @LastEditors  : DESKTOP-09EM7KP\yao
 * @LastEditTime : 2023-06-25 17:28:23
 * @FilePath     : \nanxun-town-digital-management\src\components\common\CircularPieChart.vue
 * @Description  : 环状饼图
-->
<template>
	<div class="container">
		<div :id="id" class="chart"></div>
	</div>
</template>

<script>
	const unwarp = (obj) => obj && (obj.__v_raw || obj.valueOf() || obj);
	export default {
		name: "CircularPieChart",
		props: {
			chartData: {
				type: Array,
				default: () => [],
				require: true,
			},
			colors: {
				type: Array,
				default: () => [],
				require: true,
			},
			// 图标距离图形的距离
			legendLocation: {
				type: Object,
				default: () => {
					right: '10%';
					bottom: '10%'
				},
				require: true,
			},
			// 进度百分比
		},
		data() {
			return {
				id: `chart_${this.$.uid}`,
				circleProgressChart: null,
			};
		},
		mounted() {
			console.log(this.$.uid);
			this.initEfficiencyCahrt();
		},
		watch: {
			chartData(newCount, oldCount) {
				// console.log('饼状图数据变化了~',newCount)
				this.initEfficiencyCahrt();
			}
		},
		methods: {
			hexToRgba(hex, opacity) {
				return (
					"rgba(" +
					parseInt("0x" + hex.slice(1, 3)) +
					"," +
					parseInt("0x" + hex.slice(3, 5)) +
					"," +
					parseInt("0x" + hex.slice(5, 7)) +
					"," +
					opacity +
					")"
				);
			},
			initEfficiencyCahrt() {
				this.circleProgressChart = this.$echarts.getInstanceByDom(
					document.getElementById(this.id)
				);

				if (
					this.circleProgressChart != null &&
					this.circleProgressChart != "" &&
					this.circleProgressChart != undefined
				) {
					this.circleProgressChart.dispose();
				}
				this.circleProgressChart = this.$echarts.init(
					document.getElementById(this.id)
				);

				let legends = [],
					color1 = [],
					color2 = [];

				// 设置每层圆环颜色和添加间隔的透明色
				this.colors.forEach((item) => {
					color1.push(item, "transparent");
					color2.push(this.hexToRgba(item, 0.3), "transparent");
				});

				let data1 = [];
				let sum = 0;
				// 根据总值设置间隔值大小
				this.chartData.forEach((item) => {
					legends.push(item.name);
					sum += Number(item.value);
				});
				// 给每个数据后添加特定的透明的数据形成间隔
				this.chartData.forEach((item) => {
					if (item.value !== 0) {
						data1.push(item, {
							name: "",
							value: sum * 0.01,
							tooltip: {
								show: false,
							},
							label: {
								show: false,
							},
							// itemStyle: {
							//   color: "transparent",
							// },
						});
					}
				});

				let option = {
					tooltip: {
						show: true,
						backgroundColor: "rgba(37, 31, 18, 0.8)",
						borderWidth: 0,
						textStyle: {
							color: "#7a7a7a",
							fontFamily: "Alibaba PuHuiTi",
							fontWeight: 400,
							fontSize: 13,
						},
					},

					legend: [{
						orient: "vertical",
						data: legends,
						right: this.legendLocation.right,
						bottom: this.legendLocation.bottom,
						itemWidth: 1,
						itemHeight: 1,
						textStyle: {
							color: "#7a7a7a",
							fontSize: 13,
						},
						// itemGap: 5, //间距
					}, ],

					series: [
						// 最外层圆环
						{
							type: "pie",
							radius: ["63%", "70%"],
							center: ["30%", "50%"],
							startAngle: 90,
							selectedMode: "single",
							selectedOffset: 0,
							itemStyle: {
								color: (params) => {
									return color1[params.dataIndex];
								},
							},
							label: {
								show: false,
							},

							data: data1,
						},
						{
							type: "pie",
							radius: ["45%", "70%"],
							center: ["30%", "50%"],
							startAngle: 90,
							selectedMode: "single",
							selectedOffset: 0,
							itemStyle: {
								color: (params) => {
									return color2[params.dataIndex];
								},
							},
							label: {
								show: false,
							},
							data: data1,
						},
					],
				};

				unwarp(this.circleProgressChart).setOption(option);
			},
		},
	};
</script>

<style scoped>
	.container {
		width: 100%;
		height: 100%;
	}

	.chart {
		width: 100%;
		height: 100%;
	}
</style>