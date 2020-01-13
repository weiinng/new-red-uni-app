<template>
	<!-- 用户关注的页面，想做一个页面解决问题 -->
	<view class="guanzhu-list">
		<view class="guanzhu-title">没有关注的内容</view>
		<view class="guanzhu-body">关注后，您可以在此页看到关于TA的动态</view>
		<view class="guanzhu-url" @tap="openGuanzhuList">全部视频号</view>
		
	</view>
</template>
<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			openGuanzhuList(){
				uni.navigateTo({
					url:""
				})
			}
		}
	}
</script>

<style scoped>

.guanzhu-list{
	width: 95%;
	height: 300upx;
	border-bottom: 10upx solid rgba(229,229,229,0.76);
	margin: 0 auto;
	
}
.guanzhu-title{
	text-align: center;
	font-weight: bold;
	font-size: 40upx;
	margin-top: 45upx;
}
.guanzhu-body{
	text-align: center;
	color: #C0C0C0;
	font-size: 26upx;
	margin-bottom: 35upx;
}
.guanzhu-url{
	width: 250upx;
	height: 70upx;
	border-radius: 20upx;
	background: red;
	color: white;
	font-weight: 500;
	margin: 0 auto;
	text-align: center;
	display: flex;
	justify-content: center;
	align-items: center;
}
</style>
