<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	@font-face {
		font-family: "iconfont";
		/* Project id  */
		src: url('~@/static/font/iconfont.ttf?t=1624291978489') format('truetype');
	}

	.iconfont {
		font-family: "iconfont" !important;
		font-size: 16px;
		font-style: normal;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}

	.icon-lianxiwomen:before {
		content: "\e686";
	}

	.icon-chaoshi:before {
		content: "\e602";
	}

	.icon-shipin:before {
		content: "\e624";
	}

	.icon-tupian:before {
		content: "\e607";
	}
</style>
