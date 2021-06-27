<template>
	<view class="home">
		<!-- 轮播图 -->
		<div v-if="goodsContent.pics && goodsContent.pics.length>0">
			<swiper indicator-dots>
				<swiper-item v-for="item in goodsContent.pics" :key="item.pics_id">
					<image :src="item.pics_big" mode=""></image>
				</swiper-item>
			</swiper>
		</div>
		<div v-else>暂无图片数据</div>
		<view class="box1">
			<view class="price">
				<text>￥{{ goodsContent.goods_price }}</text>
				<text>￥{{ goodsContent.goods_price +2000 }}</text>
			</view>
			<view class="goods_name">
				{{ goodsContent.goods_name}}
			</view>
		</view>
		<view class="line"></view>
		<view class="box2">
			<view>
				货号：SD{{goodsContent.goods_number}}
			</view>
			<view>
				库存：{{goodsContent.goods_weight}}
			</view>
		</view>
		<view class="line"></view>
		<view class="box3">
			<view class="tit">
				详情介绍
			</view>
			<view class="content">
				{{ goodsContent.goods_name }}{{ goodsContent.goods_name }}
			</view>
		</view>
		<view class="goods-bottom">
			<uni-goods-nav :fill="true" :options="options" :buttonGroup="buttonGroup" @click="onClick"
				@buttonClick="buttonClick" />
		</view>

	</view>
</template>

<script>
	import uniGoodsNav from '@/uni_modules/uni-goods-nav/components/uni-goods-nav/uni-goods-nav.vue'
	export default {
		data() {
			return {
				goodsContent: {},
				options: [{
					icon: 'headphones',
					text: '客服'
				}, {
					icon: 'shop',
					text: '店铺',
					info: 2,
					infoBackgroundColor: '#007aff',
					infoColor: "red"
				}, {
					icon: 'cart',
					text: '购物车',
					info: 2
				}],
				buttonGroup: [{
						text: '加入购物车',
						backgroundColor: '#ff0000',
						color: '#fff'
					},
					{
						text: '立即购买',
						backgroundColor: '#ffa200',
						color: '#fff'
					}
				]
			}
		},
		onLoad(options) {
			this.getGoodsMes(options.id)
		},
		components: {
			uniGoodsNav
		},
		methods: {
			async getGoodsMes(id) {
				const res = await this.$myRequest({
					url: '/api/public/v1/goods/detail?goods_id=' + id
				})
				if (res.data.meta.status === 200) {
					this.goodsContent = res.data.message
					console.log(this.goodsContent)
				}
			},
			onClick(e) {
				uni.showToast({
					title: `点击${e.content.text}`,
					icon: 'none'
				})
			},
			buttonClick(e) {
				console.log(e)
				this.options[2].info++
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

		.box1 {
			padding: 10px 10px 5px 10px;

			.price {
				font-size: 38rpx;
				color: $shop-color;
				line-height: 80rpx;

				text:nth-child(2) {
					font-size: 28rpx;
					color: #CCCCCC;
					text-decoration: line-through;
					margin-left: 20rpx;
				}
			}

			.goods_name {
				font-size: 32rpx;
				line-height: 60rpx;
			}
		}

		.box2,
		.box3 {
			margin-left: 20rpx;
			font-size: 32rpx;
			line-height: 60rpx;
		}

		.box3 {
			padding-bottom: 50px;

			.tit {
				font-size: 32rpx;
			}

			.content {
				line-height: 50rpx;
				font-size: 28rpx;
			}
		}

		.goods-bottom {
			position: fixed;
			width: 750rpx;
			bottom: 0;
		}

		.line {
			height: 8rpx;
			width: 750rpx;
			background-color: #EEEEEE;
		}
	}
</style>
