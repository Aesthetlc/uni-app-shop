<template>
	<view class="pics">
		<scroll-view class="left" scroll-y="true">
			<view @click="leftClickHandle(index,item.id)" v-for="(item,index) in picsCateArr" :key="item.cat_id"
				:class="active === index?'active':''">{{ item.cat_name }}</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				picsCateArr: [], // 左侧菜单导航
				active: 0 //高亮索引
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

			},
			leftClickHandle(index, id) {
				this.active = index
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

	}
</style>
