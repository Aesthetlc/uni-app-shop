<template>
	<view class="goods_list">
		<view class="goods_item" v-for="item in goods" :key="item.goods_id">
			<image src="../../static/logo.png" mode=""></image>
			<view class="price">
				<text>￥{{ item.goods_price }}</text>
				<text>￥{{ item.goods_price - 100 }}</text>
			</view>
			<view class="name">
				{{item.goods_name}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "goods-list",
		data() {
			return {

			};
		},
		props: {
			goods: {
				type: Array,
				default: () => []
			}
		}
	}
</script>

<style lang="scss">
	.goods_list {
		padding: 0 15rpx;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;

		.goods_item {
			background-color: #FFF;
			width: 355rpx;
			margin: 10rpx 0;
			padding: 15rpx;
			box-sizing: border-box;

			image {
				width: 80%;
				height: 150px;
				display: block;
				margin: 0 auto;
			}
		}

		.price {
			color: $shop-color;
			font-size: 38rpx;
			margin: 20rpx 0 5rpx 0;

			text:nth-child(2) {
				color: #CCCCCC;
				font-size: 28rpx;
				margin-left: 17rpx;
				text-decoration: line-through;
			}
		}

		.name {
			font-size: 28rpx;
			line-height: 40rpx;
			padding: 10rpx 0 15rpx 0;
		}
	}
</style>
