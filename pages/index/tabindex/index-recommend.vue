<template>
	<view>
		<!-- 直播视频的位置 -->
		<!-- <view class="index-list3"> -->
			<!-- <video-play></video-play> -->
			<!-- <new-topic-swiper :carouselList="top_imgs"></new-topic-swiper> -->
			<swiper style="height: 30vh;width: 100vw;">
				<swiper-item v-for="(item,inde) in top_imgs" :key="inde">
					<image style="height: 100%;width:100%;" :src="item.img" @tap="openzhibo"></image>
				</swiper-item>
			</swiper>
			
		<!-- </view> -->
		<!-- end -->
		
		<!-- 标题 -->
		<view class="index-list4">
			<an-notice-bar :text="noticeMsg"></an-notice-bar>
		</view>
		<!-- end -->
		
		<!-- 节目单 -->
		<view class="index-list5 u-f-wrap">
			<block v-for="(val,index) in programList" :key='index'>
				<view class="pro_list u-f-ajsb">
					<view>{{val.body}}</view>
					<view>{{val.time}}</view>
				</view>
			</block>
		</view>
		<!-- 判断是否大于4则隐藏 -->
		<template v-if="programList.length ==4">
			<view class="index-list6 icon iconfont icon-Group" @tap="addProgram"></view>
		</template>
		<!-- end -->
		
		<!-- 栏目大全star -->
		<uni-headertitle :headerTitle="columnObj.columntitle" ></uni-headertitle>
		<view class="index-list8">
			<scroll-view scroll-x="true" class="scroll-list">
				<block v-for="(val,index) in columnObj.coumnlist" :key='index'>
					<view class="scroll-view" @click="openColumnInfo(val.id)">
						<image :src="val.columns_img" lazy-load></image>
						<view class="columntitle">{{val.name}}</view>
					</view>
				</block>
			</scroll-view>
		</view>
		<!-- end -->
		
		<!-- 名人主持板块 -->
		<uni-headertitle :headerTitle="compereObj.comperetitle"></uni-headertitle>
		<view class="index-list9">
			<zhuchiren-list :zhuchiren="compereObj.comperelist" @openHome="zhuchirenHome"></zhuchiren-list>
		</view>
		<!-- end -->
		
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
	
	
	
	// 轮播图 顶部
	import newTopicSwiper from "@/components/common/new-topic-swiper.vue";
	// 滚动标题
	import AnNoticeBar from '@/components/an-notice-bar/an-notice-bar.vue';
	// 标题
	import uniHeadertitle from "@/components/common/uni-header-title.vue";
	// 主持人
	import zhuchirenList from "@/components/index/zhuchiren-list.vue";
	// 四个视频
	import uniFourvideo from "@/components/common/uni-four-video.vue";
	// 没有更多了
	import loadMore from "@/components/common/load-more.vue";
	
	import videoPlay from "@/components/index/video-play.vue"
	
	
	export default {
		components:{
			videoPlay,
			newTopicSwiper,
			AnNoticeBar,
			uniHeadertitle,
			zhuchirenList,
			uniFourvideo,
			loadMore,
			
		},
		data() {
			return {
				top_imgs:[
					{	id:"",
						img:"http://qiniu.weiinng.cn/%E5%B9%B4%E6%8A%A5.jpg",
					},
					{
						img:"http://qiniu.weiinng.cn/%E6%9C%89%E6%A2%A6%E6%B5%B7%E6%8A%A5.jpg",
					}
				],
				noticeMsg:"央视融媒《童星梦栏目》正在播出！|中国与世界展示中国精彩，传颂世界文化!|纵观世界奇石，汇聚世界英才。",	
				programList:[
					{
						body:"童星梦",
						time:"15:00-15:30"
					},
					{
						body:"中国与世界",
						time:"16:00-16:30"
					},
					{
						body:"赏石之路",
						time:"17:00-17:30"
					},
					{
						body:"今日中国",
						time:"20:00-20:30"
					},
				],
				columnObj:{
					columntitle:"栏目大全",
					coumnlist:[]
				},
				// 主持人信息
				compereObj:{
					comperetitle:"名人主持",
					comperelist:[]	
				},
				columnList:[
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
								"lookNum":"8000",
								"isHot":true
							},
							{
								"id":"",
								"title":"海阔天空",
								"info":"关于内蒙古大草原",
								"img":"../../static/imags/7089841.jpg",
								"lookNum":"8000",
								"isHot":false
							},
							{
								"id":"",
								"title":"童话",
								"info":"我要变成童话里！",
								"img":"../../static/imags/7089841.jpg",
								"lookNum":"8000",
								"isHot":false
							},
							{
								"id":"",
								"title":"你爱着的那天使。",
								"info":"关于内蒙古大草原",
								"img":"../../static/imags/7089841.jpg",
								"lookNum":"8000",
								"isHot":true
							}
						]
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
								"lookNum":"8000",
								"isHot":true
							},
							{
								"id":"",
								"title":"海阔天空",
								"info":"关于内蒙古大草原",
								"img":"../../static/imags/7089841.jpg",
								"lookNum":"8000",
								"isHot":false
							},
							{
								"id":"",
								"title":"童话",
								"info":"我要变成童话里！",
								"img":"../../static/imags/7089841.jpg",
								"lookNum":"8000",
								"isHot":false
							},
							{
								"id":"",
								"title":"你爱着的那天使。",
								"info":"关于内蒙古大草原",
								"img":"../../static/imags/7089841.jpg",
								"lookNum":"8000",
								"isHot":true
							}
						]
					}
				],
			}
		},
		mounted() {
			this.getProList(),
			this.getIndexColumnsList()
			
		},
		methods: {
			openzhibo(){
				uni.navigateTo({
					url:"../friend-link/open-zhibo"
				})
			},
			// 栏目列表
			getIndexColumnsList(){
				request.request({
					url:"/app/get/index/recommend/column_list",
					method:"GET"
				}).then(res => {
					this.columnObj.coumnlist = res.data.column_list
				}).catch( err => {
					console.log("失败！")
				})
			},
			// 主持人跳转
			zhuchirenHome(e){
				console.log(e)
				uni.navigateTo({
					url:'../../pages/celebrity/celebrity?id='+e
				})
			},
			// 跳转打开新窗口
			fnOpenWin(type) {
			  uni.navigateTo({
			    url: `/pages/${type}`
			  })
			},
			// 跳转到栏目详情页
			openColumnInfo(columnId){
				uni.navigateTo({
					url:"../../pages/column/column-info?id="+columnId
				})
			},
			getProList(){
				request.request({
					url:"/app/get/index/recommend/compere_list",
					method:"GET"
				}).then(res => {
					// 获取返货信息替换原有信息
					this.compereObj.comperelist = res.data.zhuchiren_list;
				}).catch( err => {
					console.log("失败！")
				})
			},
			// 增加4个
			addProgram(){
				var addProgram = [
					{
						body:"童星梦",
						time:"15:00-15:30"
					},
					{
						body:"中国与世界",
						time:"16:00-16:30"
					},
					{
						body:"赏石之路",
						time:"17:00-17:30"
					},
					{
						body:"今日中国",
						time:"20:00-20:30"
					},
				]
				this.programList = this.programList.concat(addProgram)
			},
		}
	}
</script>

<style scoped>
.columntitle{
	font-weight: 800;
	font-size: 31upx;
	color:rgb(0,0,0,0.7);
	text-align: center;
}
.index-list3{
	width: 100%;
}
.index-list4{
	width: 100%;
}
.index-list5{	
	width: 100%;
}
.index-list5>view{
	height: 30upx;
	width: 300upx;
	margin: 10upx 33upx;
	text-align: center;
}
.pro_list>view{
	font-size: 23upx;
}
.index-list6{
	display: flex;
	align-items: center;
	justify-content: center;
	font-size: 30upx;
	color: #AAAAAA;
}
.scroll-list{
    width: 100%;
	height: 280upx;
	overflow: hidden;
 	white-space: nowrap;
	margin-left: 30upx;
}
.scroll-view{
	display: inline-block;
	width: 320upx;
	height: 270upx;
	margin-right: 15upx;
}
.scroll-view>image{
	height: 190upx;
	position: relative;
	width: 320upx;
	border-radius: 10upx;
}
</style>
