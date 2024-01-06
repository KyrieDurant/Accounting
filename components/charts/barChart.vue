<!-- 条形图 -->
<template>
	<div class="container">
		<div :id="id" class="chart"></div>
	</div>
</template>
<script>
	const unwarp = (obj) => obj && (obj.__v_raw || obj.valueOf() || obj);
	export default {
		name: 'barChart',
		data() {
			return {
				id: `chart_${this.$.uid}`,
				barChart: null,
				// xAxisData: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24,
				// 		25, 26, 27, 28, 29, 30
				// 	],
				// chartData: [10, 20, 30, 35, 50, 40, 33, 15]
			};
		},
		props: {
			xAxisData: {
				type: Array,
				default: () => [],
			},
			chartData: {
				type: Array,
				default: () => [],
			},
		},
		watch: {
			xAxisData: {
				handler(newValue, oldValue) {
					// console.log("监听到了降雨量数据的变化", newValue);
					this.initEfficiencyCahrt();
				},
				deep: true
			}
		},

		mounted() {
			console.log(this.$.uid);
			console.log('子组件拿到', this.xAxisData);
			if (this.xAxisData) {
				this.initEfficiencyCahrt();
			}
		},
		methods: {
			initEfficiencyCahrt() {
				this.barChart = this.$echarts.getInstanceByDom(
					document.getElementById(this.id)
				);
				if (
					this.barChart != null &&
					this.barChart != "" &&
					this.barChart != undefined
				) {
					this.barChart.dispose();
				}
				this.barChart = this.$echarts.init(
					document.getElementById(this.id)
				);

				let option = {
					grid: {
						top: "23%",
						bottom: "0%",
						left: '2%',
						right: '5%',
						containLabel: true,
					},

					legend: {
						top: "3%",
						right: 13,
						icon: "roundRect",
						itemWidth: 13,
						itemHeight: 13,
						itemGap: 13,
						textStyle: {
							fontSize: 13,
							color: "#646464",
						},
					},

					tooltip: {
						trigger: "axis",
						axisPointer: {
							type: "line",
							lineStyle: {
								color: "rgba(113, 113, 113, 0)",
							},
						},
						textStyle: {
							color: "#646464",
							fontSize: 13,
						},
						backgroundColor: "rgba(25, 36, 62, 0.9)",
						borderColor: "transparent",
					},
					//             dataZoom: [
					// 	{ // 控制图表左右滑动
					//                 width: '3',
					//                 type: 'slider',
					//                 show: false, //flase直接隐藏图形
					//                 // xAxisIndex: [0],
					//                 left: 100, //滚动条靠左侧的百分比
					//                 bottom: 40,
					//                 height: 20,//组件高度  
					//                 start: 0,//滚动条的起始位置
					//                 showDataShadow: false,//是否显示数据阴影
					//                 showDetail: false,//是否显示想洗数值信息
					//                 end: 100 //滚动条的截止位置（按比例分割你的柱状图x轴长度）
					//             }, 
					// {
					//                 type: 'inside',
					//                 show: true,
					//                 xAxisIndex: [0],
					//                 start: 30,//滚动条的起始位置
					//                 end: 0.25 //滚动条的截止位置（按比例分割你的柱状图x轴长度）
					//             },
					// ],
					xAxis: {
						type: "category",
						axisLine: {
							show: true,
							lineStyle: {
								color: "rgba(117, 117, 117, 1.0)",
							},
						},
						splitLine: {
							show: false,
						},
						axisLabel: {
							fontSize: 13,
							color: "#646464",
						},
						axisTick: {
							show: false,
							alignWithLabel: true,
						},
						// boundaryGap: false,
						data: this.xAxisData,
					},
					yAxis: {
						name: '元',
						type: "value",
						min: 0,
						nameGap: '15',
						nameTextStyle: {
							color: "#646464",
							nameLocation: "start",
							padding: [0, 0, 0, -20],
							fontSize: 13
						},
						axisLine: {
							show: false,
						},
						splitLine: {
							show: true,
							lineStyle: {
								color: "rgba(140,140,140,0.3)",
								type: "dashed",
							},
						},
						axisLabel: {
							show: true,
							fontSize: 13,
							color: "#646464",
						},
						axisTick: {
							show: false,
						},
						minInterval: 1,
					},

					series: [{
						name: "收入",
						type: "bar",
						stack: "",
						barMaxWidth: 20,
						barGap: "10%",
						itemStyle: {
							color: {
								type: "linear",
								x: 0,
								y: 0,
								x2: 0,
								y2: 1,
								colorStops: [{
										offset: 0,
										color: "rgba(138, 162, 220, 1)", // 0% 处的颜色
									},
									{
										offset: 1,
										color: "rgba(79, 89, 131, 0)", // 100% 处的颜色
									},
								],
								global: false, // 缺省为 false
							},
						},
						data: this.chartData,
					}],
				};
				unwarp(this.barChart).setOption(option);
			},
		},
	}
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