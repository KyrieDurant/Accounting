<template>
	<view class="content">
		<view class="personBox">
			<image src="../../static/image/user/patience.jpg" mode="aspectFit" class="userImg"></image>
			<view class="userName">杜小帅</view>
		</view>
		<view class="manItem">
			<image src="../../static/image/user/menu.png" mode="aspectFit" class="listImg"></image>
			<view class="itemItxt">类别管理</view>
			<view class="arrow-right"></view>
		</view>
		<view class="manItem">
			<image src="../../static/image/user/menu1.png" mode="aspectFit" class="listImg"></image>
			<view class="itemItxt">选项设置</view>
			<view class="arrow-right"></view>
		</view>
		<view class="manItem">
			<image src="../../static/image/user/export.png" mode="aspectFit" class="listImg"></image>
			<view class="itemItxt">导出Excel</view>
			<view class="arrow-right"></view>
		</view>
		<view class="manItem">
			<image src="../../static/image/user/color.png" mode="aspectFit" class="listImg"></image>
			<view class="itemItxt">主题颜色</view>
			<view class="arrow-right"></view>
		</view>
		<view class="manItem">
			<image src="../../static/image/user/about.png" mode="aspectFit" class="listImg"></image>
			<view class="itemItxt">关于</view>
			<view class="arrow-right"></view>
		</view>
	</view>
</template>

<script>
</script>

<style lang="scss" scoped>
	.content {
		width: 100%;
		display: flex;
		flex-direction: column;
		color: #313131;
	}

	.personBox {
		width: 100%;
		height: 150rpx;
		background-color: #ffffff;
		display: flex;
		align-items: center;

		.userImg {
			width: 100rpx;
			height: 100rpx;
			margin-left: 7%;
			display: flex;
			justify-content: center;
			align-items: center;
			border-radius: 50%;
		}

		.userName {
			margin-left: 30rpx;
			font-size: 35rpx;
			letter-spacing: 3rpx;

		}
	}

	.manItem {
		width: 100%;
		height: 100rpx;
		background-color: #ffffff;
		margin-top: 20rpx;
		display: flex;
		align-items: center;

		.listImg {
			width: 50rpx;
			height: 50rpx;
			margin-left: 7%;
			display: flex;
			justify-content: center;
			align-items: center;
		}

		.itemItxt {
			margin-left: 30rpx;
			font-size: 35rpx;
			letter-spacing: 3rpx;
		}

		.arrow-right {
			width: 20rpx;
			height: 20rpx;
			position: absolute;
			right: 50rpx;
			background-color: transparent;
			border-color: #c7c7c7;
			border-style: solid;
			border-width: 4rpx 4rpx 0 0;
			transform: rotate(45deg);

		}
	}
</style>