<template>
	<scroll-view scroll-x class="zhuchiren">
		<block v-for="(val,index) in zhuchiren" :key="index">
			<view class="zhuchiren-view">
				<image :src="val.big_v_img1"></image>
				<view class="zhuchiName">{{val.name}}</view>
				<view class="zhuchiInfo">{{val.info || '人气主持人'}}</view>
				<view class="u-f-ajsb">
					<view class="icon iconfont icon-redu">热度</view>
					<view class="icon iconfont icon-cangkuchakan" @tap="$emit('openHome',val.id)">主页</view>
				</view>
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
	width: 100%;
	height: 320upx;
	overflow: hidden;
	white-space: nowrap;
	margin-left: 30upx;
}
.zhuchiren-view{
	display: inline-block;
	width: 220upx;
	height: 315upx;
	margin-right: 15upx;
	border: #D9D9D9 solid 1upx;
	border-radius: 10upx;
}
.zhuchiren-view>image{
	width: 160upx;
	height: 160upx;
	border-radius: 100%;
	margin-left: 32upx;
	margin-top: 10upx;
}
.zhuchiName{
	font-size: 27upx;
	font-weight: bold;
	text-align: center;
}
.zhuchiInfo{
	font-size: 20upx;
	text-align: center;
}
.zhuchiren-view>view:last-child >view{
	font-size: 23upx;
	margin: 0 10upx;
	color: #FF9897;
}	
</style>
