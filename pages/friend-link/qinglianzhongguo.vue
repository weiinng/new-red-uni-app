<template>
	<view>
		<web-view :webview-styles="webviewStyles" :src="articleurl" ></web-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				articleurl:'',
				webviewStyles: {progress: false,}
			};
		},
		onLoad(options){
			this.articleurl = 'http://qlzg.cctvzyzg.com/index.html';
		}
	}
</script>
<style>
</style>
