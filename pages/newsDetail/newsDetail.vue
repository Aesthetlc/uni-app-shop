<template>
	<view class="news_datail">
		<text class="title">我就是一个测试标题</text>
		<view class="info">
			<text>发表时间:2021年6月25日</text>
			<text>浏览：33</text>
		</view>
		<view class="content">
			<rich-text :nodes="nodes"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				showContent: {},
				nodes: '<h1>我是一个p标签，我来测试html</h1></br>我是普通的文本进行测试'
			}
		},
		onLoad(options) {
			this.getNewsDatail(options.id)
		},
		methods: {
			async getNewsDatail(id) {
				const res = await this.$myRequest({
					url: '/api/public/v1/goods/detail?goods_id=' + id
				})
				if (res.data.meta.status === 200) {
					this.showContent = res.data.message
				}
			}
		}
	}
</script>

<style lang="scss">
	.news_datail {
		font-size: 30rpx;
		padding: 0 20px;

		.title {
			text-align: center;
			width: 710rpx;
			display: block;
			margin: 20rpx 0;
		}

		.info {
			display: flex;
			justify-content: space-between;
		}

		.content {
			margin-top: 10rpx;
		}
	}
</style>
