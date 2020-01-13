<!-- 上拉加载完整组件 -->
<template>
	<view class="load-more">{{loadtext}}</view>
</template>

<script>
	export default {
		props:{
			loadtext:String,
			obj:Object
			
		},
		methods: {
			loadmore(index){
				if(this.newList[index].loadtext!="上拉加载更多"){return;}
				this.newList[index].loadtext="加载中.....";
				setTimeout(() => {
					this.newList[index].list.push(this.obj);
					this.newList[index].loadtext = "上拉加载更多";
				},1000);
				// this.newList[index].loadtext="没有更多数据了";
			}
		}
	}
</script>

<style>
.load-more{
		text-align: center;
		color: #AAAAAA;
		padding: 15upx;
	}
</style>
