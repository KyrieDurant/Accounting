<template>
	<view class="content">
		<view class="oneLayer">
			<div v-for="(item, index) in moneyType" :key="index" @click="selectType(index, item)"
				:class="typeColor == index ? 'btnBox' : 'btnBox1'">
				<div>{{ item.name }}</div>
			</div>
		</view>
		<view class="twoLayer">
			<div v-for="(item, index) in dateList" :key="index" @click="selectDate(index, item)"
				:class="dateColor == index ? 'btnBox' : 'btnBox1'">
				<div>{{ item.name }}</div>
			</div>
		</view>
		<view class="threeLayer">
			<scroll-view class="scroll-view_H" scroll-x="true" @scroll="scroll" scroll-left="0">
				<div v-for="(item, index) in timeList" :key="index" @click="selectTime(index, item)"
					:class="timeColor == index ? 'btnBox' : 'btnBox1'">
					<div>{{ item.name }}</div>
				</div>
			</scroll-view>
			<!-- <scroll-view scroll-x style="white-space: nowrap;">
				<view class="atimeBtn" v-for="(item, index) in items" :key="index">{{ item }}</view>
			</scroll-view> -->
		</view>
	</view>
</template>

<script setup>
	import {
		ref,
		onMounted
	} from 'vue';

	const moneyType = ref([{
			name: '支出',
		},
		{
			name: '收入',
		},
	])
	const typeColor = ref(0) // 改变css样式
	const defaultType = ref('支出') // 默认选择
	function selectType(e, item) {
		typeColor.value = e
		defaultType.value = item.name
	}

	const dateList = ref([{
			name: '周',
		},
		{
			name: '月',
		},
		{
			name: '年'
		}
	])

	const dateColor = ref(1) // 改变css样式
	const defaultDate = ref('月') // 默认选择
	function selectDate(e, item) {
		dateColor.value = e
		defaultDate.value = item.name
	}

	function scrool(e) {
		console.log('滑动', e)
	}

	const timeList = ref([{
			name: '2022-12',
		},
		{
			name: '2023-1',
		},
		{
			name: '2023-2'
		},
		{
			name: '2023-3',
		},
		{
			name: '2023-4',
		},
		{
			name: '2023-5'
		},
		{
			name: '2023-6',
		},
		{
			name: '2023-7',
		},
		{
			name: '2023-8'
		},
		{
			name: '2023-9',
		},
		{
			name: '2023-10',
		},
		{
			name: '2023-11'
		},
	])

	const timeColor = ref(1) // 改变css样式
	const defaultTime = ref('月') // 默认选择
	function selectTime(e, item) {
		timeColor.value = e
		defaultTime.value = item.name
	}

	const items = ref(['Item 1', 'Item 2', 'Item 3', 'Item 4', 'Item 5', 'Item 6', 'Item 7', 'Item 8', 'Item 9',
		'Item 10'
	])
</script>

<style lang="scss" scoped>
	page {
		background: #fdfdfd;
	}

	.content {
		width: 100%;
		display: flex;
		flex-direction: column;
		color: #313131;
	}

	.oneLayer {
		width: 100%;
		height: 80rpx;
		// background: #3ca0b4;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 30rpx;

		.btnBox {
			width: 180rpx;
			height: 100%;
			display: flex;
			justify-content: center;
			align-items: center;
			border-bottom: 6rpx solid #303e9f;

		}

		.btnBox1 {
			width: 180rpx;
			height: 100%;
			display: flex;
			justify-content: center;
			align-items: center;
		}
	}

	.twoLayer {
		width: 100%;
		height: 80rpx;
		// background: #3ca0b4;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 30rpx;
		margin-top: 20rpx;

		.btnBox {
			width: 130rpx;
			height: 64rpx;
			display: flex;
			justify-content: center;
			align-items: center;
			color: #fdfdfd;
			background: #303e9f;


		}

		.btnBox1 {
			width: 130rpx;
			height: 60rpx;
			display: flex;
			justify-content: center;
			align-items: center;
			border: 1rpx solid #303e9f;
		}
	}

	.threeLayer {
		height: 60rpx;
		display: flex;
		background: #efefef;
		margin-top: 20rpx;

		.scroll-view_H {
			white-space: nowrap;
			line-height: 60rpx;

			.btnBox {
				padding-right: 60rpx;
				height: 100%;
				display: inline-block;
				color: #303e9f;
			}

			.btnBox1 {
				padding-right: 60rpx;
				height: 100%;
				display: inline-block;
				coloe: #969696;
			}
		}
	}
</style>