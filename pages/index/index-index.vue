<template>
	<view class="container">
		<view class="content">
			<ms-tabs :type="tablist" v-model="tabIndex" itemColor="#F5C7CE" lineColor="#D84C29" :titleNViewBackground="titleNViewBackground"></ms-tabs>
		</view>
		
		<swiper style="min-height: 100vh;" :current="tabIndex" @change="swiperTab">
			<swiper-item v-for="(val,index) in tablist" :key="index">
				<!-- <scroll-view style="height: 100%;" scroll-y="true" @scrolltolower="lower1" scroll-with-animation :scroll-into-view="toView"> -->
				<scroll-view style="height: 100%;" scroll-y scroll-with-animation>
				<!-- <view :id="'top'+listIndex" style="width: 100%;height: 100upx;"></view> -->
					<view class='content'>
						<!-- 推荐 -->
						<view v-if="tabIndex == 0">
							<!-- 头部轮播 -->
							<index-recommend></index-recommend>
						</view>
						<!-- 推荐end -->
						
						<!-- 爱看 -->
						<view v-if="tabIndex == 1">
							<index-lovelook></index-lovelook>
						</view>
						<!-- 关注end -->
						
						<!-- 电影 -->
						<view v-if="tabIndex == 2">
							<!-- 电影外联模板 -->
								<index-film></index-film>
							<!-- 电影end -->
						</view>
						<!-- end -->
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	// 顶部导航栏
	import msTabs from "@/components/common-tab-Bar/ms-tabs.vue"
	
	// tab分页
	import indexAttention from "./tabindex/index-attention.vue";
	import indexRecommend from "./tabindex/index-recommend.vue";
	import indexFilm from "./tabindex/index-film.vue";
	import indexLovelook from "./tabindex/index-lovelook.vue";
	export default {
		components:{
			msTabs,
		
			indexRecommend,
			indexAttention,
			indexFilm,
			indexLovelook,
		},
		data() {
			return {
				tablist: [
					{title: '精选'},
					{title: "爱看"},
					{title: '电影'},
				],
				tabIndex:0,
				titleNViewBackground: '',
				swiperCurrent: 0,
				swiperLength: 0,
				carouselList: [],
				goodsList: []
			};
		},
		// 顶部导航栏 左边的点击事件
		onNavigationBarButtonTap(e){
			switch (e.index){
				case 0:
				// 打开设置页面
				uni.navigateTo({
					url: '../../pages/selectCity/selectCity',
				});
					break;
			}
		},
		onNavigationBarSearchInputClicked(){
			// 打开设置页面
			uni.navigateTo({
				url: '../../pages/search/search',
			});	
		},

		onLoad() {
			this.loadData();
		},
		methods: {
			async loadData() {
				let carouselList = [
					{
						src: "/static/temp/banner3.jpg",
						background: "rgb(203, 87, 60)",
					},
					{
						src: "/static/temp/banner2.jpg",
						background: "rgb(205, 215, 218)",
					},
					{
						src: "/static/temp/banner4.jpg",
						background: "rgb(183, 73, 69)",
					}
					
				];
				this.titleNViewBackground = carouselList[0].background;
				this.swiperLength = carouselList.length;
				this.carouselList = carouselList;
			},
			//轮播图切换修改背景色
			swiperChange(e) {
				const index = e.detail.current;
				this.swiperCurrent = index;
				this.titleNViewBackground = this.carouselList[index].background;
			},
			swiperTab: function(e) {
				var index = e.detail.current //获取索引
				this.tabIndex = index
			}
		},
	}
</script>

<style lang="scss">
.content {
	background: #fff;
	margin-bottom: 20rpx;
}
.title {
	margin-left: 20rpx;
	// padding: 20rpx 0;
	color: #818586;
	// border-bottom: 1px solid #f6f6f6;
}
</style>
