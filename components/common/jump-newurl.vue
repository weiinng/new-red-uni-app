<template>
	<view>
		<web-view :webview-styles="webviewStyles" :src="articleurl"></web-view>
	</view>
</template>

<script>
	export default {
		props:{
			getNewUrl:{
				type:String,
				default:"",
			}
		},
		data() {
			return {
				articleurl:"",
				webviewStyles: {
                    progress: {
                        color: '#FF7200'
                    }
                }
			};
		},
		onLoad(options){
			this.articleurl = this.getNewUrl;
		}
	}
</script>
<style>
</style>
