<template>
	<view class="contact">
		<image class="img"
			src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic2.16pic.com%2F00%2F48%2F95%2F16pic_4895971_b.jpg&refer=http%3A%2F%2Fpic2.16pic.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1627053551&t=6b28b8a7829da3e9d3349df6e67617a9"
			mode=""></image>
		<view class="info">
			<view @click="phone">
				联系电话：18745778667
			</view>
			<view>
				联系地址：北京市顺义区中国航信
			</view>
			<map class="map" :scale="scale" :markers="markers" :longitude="longitude" :latitude="latitude"></map>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude: 116.534121,
				latitude: 40.124332,
				markers: [{
					longitude: 116.534121,
					latitude: 40.124332,
					iconPath: '../../static/logo.png',
					width: 30,
					height: 30
				}],
				scale: 13
			}
		},
		methods: {
			phone() {
				console.log('波i大')
				uni.makePhoneCall({
					phoneNumber: '18745778667'
				})
			}
		}
	}
</script>

<style lang="scss">
	.contact {
		.img {
			width: 750rpx;
			height: 320rpx;
		}

		.info {
			padding: 10rpx 20rpx;
			font-size: 30rpx;

			view {
				line-height: 80rpx;
				border-bottom: 1px solid #EEEEEE;
			}
		}

		.map {
			width: 750rpx;
			height: 750rpx;
		}
	}
</style>
