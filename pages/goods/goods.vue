<template>
	<view class="goods_list">
		<goods @goodsItemClick="goGoodsDetail" :goods="goodsList"></goods>
		<view class="isOver" v-if="flag"> -----别刷新了，没有了-----</view>
	</view>
</template>

<script>
	import goods from "../../components/goods-list/goods-list.vue";
	export default {
		data() {
			return {
				pagenum: 1, //当前页
				goodsList: [], //列表数据
				flag: false,
				total: 0
			}
		},
		components: {
			goods
		},
		onLoad() {
			this.getGoodsList()
		},
		onReachBottom() {
			if (this.goodsList.length = this.total) {
				return this.flag = true
			}
			this.pagenum++
			this.getGoodsList()
		},
		onPullDownRefresh() {
			this.pagenum = 1
			this.goodsList = []
			this.flag = false
			setTimeout(() => {
				this.getGoodsList(() => {
					uni.stopPullDownRefresh()
				})
			}, 1000);
		},
		methods: {
			//获取商品列表的数据
			async getGoodsList(callBack) {
				const res = await this.$myRequest({
					url: `/api/public/v1/goods/search?pagenum=${this.pagenum}`
				})
				this.goodsList = [...this.goodsList, ...res.data.message.goods]
				this.total = res.data.message.total
				callBack && callBack()
			},
			// 导航到商品详情页
			goGoodsDetail(id) {
				uni.navigateTo({
					url: '/pages/goodsDetail/goodsDetail?id=' + id
				})
			}
		}
	}
</script>

<style lang="scss">
	.goods_list {
		background-color: #EEEEEE;
	}

	.isOver {
		width: 100%;
		height: 50px;
		line-height: 50px;
		font-size: 28rpx;
	}
</style>
