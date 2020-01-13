<template>
	<view class="tuijian-list u-f-ac">
		<view>
			<image :src="val.img"></image>
		</view>
		<view>{{val.name}}</view>
	</view>
</template>

<script>
	export default {
		props:{
			val:Object
		},
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
.tuijian-list{
	width: 700upx;
}
.tuijian-list>view:first-child{
	
}
.tuijian-list>view:first-child>image{
	width: 300upx;
	height: 180upx;
	border-radius: 15upx;
}
.tuijian-list>view:last-child{
	width: 300upx;
	height: 180upx;
	margin-left: 30upx;
	text-align: left;
	line-height: 150upx;
	font-weight: 700;
}
</style>
