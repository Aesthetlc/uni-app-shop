<template>
	<view class="pics">
		<scroll-view class="left" scroll-y="true">
			<view @click="leftClickHandle(index,item.cat_name)" v-for="(item,index) in picsCateArr" :key="item.cat_id"
				:class="active === index?'active':''">{{ item.cat_name }}</view>
		</scroll-view>
		<scroll-view class="right" scroll-y="true">
			<view class="item" v-for="item in rightContent" :key="item.cat_id">
				<image @click="previewImg(item.cat_icon)" :src="item.cat_icon"></image>
				<text>{{ item.cat_name }}</text>
			</view>
			<text v-if="rightContent.length === 0">暂无数据</text>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				picsCateArr: [], // 左侧菜单导航
				active: 0, //高亮索引
				rightContent: '' //右侧显示内容
			}
		},
		onLoad() {
			this.getPicsCate()
		},
		methods: {
			// 获取左侧导航数据
			async getPicsCate() {
				const res = await this.$myRequest({
					url: '/api/public/v1/categories'
				})

				res.data.message.forEach(item => {
					this.picsCateArr.push(...item.children)
				})
				this.leftClickHandle(0, this.picsCateArr[0].cat_name)


			},
			// 点击左侧导航
			leftClickHandle(index, name) {
				this.active = index
				this.picsCateArr.forEach(item => {
					if (item.cat_name === name && item.children) {
						this.rightContent = item.children
					}
				})
			},
			// 预览图片
			previewImg(current) {
				const urls = this.rightContent.map(item => {
					return item.cat_icon
				})
				uni.previewImage({
					current,
					urls
				})
			}
		}
	}
</script>

<style lang="scss">
	page {
		height: 100%;
	}

	.pics {
		height: 100%;
		display: flex;

		.left {
			width: 200rpx;
			height: 100%;
			border-right: 1px solid #EEEEEE;

			view {
				height: 60px;
				line-height: 60px;
				color: #333;
				text-align: center;
				font-size: 30rpx;
				border-top: 1px solid #EEEEEE;
			}

			.active {
				background-color: $shop-color;
				color: #FFF;
			}
		}

		.right {
			height: 100%;
			width: 520rpx;
			margin: 10rpx auto;

			.item {
				image {
					width: 520rpx;
					height: 520rpx;
					border-radius: 5px;
				}

				text {
					font-size: 30rpx;
					line-height: 60rpx;
				}
			}
		}

	}
</style>
