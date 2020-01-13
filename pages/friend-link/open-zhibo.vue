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
			this.articleurl = 'http://cloud.quklive.com/cloud/h5/1578643848137933';
		}
	}
</script>
<style>
</style>
