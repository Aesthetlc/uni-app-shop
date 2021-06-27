<template>
	<view class="news">
		<newsItem @itemClick="geDetail" :contentArr="contentArr"></newsItem>
	</view>

</template>

<script>
	import newsItem from '../../components/news-item/news-item.vue';
	export default {
		data() {
			return {
				contentArr: []
			}
		},
		onLoad() {
			this.getNews()
		},
		methods: {
			// 获取数据
			async getNews() {
				const res = await this.$myRequest({
					url: '/api/public/v1/goods/search'
				})
				this.contentArr = res.data.message.goods
			},
			// 跳转详情
			geDetail(id) {
				uni.navigateTo({
					url: '/pages/newsDetail/newsDetail?id=' + id
				})
			}
		},
		components: {
			newsItem
		}
	}
</script>

<style lang="scss">
	.news {}
</style>
