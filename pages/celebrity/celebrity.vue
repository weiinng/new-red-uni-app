<template>
	<view>
		<!-- 背景图 + 用户基本信息 -->
		<star-space-head :userinfo="userinfo"></star-space-head>
		<!-- 统计 -->
		<view class="user-space-data">
			<home-data :homedata="spacedata"></home-data>
		</view>
		<view style="height: 20upx; background: #F4F4F4;"></view>
		<!-- tab导航 -->
		<swiper-tab-head 
		:tabBars="tabBars" 
		:tabIndex="tabIndex"
		@tabtap="tabtap"
		scrollItemStyle="width:33.33%;"
		scrollStyle="border-bottom:0;">
		</swiper-tab-head>
		<template v-if="tabIndex==0">
			<!-- 主页 -->
			<star-space-userinfo :userinfo="userinfo"></star-space-userinfo>
		</template>
		<block v-for="(item,index) in tablist" :key="index">
			<template v-if="tabIndex==index">
				<!-- 列表 -->
				<block v-for="(list,listindex) in item.list" :key="listindex">
					<common-list :item="list" :index="listindex"></common-list>
				</block>
				<!-- 上拉加载 -->
				<load-more :loadtext="item.loadtext"></load-more>
			</template>
		</block>
		
		<!-- 操作菜单 -->
		<star-space-popup :show="show" 
		@hide="togleShow"
		@lahei="lahei"
		@beizhu="beizhu"></star-space-popup>
		
	</view>
</template>

<script>
	import request from "@/common/request.js"
	
	
	
	import starSpaceHead from "@/components/star-space/star-space-head.vue";
	import homeData from "@/components/home/home-data.vue";
	import swiperTabHead from "@/components/index/swiper-tab-head.vue";
	
	
	
	import starSpaceUserinfo from "@/components/star-space/star-space-userinfo.vue";
	
	import commonList from "@/components/common/common-list.vue";
	import loadMore from "@/components/common/load-more.vue";
	import starSpacePopup from "@/components/star-space/star-space-popup.vue";
	export default {
		components:{
			starSpaceHead,
			homeData,
			swiperTabHead,
			starSpaceUserinfo,
			commonList,
			loadMore,
			starSpacePopup
		},
		data() {
			return {
				show:false,
				userinfo:{},
				spacedata:[
					{ name:"获赞", num:"10k" },
					{ name:"关注", num:11 },
					{ name:"粉丝", num:12 },
				],
				tabIndex:0,
				tabBars:[
					{ name:"主页",id:"zhuye" },
					{ name:"糗事",id:"qiushi" },
					{ name:"动态",id:"dongtai" },
				],
				tablist:[ {},
					{
						loadtext:"上拉加载更多",
						list:[
							// 文字
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"哈哈",
								sex:0, //0 男 1 女
								age:25,
								isguanzhu:false,
								title:"我是标题",
								titlepic:"",
								video:false,
								share:false,
								path:"深圳 龙岗",
								sharenum:20,
								commentnum:30,
								goodnum:20
							},
							// 图文
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"哈哈",
								sex:0, //0 男 1 女
								age:25,
								isguanzhu:false,
								title:"我是标题",
								titlepic:"../../static/demo/datapic/13.jpg",
								video:false,
								share:false,
								path:"深圳 龙岗",
								sharenum:20,
								commentnum:30,
								goodnum:20
							},
							// 视频
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"哈哈",
								sex:0, //0 男 1 女
								age:25,
								isguanzhu:false,
								title:"我是标题",
								titlepic:"../../static/demo/datapic/13.jpg",
								video:{
									looknum:"20w",
									long:"2:47"
								},
								share:false,
								path:"深圳 龙岗",
								sharenum:20,
								commentnum:30,
								goodnum:20
							},
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[
							// 文字
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"哈哈",
								sex:0, //0 男 1 女
								age:25,
								isguanzhu:false,
								title:"我是标题",
								titlepic:"",
								video:false,
								share:false,
								path:"深圳 龙岗",
								sharenum:20,
								commentnum:30,
								goodnum:20
							},
							// 图文
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"哈哈",
								sex:0, //0 男 1 女
								age:25,
								isguanzhu:false,
								title:"我是标题",
								titlepic:"../../static/demo/datapic/13.jpg",
								video:false,
								share:false,
								path:"深圳 龙岗",
								sharenum:20,
								commentnum:30,
								goodnum:20
							},
							// 视频
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"哈哈",
								sex:0, //0 男 1 女
								age:25,
								isguanzhu:false,
								title:"我是标题",
								titlepic:"../../static/demo/datapic/13.jpg",
								video:{
									looknum:"20w",
									long:"2:47"
								},
								share:false,
								path:"深圳 龙岗",
								sharenum:20,
								commentnum:30,
								goodnum:20
							},
						]
					},
				]
			}
		},
		// 获取url传来的值
		onLoad(option) {
			this.userId=option.id
			console.log("接收到参数为："+option.id)
		},
		// 上拉触底事件
		onReachBottom() {
			// 上拉加载
			this.loadmore();
		},
		onNavigationBarButtonTap(e) {
			if(e.index==0){ this.togleShow(); }
		},
		mounted() {
			// 调用这个函数
			this.gitBigVinfo()
			
		},
		methods: {
			gitBigVinfo(){
				request.request({
					url:'/app/get/index/recommend/compere_particulars/'+this.userId,
					method: 'GET'
				}).then(res => {
					if(res.data.status==200){
						this.userinfo = res.data.zhuchiren_info
					}
					console.log(res.data)
				}).catch(err => {
					console.log("失败！")
				})
			},
			// 操作菜单显示隐藏
			togleShow(){
				this.show=!this.show;
			},
			// 拉黑
			lahei(){
				console.log("拉黑")
				this.togleShow();
			},
			// 备注
			beizhu(){
				console.log("备注")
				this.togleShow()
			},
			// 上拉加载更多
			loadmore(){
				if(this.tablist[this.tabIndex].loadtext!="上拉加载更多"){ return; }
				// 修改状态
				this.tablist[this.tabIndex].loadtext="加载中...";
				// 获取数据
				setTimeout(()=> {
					//获取完成
					let obj={
						userpic:"../../static/demo/userpic/12.jpg",
						username:"哈哈",
						sex:0, //0 男 1 女
						age:25,
						isguanzhu:false,
						title:"我是标题",
						titlepic:"../../static/demo/datapic/13.jpg",
						video:false,
						share:false,
						path:"深圳 龙岗",
						sharenum:20,
						commentnum:30,
						goodnum:20
					};
					this.tablist[this.tabIndex].list.push(obj);
					this.tablist[this.tabIndex].loadtext="上拉加载更多";
				}, 1000);
				//this.tablist[this.tabIndex].loadtext="没有更多数据了";
			},
			tabtap(index){
				this.tabIndex=index;
			},
		}
	}
</script>

<style>
.user-space-margin{
	margin: 15upx 0;
}
.user-space-data{
	background: #FFFFFF;
	position: relative;
	z-index: 10;
	border-top-left-radius: 20upx;
	border-top-right-radius: 20upx;
	margin-top: -15upx;
}

</style>
