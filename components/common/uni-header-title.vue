<template>
	<view class="index-list7 u-f-ajsb">
		<view>{{headerTitle}}</view>
		<view class="icon iconfont icon-gengduo"></view>
	</view>
</template>

<script>
	export default {
		props:{
			headerTitle:String,
			plateId:String,
		}
	}
</script>

<style>
.index-list7{
	margin: 0 29upx;
}
.index-list7>view:first-child{
	font-size: 32upx;
	font-weight: 700;
}
.index-list7>view:last-child{
	font-size: 40upx;
}
</style>
