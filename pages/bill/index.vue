<template>
	<view class="content">
		<view class="topBox">
			<view class="topBar">
				<image src="../../static/image/bill/account-book.png" mode="aspectFit"
					style="width: 60rpx;margin-left: 20rpx;"></image>
				<view class="dateBox">2024年1月 ▼</view>
				<image src="../../static/image/bill/switch.png" mode="aspectFit"
					style="width: 40rpx;margin-left: 20%; "></image>
				<image src="../../static/image/bill/search.png" mode="aspectFit" style="width: 50rpx;margin-left: 5%; ">
				</image>
				<image src="../../static/image/bill/calendar.png" mode="aspectFit"
					style="width: 60rpx;margin-left: 5%; "></image>
			</view>
			<view class="modTxt">
				<span>本月支出</span>
				<view class="reportBtn">
					<span>报表统计 </span>
					<image src="../../static/image/bill/arrow.png" mode="aspectFit"
						style="width: 30rpx;padding-left: 10rpx;"></image>
				</view>
			</view>
			<view class="moneyTxt">
				<span class="unit">￥</span>
				<span class="num">12.00</span>
			</view>
			<view class="monStatus">
				<div class="monCont">
					<view class="units">本月收入</view>
					<view class="nums">0.00</view>
				</div>
				<div class="monCont">
					<view class="units">本月支出</view>
					<view class="nums">-12.00</view>
				</div>
			</view>
		</view>
		<!-- 花销面板 -->
		<view class="costBox">
			<view class="dayCost" v-for="(item,index) in costList" :key="index">
				<view class="costDate">
					<span>{{ item.date }}</span>
					<span>支出: {{ item.money }}</span>
				</view>
				<view class="codeBox" v-for="(item1,index1) in item.childData" :key="index1">
					<view class="leftCont">
						<view class="costImg">
							<image src="../../static/image/bill/account-book.png" mode="aspectFit"
								style=" width: 60rpx;"></image>
						</view>
						<view class="costCont">
							<span class="contType">{{item1.type}}</span>
							<span class="contDetile">{{item1.detile}}</span>
						</view>
					</view>
					<span style="padding-right: 2%;">{{ item1.money }}</span>
				</view>
			</view>
		</view>
		<u-popup v-model="show" mode="bottom" width="100%" height="300rpx">
			<view>
				骊山语罢清宵半，泪雨霖铃终不怨
			</view>
		</u-popup>
		<view class="plus"></view>

	</view>
</template>

<script setup>
	import {
		ref,
		onMounted
	} from "vue";
	
	const show = ref(true)

	const costList = ref([{
		date: '1月1日,周一',
		money: '-12.00',
		childData: [{
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
		]
	}, {
		date: '1月2日,周二',
		money: '-39.00',
		childData: [{
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
		]
	}, ])
</script>

<style lang="scss" scoped>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.topBox {
		height: 400rpx;
		width: 100%;
		color: #ffffff;
		background-color: #303e9f;
		display: flex;
		flex-direction: column;

		.topBar {
			width: 100%;
			height: 80rpx;
			margin-top: 20rpx;
			display: flex;
			align-items: center;
			// background-color: #37c8c3;

			.dateBox {
				color: #ffffff;
				display: flex;
				align-items: center;
				margin-left: 10%;
			}
		}
	}

	.imgBox {
		width: 60rpx;
		height: 60rpx;
	}

	.modTxt {
		height: 60rpx;
		width: 90%;
		margin-left: 5%;
		margin-top: 40rpx;
		display: flex;
		justify-content: space-between;
		align-items: center;
		color: #ffffff;
		font-size: 25rpx;
		// background-color: rgba(45, 217, 145, 0.7);

		.reportBtn {
			color: #ffffff;
			position: relative;
			display: flex;
			align-items: center;
		}
	}

	.moneyTxt {
		width: 90%;
		height: 100rpx;
		margin-left: 5%;
		margin-top: 40rpx;
		display: flex;
		color: #ffffff;

		.unit {
			font-size: 25rpx;
			line-height: 100rpx;
		}

		.num {
			font-size: 60rpx;
			font-weight: 600;
			margin-left: 3%;
		}
	}

	.monStatus {
		width: 90%;
		height: 30rpx;
		margin-left: 5%;
		display: flex;

		// background-color: rgba(45, 217, 145, 0.7);
		.monCont {
			width: 50%;
			display: flex;
			align-items: center;
			position: relative;

			.units {
				font-size: 25rpx;
			}

			.nums {
				font-size: 35rpx;
				font-weight: 600;
				margin-left: 5%;
			}
		}
	}

	.costBox {
		width: 100%;
		display: flex;
		flex-direction: column;
		overflow-y: scroll;
		color: #767676;

		.dayCost {
			width: 100%;
			display: flex;
			flex-direction: column;

			.costDate {
				width: 96%;
				height: 60rpx;
				margin-left: 2%;
				// background-color: #5fc9ef;
				display: flex;
				justify-content: space-between;
				align-items: center;
				font-size: 25rpx;
				color: #767676;
			}

			.codeBox {
				height: 100rpx;
				width: 100%;
				display: flex;
				justify-content: space-between;
				align-items: center;
				background-color: #ffffff;
				border-bottom: 1rpx solid #dedede;

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
		}
	}

	.plus {
		width: 120rpx;
		height: 120rpx;
		background-color: #303e9f;
		border-radius: 50%;
		position: absolute;
		bottom: 5%;
		right: 5%;
	}

	.plus::before,
	.plus::after {
		content: "";
		position: absolute;
		top: 50%;
		left: 50%;
		width: 50rpx;
		height: 4rpx;
		background-color: white;
		transform: translate(-50%, -50%);
	}

	.plus::before {
		transform: translate(-50%, -50%) rotate(90deg);
	}
</style>