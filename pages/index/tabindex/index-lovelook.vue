<template>
	<view class="uni-tab-bar">
		<swiper class="swiper-box" :style="{height:swiperheight+'px'}">
			<!-- 推荐 -->
			<swiper-item>
				<scroll-view scroll-y class="list" @scrolltolower="loadmore">
					<template v-if="videoLenght > 0">
						<!-- 图文列表 -->
						<block v-for="(val,index1) in videoList.list" :key='index1'>
							<index-list :val="val" :index="index1" @openNewsVideo="openNewVideo"></index-list>
						</block>
						<!-- 上拉加载 -->
						<load-more :loadtext="videoList.loadtext"></load-more>
					</template>
					<template v-else>
						<noThing></noThing>
					</template>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	import request from "@/common/request.js"
	
	
	import indexList from "@/components/index-one/index-list.vue";
	import noThing from "@/components/common/no-thing.vue";
	import loadMore from "@/components/common/load-more.vue";
	export default {
		components:{
			loadMore,
			noThing,
			indexList,
		},
		data() {
			return {
				requestUrl:getApp().globalData.requestUrl,
				videoList:{
					loadtext:"上拉加载更多",
					list:[]
				},
				swiperheight:800,
				videolistPop:0,
				videoLenght:0,
			}
		},
		onLoad() {
			uni.getSystemInfo({
				success:(res) => {
					let height = res.windowHeight-uni.upx2px(100);
					this.swiperheight=height;
				}
			});
		},
		mounted() {
			this.gitTuijianVideo()
		},
		methods: {
			openNewVideo(e){
				console.log(e)
				uni.navigateTo({
					url:'../../pages/common/common-video-content?id='+e
				})
			},
			// 请求页内数据
			gitTuijianVideo(){
				request.request({
					url: '/app/get/index/love_look/video_list/0', //接口地址
					method: 'GET'
				}).then(res => {
					// 打印接口的数据
					// console.log(res.data.video_list);
					this.videoList.list = res.data.video_list;
					this.videoLenght = this.videoList.list.length;
					// console.log(this.videoLenght)
				}).catch(err => {
					console.log("失败！")
				})
				
			},
			loadmore(index){
				if(this.videoList.loadtext!="上拉加载更多"){return;}
				this.videoList.loadtext="加载中.....";
				var videolistPop = this.videoList.list.pop().id
				setTimeout(() => {
					request.request({
						url:"/app/get/index/love_look/video_list/"+videolistPop, //接口地址   
						method: 'GET'
					}).then(res => {
						this.videoList.list = this.videoList.list.concat(res.data.video_list)
						this.videoList.loadtext = "上拉加载更多";
						// console.log(res.data)
					}).catch(err => {
						console.log("失败！")
					})
				},1000);
				// this.videoList.loadtext ="没有更多数据了";
			},
		}
	}
</script>

<style scoped>
	

</style>
