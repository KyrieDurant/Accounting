<!-- 折线图 -->
<template>
	<div class="container">
		<div ref="roseChart" class="chart"></div>
	</div>
</template>
<script setup>
	import {
		watch,
		ref,
		reactive,
		toRefs,
		computed,
		onMounted,
		nextTick,
		onBeforeUnmount,
		getCurrentInstance,
	} from "vue";
	import * as echarts from "echarts";
	const unwarp = (obj) => obj && (obj.__v_raw || obj.valueOf() || obj);
	const {
		proxy
	} = getCurrentInstance();

	// const props = defineProps({
	//     xAxisData: {
	//         type: Array,
	//         default: () => []
	//     },
	//     seriesData: {
	//         type: Array,
	//         default: () => []
	//     }
	// })
	// // 使用父组件传过来的值
	// const { xAxisData } = toRefs(props)
	// const { seriesData } = toRefs(props)
	// console.log('折线图父组件传过来的值----', xAxisData, seriesData);

	// watch(() => [props.xAxisData], (newValue, oldValue) => {
	//     console.log('重新获取数据🚀~~~', newValue);
	//     initChart()
	// },)

	let data = reactive({
		lPie1: null,
	});

	const roseData = ref([{
			value: 40,
			name: '娱乐'
		},
		{
			value: 33,
			name: '医疗'
		},
		{
			value: 28,
			name: '水果'
		},
		{
			value: 22,
			name: '交通'
		},
		{
			value: 20,
			name: '通讯'
		},
		{
			value: 15,
			name: '日用品'
		},
		{
			value: 12,
			name: '买菜'
		},
		{
			value: 10,
			name: '旅游'
		},
		{
			value: 20,
			name: '游戏'
		},
		{
			value: 60,
			name: '餐饮'
		}
	])

	const colors = ref([
		'#9fe6b8',
		'#32c5e9',
		'#5eb5fc',
		'#1d9dff',
		'#8378ea',
		'#aa6eff',
		'#e7bcf3',
		'#fb7293',
		'#ff9f7f',
		'#ffdb5c'
	]);


	const initChart = () => {
		data.lPie1 = proxy.$echarts.getInstanceByDom(proxy.$refs.roseChart)
		if (data.lPie1 != null && data.lPie1 != "" && data.lPie1 != undefined) {
			data.lPie1.dispose();
		}

		data.lPie1 = proxy.$echarts.init(proxy.$refs.roseChart);

		for (let i = 0; i < roseData.value.length; i++) {
			roseData.value[i].itemStyle = {
				color: colors.value[i]
			};
		}

		const originDataLen = roseData.value.length;
		const spanAngle = 180; // 需要显示的角度
		const repeatedMultiple = 360 / spanAngle;
		// 这里根据要显示的角度 计算了需要插入的数据量
		const addDataLen = parseInt((repeatedMultiple - 1) * originDataLen);
		for (let index = 0; index < addDataLen; index++) {
			roseData.value.push({
				name: null,
				// 这里给数据置零，即在视觉上不显示
				value: 0,
				// 这里保证了异常情况下(数据都为0时)作为占位的数据在视觉上仍为不可见状态。
				itemStyle: {
					color: 'rgba(0,0,0,0)'
				},
				tooltip: {
					show: true,
					formatter: null
				}
			});
		}

		let option = {
			// backgroundColor: '#767676',
			"color": colors.value,
			"series": [{
					"name": "面积模式",
					"type": "pie",
					"roseType": "area",
					"radius": [
						"20%",
						"110%"
					],
					"center": [
						"50%",
						"80%"
					],
					"startAngle": 180,
					"label": {
						"show": true
					},
					"data": roseData.value
				},
				{
					type: 'gauge',
					radius: '110%',
					center: ['50%', '90%'],
					startAngle: 180,
					endAngle: 0,
					min: 0,
					max: 1,
					splitNumber: 20,
					axisLine: {
						show: false,
						lineStyle: {
							width: 1,
							color: [
								[1, '#5bdf22']
							]
						}
					},
					axisTick: {
						show: false,
						length: 18,
						lineStyle: {
							color: 'auto',
							width: 1
						}
					},
					splitLine: {
						length: '0',
						lineStyle: {
							color: 'auto',
							width: 1
						}
					},
					// 外边文字显示,color设置与背景颜色相同时不显示
					axisLabel: {
						color: '#fdfdfd',
						fontSize: 14,
						distance: -85,
						// lineHeight: 25,
						height: 50,
						formatter: function(value) {
							if (value === 0.05) {
								return '餐饮';
							} else if (value === 0.15) {
								return '交通';
							} else if (value === 0.25) {
								return '通讯';
							} else if (value === 0.35) {
								return '水电';
							} else if (value === 0.45) {
								return '日用品';
							} else if (value === 0.55) {
								return '买菜';
							} else if (value === 0.65) {
								return '娱乐';
							} else if (value === 0.75) {
								return '旅游';
							} else if (value === 0.85) {
								return '游戏';
							} else if (value === 0.95) {
								return '维修';
							}
						}
					},
					"type": "gauge",
					"radius": "100%",
					"center": [
						"50%",
						"97%"
					],
					title: {
						offsetCenter: [0, '-20%'],
						fontSize: 30
					},
					detail: {
						fontSize: 50,
						offsetCenter: [0, '0%'],
						color: 'auto'
					},
					data: []
				},
				// 虚线
				{
					"type": "gauge",
					"radius": "110%",
					// "radius": "0%",
					"center": [
						"50%",
						"80%"
					],
					"startAngle": 180,
					"endAngle": 0,
					"min": 0,
					"max": 1,
					"z": 3,
					"splitNumber": 10,
					"axisLine": {
						"show": false,
						"lineStyle": {
							"width": 1,
							"color": [
								[
									1,
									"#dd0a69"
								]
							]
						}
					},
					"axisTick": {
						"show": false
					},
					"splitLine": {
						"distance": 0,
						"length": "81%",
						"lineStyle": {
							"type": "dashed",
							"color": "#ab24cc",
							"opacity": 0.5,
							"width": 1
						}
					},
					"axisLabel": {
						"show": false,

					},
					"data": []
				},
				{
					"type": "gauge",
					"radius": "110%",
					"center": [
						"50%",
						"80%"
					],
					"startAngle": 180,
					"endAngle": 0,
					"min": 0,
					"max": 1,
					"z": 3,
					"splitNumber": 10,
					"axisLine": {
						show: false,
						"lineStyle": {
							"width": 1,
							"opacity": "0.5",
							"color": [
								[
									1,
									"red"
								]
							]
						}
					},
					"axisTick": {
						"show": false
					},
					"splitLine": {
						"show": false
					},
					"axisLabel": {
						"show": true,
						distance: -30,
						opacity: 0.6,
						formatter: function(params) {
							var value = params.toFixed(2)
							let val = 40
							if (value == 0.00) {
								return `{value|${val}}`
							} else if (value == 1.00) {
								return `{value|${val}}`
							} else {
								return ''
							}
						},
						rich: {
							value: {
								padding: [20, 0, 0, 0],
								color: '#2bc1bc',
								opacity: 0.6,
							}
						}
					},
					"data": []
				},
				{
					"type": "gauge",
					"radius": "88%",
					"center": [
						"50%",
						"80%"
					],
					"startAngle": 180,
					"endAngle": 0,
					"min": 0,
					"max": 1,
					"z": 3,
					"splitNumber": 10,
					"axisLine": {
						"lineStyle": {
							"width": 1,
							"opacity": "0.5",
							"color": [
								[
									1,
									"#6c21c1"
								]
							]
						}
					},
					"axisTick": {
						"show": false
					},
					"splitLine": {
						"show": false
					},
					"axisLabel": {
						"show": false,
					},
					"detail": {
						"fontSize": 50,
						"offsetCenter": [
							0,
							"0%"
						],
						"valueAnimation": true,
						"color": "auto"
					},
					"data": []
				},
				{
					"type": "gauge",
					"radius": "110%",
					"center": [
						"50%",
						"80%"
					],
					"startAngle": 180,
					"endAngle": 0,
					"min": 0,
					"max": 1,
					"z": 3,
					"splitNumber": 10,
					"axisLine": {
						"lineStyle": {
							"width": 1,
							"opacity": "0.5",
							"color": [
								[
									1,
									"#23c280"
								]
							]
						}
					},
					"axisTick": {
						"show": false
					},
					"splitLine": {
						"show": false
					},
					"axisLabel": {
						"show": false,
						distance: -25,
						color: '#767676',

					},
					"detail": {
						"fontSize": 50,
						"offsetCenter": [
							0,
							"0%"
						],
						"valueAnimation": true,
						"color": "auto"
					},
					"data": []
				},
				{
					"type": "gauge",
					"radius": "66%",
					"center": [
						"50%",
						"80%"
					],
					"startAngle": 180,
					"endAngle": 0,
					"min": 0,
					"max": 1,
					"z": 3,
					"splitNumber": 10,
					"axisLine": {
						"lineStyle": {
							"width": 1,
							"opacity": "0.5",
							"color": [
								[
									1,
									"#982cf0"
								]
							]
						}
					},
					"axisTick": {
						"show": false
					},
					"splitLine": {
						"show": false
					},
					"axisLabel": {
						"show": true,
						distance: -25,
						color: '#767676',
						formatter: function(params) {
							var value = params.toFixed(2)
							let val = 20
							if (value == 0.00) {
								return `{value|${val}}`
							} else if (value == 1.00) {
								return `{value|${val}}`
							} else {
								return ''
							}
						},
						rich: {
							value: {
								padding: [20, 0, 0, 0],
								color: '#767676',
								opacity: 0.6,
							}
						}
					},
					"data": []
				},
				{
					"type": "gauge",
					"radius": "45%",
					"center": [
						"50%",
						"80%"
					],
					"startAngle": 180,
					"endAngle": 0,
					"min": 0,
					"max": 1,
					"z": 3,
					"splitNumber": 10,
					"axisLine": {
						"lineStyle": {
							"width": 1,
							"opacity": "0.5",
							"color": [
								[
									1,
									"#767676"
								]
							]
						}
					},
					"axisTick": {
						"show": false
					},
					"splitLine": {
						"show": false
					},
					"axisLabel": {
						"show": false
					},
					"data": []
				},
				{
					"type": "gauge",
					"radius": "20%",
					"center": [
						"50%",
						"80%"
					],
					"startAngle": 180,
					"endAngle": 0,
					"min": 0,
					"max": 1,
					"z": 3,
					"splitNumber": 10,
					"axisLine": {
						"lineStyle": {
							"width": 1,
							"opacity": "0.5",
							"color": [
								[
									1,
									"#767676"
								]
							]
						}
					},
					"axisTick": {
						"show": false
					},
					"splitLine": {
						"show": false
					},
					"axisLabel": {
						"show": true,
						distance: -20,
						color: '#767676',
						formatter: function(params) {
							var value = params.toFixed(2)
							let val = 0
							if (value == 0.00) {
								return `{value|${val}}`
							} else if (value == 1.00) {
								return `{value|${val}}`
							} else {
								return ''
							}
						},
						rich: {
							value: {
								padding: [20, 0, 0, 0],
								color: '#767676',
								opacity: 0.6,
							}
						}
					},
					"data": []
				}
			]
		}

		unwarp(data.lPie1).setOption(option)

	}

	onMounted(() => {
		initChart()
	});
</script>

<style scoped>
	.container {
		width: 750rpx;
		height: 350rpx;
	}

	.chart {
		width: 100%;
		height: 100%;
	}
</style>