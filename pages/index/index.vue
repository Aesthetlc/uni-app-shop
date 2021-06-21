<template>
	<view class="home">
		<!-- https://www.showdoc.com.cn/128719739414963/2513235043485226 -->
		<swiper indicator-dots circular>
			<swiper-item v-for="item in swiperArr" :key="item.goods_id">
				<image :src="item.image_src" mode=""></image>
			</swiper-item>
		</swiper>
		<view class="nav">
			<view class="nav-item">
				<view class="iconfont icon-chaoshi"></view>
				<text>超市</text>
			</view>
			<view class="nav-item">
				<view class="iconfont icon-lianxiwomen"></view>
				<text>联系我们</text>
			</view>
			<view class="nav-item">
				<view class="iconfont icon-tupian"></view>
				<text>社区图片</text>
			</view>
			<view class="nav-item">
				<view class="iconfont icon-shipin"></view>
				<text>社区视频</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swiperArr: [] //轮播图数据
			}
		},
		onLoad() {
			this.getSwipers()
		},
		methods: {
			//获取轮播图数据
			async getSwipers() {
				// uni.request({
				// 	url: "https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata",
				// 	success: (res) => {
				// 		if (res.data.meta.status === 200) {
				// 			this.swiperArr = res.data.message
				// 		} else {
				// 			return uni.showToast({
				// 				title: '获取数据失败'
				// 			})
				// 		}
				// 	}
				// })
				const res = await this.$myRequest({
					url: '/api/public/v1/home/swiperdata'
				})
				this.swiperArr = res.data.message
				console.log(res)
			}
		}
	}
</script>

<style lang="scss">
	.home {
		swiper {
			height: 380rpx;
			width: 750rpx;

			image {
				width: 100%;
				height: 100%;
			}
		}

		.nav {
			display: flex;
				justify-content: space-around;

			.nav-item {
				text-align: center;
				

				view {
					width: 120rpx;
					height: 120rpx;
					background-color: #b50e03;
					border-radius: 60rpx;
					line-height: 120rpx;
					font-size: 60rpx;
					color: #FFF;
					margin: 20rpx 0;
				}

				text {
					font-size: 30rpx;
				}
			}
		}
	}
</style>
