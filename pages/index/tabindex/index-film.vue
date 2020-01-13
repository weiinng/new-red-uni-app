<template>
	<view class="container">

		<!--banner-->
		<view class="tui-banner-box">
			<swiper :indicator-dots="true" :autoplay="true" :interval="5000" :duration="150" class="tui-banner-swiper" :circular="true"
			 previous-margin="60rpx" next-margin="60rpx" @change="change">
				<swiper-item v-for="(item,index) in banner" :key="index" class="tui-banner-item">
					<image :src="'../../static/images/mall/banner/'+item" class="tui-slide-image" :class="[current!=index?'tui-banner-scale':'']"
					 mode="scaleToFill" @tap="detail" />
				</swiper-item>
			</swiper>
		</view>
		<!--banner-->

		<!--headlines-->
		<view class="tui-rolling-news list-item">
			<swiper :vertical="true" :autoplay="true" :circular="true" :interval="4000" class="tui-swiper">
				<swiper-item v-for="(item,index) in headlines" :key="index" class="tui-swiper-item">
					<view class="icon iconfont icon-volume" style="font-size: 40upx;"></view>
					<view class="tui-news-item">{{item}}</view>
				</swiper-item>
			</swiper>
		</view>
		<!--headlines-->
		<view class="tui-classify-box">
			<view class="tui-classify-item" v-for="(item,index) in classify" :key="index" @tap="more" :data-key="item.name">
				<image :src="'../../static/images/classify/'+item.img+'.png'" class="tui-classify-img" />
				<view class="tui-classify-name">{{item.name}}</view>
			</view>
		</view>
		<!-- 视频板块 -->
		<block v-for="(item,columnIndex) in columnList" :key="columnIndex">
			<view>
				<!-- four video -->
				<uni-headertitle :headerTitle="item.headerTitle" :plateId="item.plateId"></uni-headertitle>
				<!-- 只接受四条信息 -->
				<uni-fourvideo :fourList="item.bodyList"></uni-fourvideo>
			</view>
		</block>
		<!-- end -->
		<load-more loadtext="没有更多了"></load-more>

	</view>
</template>

<script>
	import request from "@/common/request.js"
	
	
	
	
	import tuiIcon from "@/components/ThorUi-module/countdown/countdown.vue";
	import tuiCountdown from "@/components/ThorUi-module/countdown/countdown.vue";
	import uniFourvideo from "@/components/common/uni-four-video.vue";
	import loadMore from "@/components/common/load-more.vue";
	import uniHeadertitle from "@/components/common/uni-header-title.vue";
	export default {
		components:{
			tuiIcon,
			tuiCountdown,
			uniFourvideo,
			loadMore,
			uniHeadertitle,
		},
		data() {
			return {
				banner: [
					"1.jpg",
					"2.jpg",
					"3.jpg",
					"4.jpg",
					"5.jpg"
				],
				classify: [{
						img: "kongtiao",
						name: "正能量"
					},
					{
						img: "Icewash",
						name: "喜剧"
					},
					{
						img: "heater",
						name: "动作"
					},
					{
						img: "bed",
						name: "恐怖"
					},
					{
						img: "boutique",
						name: "教育"
					}
				],
				current: 0,
				headlines: [
					"苹果XR对比华为Mate20你会选择谁",
					"格兰仕暗示拜访拼多多后遭天猫打压，拼多多高层赞其有勇气",
					"耐克没进前十，今年Q1全球受欢迎品牌榜"
				],
				productList: [
					{
						img: 1,
						name: "欧莱雅（LOREAL）奇焕光彩粉嫩透亮修颜霜 30ml（欧莱雅彩妆 BB霜 粉BB 遮瑕疵 隔离）",
						sale: 599,
						factory: 899,
						time:2000
					},
					{
						img: 2,
						name: "德国DMK进口牛奶  欧德堡（Oldenburger）超高温处理全脂纯牛奶1L*12盒",
						sale: 29,
						factory: 69,
						time: 1500
					},
					{
						img: 3,
						name: "【第2支1元】柔色尽情丝柔口红唇膏女士不易掉色保湿滋润防水 珊瑚红",
						sale: 299,
						factory: 699,
						time: 1800
					},
					{
						img: 4,
						name: "百雀羚套装女补水保湿护肤品",
						sale: 1599,
						factory: 2899,
						time:1000
					},
					{
						img: 5,
						name: "百草味 肉干肉脯 休闲零食 靖江精制猪肉脯200g/袋",
						sale: 599,
						factory: 899,
						time: 3000
					},
					{
						img: 6,
						name: "短袖睡衣女夏季薄款休闲家居服短裤套装女可爱韩版清新学生两件套 短袖粉色长颈鹿 M码75-95斤",
						sale: 599,
						factory: 899,
						time:2400
					},
					{
						img: 1,
						name: "欧莱雅（LOREAL）奇焕光彩粉嫩透亮修颜霜",
						sale: 599,
						factory: 899,
						time: 1600
					},
					{
						img: 2,
						name: "德国DMK进口牛奶",
						sale: 29,
						factory: 69,
						time: 1200
					},
					{
						img: 3,
						name: "【第2支1元】柔色尽情丝柔口红唇膏女士不易掉色保湿滋润防水 珊瑚红",
						sale: 299,
						factory: 699,
						time:1800
					},
					{
						img: 4,
						name: "百雀羚套装女补水保湿护肤品",
						sale: 1599,
						factory: 2899,
						time:2600
					}
				],
				
				
				columnList:[
						{
						"headerTitle":"赛事专区",
						"plateId":"",
						// 只传入四条信息
						"bodyList":[]
					},
					{
						"headerTitle":"赛事专区",
						"plateId":"",
						"bodyList":[
							// 只传入四条信息
							{	
								"id":"",
								"title":"套马杆",
								"info":"关于内蒙古大草原",
								"img":"../../static/imags/7089841.jpg",
								"lookNun":"8000",
								"isHot":true
							},
							{
								"id":"",
								"title":"海阔天空",
								"info":"关于内蒙古大草原",
								"img":"../../static/imags/7089841.jpg",
								"lookNun":"8000",
								"isHot":false
							},
							{
								"id":"",
								"title":"童话",
								"info":"我要变成童话里！",
								"img":"../../static/imags/7089841.jpg",
								"lookNun":"8000",
								"isHot":false
							},
							{
								"id":"",
								"title":"你爱着的那天使。",
								"info":"关于内蒙古大草原",
								"img":"../../static/imags/7089841.jpg",
								"lookNun":"8000",
								"isHot":true
							}
						]
					}
				],
			}
		},
		// 一进来就调用
		mounted() {
			this.getFilmVideoList()
			
		},
		// 方法
		methods: {
			// 获取电影业的电影
			getFilmVideoList(){
				request.request({
					url:'/app/get/index/index_film/film_videolist',
					method: 'GET'
				}).then(res => {
					this.columnList[0].bodyList = res.data.filmvideolist
					// console.log(res.data)
				}).catch(err => {
					console.log("失败！")
				})
			},
			change: function(e) {
				this.current = e.detail.current
			},
			detail: function() {
				uni.navigateTo({
					url: '../productDetail/productDetail'
				})
			},
			more: function(e) {
				let key = e.currentTarget.dataset.key || "";
				uni.navigateTo({
					url: '../productList/productList?searchKey=' + key
				})
			}
		}
	}
</script>

<style scoped>
	.container {
		padding-bottom: 100rpx;
		box-sizing: border-box;
	}

	/*banner*/

	.tui-banner-box {
		width: 100%;
		padding-top: 20rpx;
		box-sizing: border-box;
		background: #fff;
	}

	.tui-banner-swiper {
		width: 100%;
		height: 240rpx;
	}

	.tui-banner-item {
		padding: 0 16rpx;
		box-sizing: border-box;
	}

	.tui-slide-image {
		width: 100%;
		height: 240rpx;
		display: block;
		border-radius: 12rpx;
		/* transition: all 0.1s linear; */
	}

	.tui-banner-scale {
		transform: scaleY(0.9);
		transform-origin: center center;
	}

	/* #ifdef APP-PLUS || MP */
	.tui-banner-swiper .wx-swiper-dot {
		width: 8rpx;
		height: 8rpx;
		display: inline-flex;
		background: none;
		justify-content: space-between;
	}
	
	.tui-banner-swiper .wx-swiper-dot::before {
		content: '';
		flex-grow: 1;
		background: rgba(255, 255, 255, 0.8);
		border-radius: 16rpx;
		overflow: hidden;
	}
	
	.tui-banner-swiper .wx-swiper-dot-active::before {
		background: #fff;
	}
	
	.tui-banner-swiper .wx-swiper-dot.wx-swiper-dot-active {
		width: 16rpx;
	}
	
	/* #endif */
	
	/* #ifdef H5 */
	>>>.tui-banner-swiper .uni-swiper-dot {
		width: 8rpx;
		height: 8rpx;
		display: inline-flex;
		background: none;
		justify-content: space-between;
	}
	
	>>>.tui-banner-swiper .uni-swiper-dot::before {
		content: '';
		flex-grow: 1;
		background: rgba(255, 255, 255, 0.8);
		border-radius: 16rpx;
		overflow: hidden;
	}
	
	>>>.tui-banner-swiper .uni-swiper-dot-active::before {
		background: #fff;
	}
	
	>>>.tui-banner-swiper .uni-swiper-dot.uni-swiper-dot-active {
		width: 16rpx;
	}
	
	/* #endif */
	/*banner*/

	/*headlines*/

	.tui-rolling-news {
		width: 100%;
		padding: 0 30rpx;
		box-sizing: border-box;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-wrap: nowrap;
		background: #fff;
	}

	.tui-rolling-news::after {
		left: 0;
	}

	.tui-swiper {
		margin-left: 8rpx;
		font-size: 28rpx;
		height: 80rpx;
		flex: 1;
	}

	.tui-swiper-item {
		display: flex;
		align-items: center;
	}

	.tui-news-item {
		line-height: 28rpx;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
		color: #555;
	}

	/*headlines*/

	/*classify*/

	.tui-classify-box {
		width: 100%;
		display: flex;
		flex-wrap: wrap;
		align-items: center;
		justify-content: space-between;
		padding: 28rpx 0;
		background-color: #fff;
	}

	.tui-classify-item {
		width: 20%;
		text-align: center;
	}

	.tui-classify-img {
		width: 88rpx;
		height: 88rpx;
	}

	.tui-classify-name {
		font-size: 26rpx;
		line-height: 26rpx;
		padding-top: 8rpx;
		color: #555;
		white-space: nowrap;
	}

	/*classify*/

	/*spike*/

	.tui-spike-box {
		background: #fff;
		margin-top: 20rpx;
	}

	.tui-spike-title {
		padding: 20rpx 30rpx;
		box-sizing: border-box;
		font-size: 30rpx;
		color: #333;
		font-weight: bold;
	}

	.tui-spike-title::after {
		left: 0;
	}

	.tui-spike-swiper {
		min-height: 440rpx;
	}

	.tui-pro-item {
		display: flex;
		width: 100%;
		background: #fff;
		box-sizing: border-box;
		border-radius: 12rpx;
		position: relative;
	}

	.tui-pro-item::after {
		left: 240rpx;
	}

	.tui-pro-img {
		width: 220rpx;
		height: 220rpx;
		display: block;
		flex-shrink: 0;
		border-radius: 12rpx;
	}

	.tui-pro-content {
		flex: 1;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		box-sizing: border-box;
		padding: 20rpx;
	}

	.tui-pro-tit {
		color: #2e2e2e;
		font-size: 26rpx;
		word-break: break-all;
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
	}

	.tui-pro-btmbox {
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.tui-sale-price {
		font-size: 34rpx;
		font-weight: 500;
		color: #e41f19;
	}

	.tui-factory-price {
		font-size: 24rpx;
		color: #a0a0a0;
		text-decoration: line-through;
		padding-left: 12rpx;
	}

	.tui-countdown {
		display: flex;
		align-items: center;
	}

	.tui-countdown-text {
		padding: 0 8rpx;
		font-size: 24rpx;
		line-height: 24rpx;
		color: #555;
	}

	/*spike*/
</style>
