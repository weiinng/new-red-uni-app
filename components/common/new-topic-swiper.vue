<template>
	<swiper class="swiper-new-list" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
		<block v-for="(val,index) in carouselList" :key="index">
			<swiper-item>
				<image :src="val.img" mode="widthFix" lazy-load></image>
			</swiper-item>
		</block>
	</swiper>
</template>

<script>
	export default {
		props:{
			carouselList:Array
		},
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
.swiper-new-list{
	padding: 0 20upx 20upx 20upx;
	
}
.swiper-new-list image{
	width: 100%;
}
.swiper-new-list swiper-item{
	height: 400upx;
}
</style>
