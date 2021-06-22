<template>
	<view class="home">
		<!-- https://www.showdoc.com.cn/128719739414963/2513235043485226 -->
		<swiper indicator-dots circular>
			<swiper-item v-for="item in swiperArr" :key="item.goods_id">
				<image :src="item.image_src" mode=""></image>
			</swiper-item>
		</swiper>
		<view class="nav">
			<view class="nav-item" v-for="item in navs" :key="item.path" @click="gotoPath(item)">
				<view :class="item.icon"></view>
				<text>{{ item.title }}</text>
			</view>
		</view>
		<view class="hot_goods">
			<view class="tit">
				推荐商品
			</view>
			<goods :goods="hotGoodsArr"></goods>
		</view>
	</view>
</template>

<script>
	import goods from "../../components/goods-list/goods-list.vue";
	export default {
		data() {
			return {
				swiperArr: [], //轮播图数据
				hotGoodsArr: [], //热门商品数据
				navs: [{
						icon: 'iconfont icon-chaoshi',
						title: '超市',
						path: '/pages/goods/goods'
					},
					{
						icon: 'iconfont icon-lianxiwomen',
						title: '联系我们',
						path: '/pages/contact/contact'
					},
					{
						icon: 'iconfont icon-tupian',
						title: '社区图片',
						path: '/pages/pics/pics'
					},
					{
						icon: 'iconfont icon-shipin',
						title: '社区视频',
						path: '/pages/videos/videos'
					},
				]
			}
		},
		components: {
			goods
		},
		onLoad() {
			this.getSwipers()
			this.getHotGoods()
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
			},
			// 获取热门商品列表数据
			async getHotGoods() {
				const res = await this.$myRequest({
					url: '/api/public/v1/goods/search'
				})
				this.hotGoodsArr = res.data.message.goods
			},
			gotoPath(item) {
				uni.navigateTo({
					url: item.path
				})
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
					background-color: $shop-color;
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

		.hot_goods {
			background-color: #eee;
			overflow: hidden;
			margin-top: 10px;

			.tit {
				height: 50px;
				line-height: 50px;
				color: $shop-color;
				text-align: center;
				letter-spacing: 20px;
				background-color: #FFF;
				margin: 7rpx 0;
				font-size: 40rpx;
			}
		}
	}
</style>
