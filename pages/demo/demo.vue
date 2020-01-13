<template>
	<view class="index-list">
		<navigator url="../mine/login">登录</navigator>
		<navigator url="../index/play-video">视频播放</navigator>
		<navigator url="../index/play-web">直播网页</navigator>
		<navigator url="../search/search">搜索页</navigator>
		<navigator url="../column/column-info">栏目主页</navigator>
		<navigator url="../friend-link/open-zhibo">电视直播</navigator>
		<navigator url="../../pages/mine/login">登录</navigator>
		<navigator url="../common/common-video-content">视频详情页</navigator>
		
		<button @click="sed_get">点击发起GET</button>
	</view>
</template>

<script>
	import request from "@/common/request.js"
	
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			sed_get(){
				request.request({
					url:"/get/index/getIndexCompere_particulars",
					data:{
						video_id:1
					},
					method:"POST"
				}).then(res => {
					if(res.data.status == 200){
						console.log("请求成功！")
					}
					else{
						
					}
				}).catch( err => {
					console.log("失败！")
				})
			}
		}
	}
</script>

<style>
.index-list>navigator{
	width: 100%;
	height: 50upx;
	margin: 10upx 0 10upx 0;
	background: #BBBBBB;
	color: red;
	font-weight: bold;
	display: flex;
	align-items: center;
	font-size: 42upx;
	padding-left: 30upx;
}
</style>
