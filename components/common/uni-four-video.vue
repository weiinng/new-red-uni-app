<template>
	<view class="four-video">
		<block v-for="(val,index) in fourList" :key="index">
			<view class="four-list">
				<image class="four-list-img" :src="val.img"></image>
				<view class="four-list-title u-f-ajsb">
					<view>{{val.title}}</view>
					<view class="icon iconfont icon-redu"></view>
				</view>
				<view class="four-list-info">{{val.info}}</view>
				<view class="hot-and-share u-f-ajsb">
					<view class="icon iconfont icon-kanjian">{{val.lookNum}}</view>
					<view class="icon iconfont icon-zhuanfa">转发</view>
				</view>
			</view>
		</block>
	</view>
</template>

<script>
	export default {
		props:{
			fourList:Array,
		},
		methods: {
			
		}
	}
</script>

<style>
.four-video{
	width: 800upx;
	height: 970upx;
	flex-wrap: wrap;
	display: flex;
}
.four-list{
	width: 340upx;
	height: 420upx;
	margin: 20upx;
}

.four-list-img{
	width: 100%;
	height: 300upx;
	border-radius: 5upx;
}
.four-list-title{
	
}
.four-list-title>view:first-child{
	font-weight: 600;
	font-size: 32upx;
}
.four-list-title>view:last-child{
	color: #FF9897;
}
.four-list-info{
	font-weight: 400;
	font-size: 25upx;
	color: #AAAAAA;
}


.hot-and-share{
	width: 100%;
	bottom: 0upx;
}
.hot-and-share>view:first-child{
	font-size: 22upx;
	color: #D8DAD7;
}
.hot-and-share>view:last-child{
	font-size: 22upx;
	color: #D8DAD7;
}

</style>
