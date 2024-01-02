<template>
	<view class="content">
		<view class="topBox">
			<view class="topBar">
				<image src="../../static/image/bill/account-book.png" mode="aspectFit"
					style="width: 60rpx;margin-left: 20rpx;"></image>
				<view class="dateBox">2024年1月 ▼</view>
				<image src="../../static/image/bill/switch.png" mode="aspectFit"
					style="width: 40rpx;margin-left: 20%; "></image>
				<image src="../../static/image/bill/search.png" mode="aspectFit" 
				style="width: 50rpx;margin-left: 5%; "></image>
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
	</view>
</template>

<script setup>
	import {
		ref,
		onMounted
	} from "vue";
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
		font-size: 18rpx;
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
			font-size: 20rpx;
			line-height: 100rpx;
		}

		.num {
			font-size: 60rpx;
			font-weight: 600;
			margin-left: 5%;
		}
	}
	.monStatus{
		width: 90%;
		height: 60rpx;
		margin-left: 5%;
		display: flex;
		// background-color: rgba(45, 217, 145, 0.7);
		.monCont{
			width: 50%;
			display: flex;
			align-items: center;
			position: relative;
			.units{
				font-size: 20rpx;
			}
			.nums{
				font-size: 35rpx;
				font-weight: 600;
				margin-left: 20rpx;
			}
		}
	}
</style>