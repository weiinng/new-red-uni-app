<template>
	<view>
		<web-view :webview-styles="webviewStyles" :src="articleurl"></web-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				articleurl:'',
				webviewStyles: {
                    progress: {
                        color: '#FF7200'
                    }
                }
			};
		},
		onLoad(options){
			this.articleurl = 'http://cloud.quklive.com/cloud/h5/1578480143749969';
		}
	}
</script>
<style>
</style>
