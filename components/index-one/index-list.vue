<template>
	<!-- 微电影用的短视频样式 -->
	<view class="index-list animated fadeInLeft fast">
		<template v-if="val.title">
			<view class="valTitle">{{val.title}}</view>
		</template>
		<template v-else>
			<view class="valTitle">{{val.column_name}}的作品</view>
		</template>
		<view class="index-list1 u-f-ajc">
			<image :src="val.video_img" lazy-load></image>
			<view class="icon iconfont icon-bofang micorFilm-list-play" @tap="$emit('openNewsVideo',val.id)"></view>
			<!-- <video 
			:src="val.video_url"
			:poster="val.video_img"
			objectFit="fill"
			></video> -->
		</view>
		<view class="index-list2 u-f-ajsb" v-if="val.column_img">
			<!-- 左边 -->
			<view class="u-f-ac">
				<image :src="val.column_img" mode="widthFix" lazy-load></image>
				<view class="info-text">{{val.column_name}}</view>
				<view class="icon iconfont icon-jia" @tap="guanzhu" v-show="!isAttention"></view>
			</view>
			<!-- 右边 -->
			<view class="u-f-ac">
				<!-- <view class="icon iconfont icon-xiaoxi"></view> -->
				<!-- <view>{{val.playnum}}</view> -->
				<view class="icon iconfont icon-zhuanfa" style="margin-left: 10upx;"></view>
				<view>分享</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			val:Object,
			index:Number
		},
		methods:{
			// 关注
			guanzhu(){
				this.isAttention=true;
				uni.showToast({
					title:'关注成功',
				})
			},			
		},
		data(){
			return{
				isAttention:this.val.isAttention,
				
			}
		}
	}
</script>
<!-- 限制作用域，这里面的css不会影响到其他 -->
<style scoped> 
	.valTitle{
		font-weight: 600;
		font-size: 33upx;
	}
	.index-list{
		padding: 20upx;
		border-bottom: 1upx solid #C8C7CC;
	}
	.index-list1{
		padding-top: 15upx;
		position: relative;
	}
	.index-list1>video{
		width: 100%;
	}
	.index-list1>image{
		width: 100%;
		height: 350upx;
		border-radius: 20upx;
	}
	.index-list2{
		margin-top: 20upx;
	}
	.index-list2>view:first-child{
		background-color: #EFEFEF;
		border-radius: 800upx;
		width: 280upx;
	}
	.index-list2>view:first-child image{
		width: 60upx;
		height: 60upx;
		border-radius: 100%;
		margin-right: 10upx;
	}
	.info-text{
		width: 163upx;
	}
	.micorFilm-list-play{
		position: absolute;
		font-size: 140upx;
		color:rgba(0,0,0,0.7);
	}
</style>
