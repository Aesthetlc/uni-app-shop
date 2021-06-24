<template>
	<view>
		<view class="news_item" @click="navigator(item.goods_id)" v-for="item in contentArr" :key="item.goods_id">
			<image src="../../static/logo.png" mode=""></image>
			<view class="right">
				<view class="tit">
					我是咨询标题--{{item.goods_name}}
				</view>
				<view class="info">
					<text>发表时间:2021年6月24日</text>
					<text>浏览:55</text>
				</view>
			</view>
		</view>
	</view>

</template>

<script>
	export default {
		data() {
			return {

			}
		},
		props: {
			contentArr: {
				type: Array,
				default: () => []
			}
		},
		methods: {
			navigator(id) {
				this.$emit('itemClick',id)
			}
		}
	}
</script>

<style lang="scss">
	.news_item {
		display: flex;
		padding: 10rpx 20rpx;
		border-bottom: 1px solid $shop-color;

		image {
			max-width: 200rpx;
			min-width: 200rpx;
			height: 150rpx;
		}

		.right {
			margin-right: 15rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-between;

			.tit {
				font-size: 30rpx;
			}

			.info {
				font-size: 24rpx;

				text:nth-child(2) {
					margin-left: 20rpx;
				}
			}

		}
	}
</style>
