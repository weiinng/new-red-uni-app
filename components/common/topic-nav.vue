<template>
	<view class="topic-nav">
		<!-- 顶部 -->
		<view class="u-f-ac u-f-jsb">
			<view>{{className}}</view>
			<view class="u-f-ac">
				更多<view class="icon iconfont icon-gengduo"></view>
			</view>
		</view>
		<!-- 分类内容 -->
		<view class="u-f-ac">
			<block v-for="(val,index) in navList" :key="index">
				<view class="u-f-ajc">{{val.name}}</view>
			</block>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			className:{
				type:String,
				default:"热门分类"
			},
			navList:{
				type:Array
			}
			
		},
		data() {
			return {
				
			}
		}
	}
</script>

<style scoped>
	
.topic-nav{
	border-bottom: 1upx #EEEEEE solid;
	border-top: 1upx #EEEEEE solid;
	padding: 20upx;
}
.topic-nav>view:first-child{
	margin-bottom: 10upx;
}
.topic-nav>view:first-child view{
	color: #AAAAAA;
}
.topic-nav>view:first-child>view:first-child{
	color: #333333;
	font-size: 32upx;
}
.topic-nav>view:last-child>view{
	flex: 1;
	background:#EEEEEE;
	color: #AAAAAA;
	border-radius: 10upx;
	margin: 0 10upx;
	font-weight: 700;
}
</style>
