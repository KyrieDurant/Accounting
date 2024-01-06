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
		</view>
		<view class="fourLayer">
			<view class="chartBox"></view>
			<view class="minTitle">支出占比</view>
			<view class="chartBox1"></view>
			<view class="minTitle">支出排行</view>
			<view class="getMoney">
				<view class="codeBox" v-for="(item,index) in timeData" :key="index">
					<view class="leftCont">
						<view class="costImg">
							<image src="../../static/image/bill/account-book.png" mode="aspectFit"
								style=" width: 60rpx;">
							</image>
						</view>
						<view class="costCont">
							<span class="contType">{{item.type}}</span>
							<span class="contDetile">{{item.detile}}</span>
						</view>
					</view>
					<span style="padding-right: 2%;">{{ item.money }}</span>
				</view>
			</view>
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

	const timeData = ref([{
			showImg: '',
			type: '交通',
			detile: '杭州-德清',
			money: '-12.00'
		},
		{
			showImg: '',
			type: '餐饮',
			detile: '焖面',
			money: '-17.00'
		},
		{
			showImg: '',
			type: '餐饮',
			detile: '沙县小吃',
			money: '-15.00'
		},
		{
			showImg: '',
			type: '水果',
			detile: '橘子',
			money: '-11.00'
		},
	])
</script>

<style lang="scss" scoped>
	page {
		background: #fdfdfd;
		height: 100%;
	}

	.content {
		width: 100%;
		height: 100%;
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
		position: fixed;
		z-index: 7;

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
		position: fixed;
		top: 80rpx;
		z-index: 7;

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
		position: fixed;
		top: 180rpx;
		z-index: 7;

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

	.fourLayer {
		flex: 1;
		width: 100%;
		overflow-y: auto;
		display: flex;
		flex-direction: column;
		position: fixed;
		top: 240rpx;
	}

	.chartBox {
		width: 100%;
		height: 300rpx;
		background-color: rgba(69, 198, 151, 0.5);
		// margin-top: 200rpx;
	}

	.minTitle {
		width: 100%;
		height: 60rpx;
		background: #efefef;
		text-align: left;
		font-size: 30rpx;
		text-indent: 20rpx;
		line-height: 60rpx;
	}

	.chartBox1 {
		width: 100%;
		height: 350rpx;
		background-color: rgba(69, 198, 151, 0.5);
	}

	.getMoney {
		width: 100%;
		flex: 1;
		display: flex;
		flex-direction: column;
	}

	.codeBox {
		height: 100rpx;
		width: 100%;
		display: flex;
		justify-content: space-between;
		align-items: center;
		background-color: #ffffff;
		border-bottom: 1rpx solid #dedede;
		flex-shrink: 0;

		.leftCont {
			display: flex;
			align-items: center;

			.costImg {
				width: 80rpx;
				height: 80rpx;
				background-color: #dddddd;
				border-radius: 50%;
				margin-left: 20rpx;
				display: flex;
				justify-content: center;
				align-items: center;
			}

			.costCont {
				height: 100%;
				margin-left: 30rpx;
				display: flex;
				flex-direction: column;

				.contType {
					font-size: 30rpx;
				}

				.contDetile {
					font-size: 20rpx;
					margin-top: 5rpx;
				}
			}
		}
	}
</style>