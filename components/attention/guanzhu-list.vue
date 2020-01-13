<template>
	<view class="att-list u-f-ac">
		 <view class="att-img">
			 <image :src="guanzhuObj.img"></image>
		 </view>
		 <view class="att-body">
			 <view class="att-title">{{guanzhuObj.title}}</view>
			 <template v-if="guanzhuObj.is_attention==true">
				 <view class="att-notguanzhu u-f-ac">
					 <view @tap="guanzhu">+</view>
					 <view>已关注</view>
				 </view>
			 </template>
			 <template v-else>
				 <view class="att-guanzhu u-f-ac">
					 <view @tap="guanzhu">+</view>
					 <view>关注</view>
				 </view>
			 </template>
		 </view>
	</view>
</template>

<script>
	export default {
		props:{
			guanzhuObj:Object
		},
		data() {
			return {
				isAttention:this.guanzhuObj.is_attention
			}
		},
		methods: {
			guanzhu(){
				if(this.isAttention==true){
					this.isAttention=false;
				}
				else{
					this.isAttention=false;
					uni.showToast({
						title:'关注成功',
					})
				}
			}
		}
	}
</script>

<style scoped>

.att-list{
	width: 330upx;
	height: 150upx;
	margin-left: 27upx;
	margin-right: 10upx;
}
.att-img{
	margin-right: 20upx;
}
.att-img>image{
	width: 120upx;
	height: 120upx;
	border-radius: 100%;
}
.att-body{
	
}
.att-title{
	font-size: 27upx;
	font-weight: 800;
}

/* 公共样式 */
.att-guanzhu>view:first-child,.att-notguanzhu>view:first-child{
	font-size: 25;
	font-weight: 600;
	background-color: crimson;
	color: white;
	width: 30upx;
	height: 30upx;
	border-radius: 10upx;
	text-align: center;
	display: flex;
	align-items: center;
	justify-content: center;
	margin-right: 5upx;
}
.att-notguanzhu>view:first-child,.att-notguanzhu>view:last-child{
	font-weight: 600;
	font-size: 23upx;
}

/* 关注的样式 */
.att-guanzhu>view:first-child{
	background-color: crimson;
	color: white;
}

.att-guanzhu>view:last-child{
	color: crimson;
}


/* 不关注的样式 */
.att-notguanzhu>view:first-child{
	background-color: #E7E1CD;
	color: black;
}
.att-notguanzhu>view:last-child{
	color: #E7E1CD;
}
</style>
