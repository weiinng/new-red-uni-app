<template>
	<scroll-view scroll-x class="zhuchiren">
		<block v-for="(val,index) in zhuchiren" :key="index">
			<view class="zhuchiren-view">
				<image :src="val.zhuchirenImg">
				<view class="tag">{{val.tag}}</view>
			</view>
		</block>
	</scroll-view>
</template>

<script>
	export default {
		props:{
			zhuchiren:Array
		}
	}
</script>

<style scoped>
.zhuchiren{
	margin-top: 30upx;
	width: 100%;
	overflow: hidden;
	white-space: nowrap;
}
.zhuchiren-view{
	display: inline-block;
	margin-right: 40upx;
}
.tag{
	position: absolute;
	background-color: #F98B54;
	bottom: 10upx;
	margin-left: 50upx;
	font-size: 18upx;
	text-align: center;
	width: 54upx;
	border-radius: 10upx;
	font-weight: 600;
	
}
.zhuchiren-view>image{
	width: 110upx;
	height: 110upx;
	border-radius: 50%;
}	
</style>
