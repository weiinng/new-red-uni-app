<template>
	<view class="body">
		<block v-for="(item,index) in LoginList" :key="index">
			<home-list-item :item="item"
			:index="index"
			:userid="userid"></home-list-item>
		</block>
		<button class="user-set-btn" type="primary" v-if="userid > 0" @click="removeStorageinfo">退出登陆</button>
	</view>
</template>

<script>
	import homeListItem from "@/components/home/home-list-item.vue";
	export default {	
		components:{
			homeListItem
		},
		data() {
			return {
				userid:0,
				LoginList:[
					{ icon:"",name:"账号与安全",clicktype:"noLoginNavigateTo",url:"../../pages/mine/user-set-password"},
					{ icon:"",name:"绑定邮箱",clicktype:"noLoginNavigateTo",url:"../../pages/mine/user-set-email" },
					{ icon:"",name:"资料编辑",clicktype:"noLoginNavigateTo",url:"../../pages/mine/user-set-info" },
					{ icon:"",name:"清除缓存",clicktype:"clear",url:"" },
					{ icon:"",name:"意见反馈",clicktype:"navigateTo",url:"../../pages/mine/user-set-help" },
					{ icon:"",name:"关于我们",clicktype:"navigateTo",url:"../../pages/mine/user-set-about" }
				]
			}
		},
		// 一进来就调用
		mounted() {
			this.getStorageinfo()	
		},
		// 方法块
		methods: {
			removeStorageinfo(){
				try {
					uni.showModal({
						title: '提示',
						content: '是否要退出登录？',
						confirmText: '退出',
						success: res => {
							if(res.confirm){
								uni.removeStorageSync('user_data');
								uni.reLaunch({
									url: './personalCenter'
								});
							}
						}
					})
					
				} catch (e) {
				    uni.showToast({
				    	title:"操作失败！",
				    	icon:"none"
				    })
				}
			},
			// 获取缓存内的数据
			getStorageinfo(){
				try {
				    const value = uni.getStorageSync('user_data');
				    if (value) {
						this.userid = value.userid
						console.log("取到了值："+this.userid)
				    }
					else{
						console.log("没有获取到任何值")
					}
				} catch (e) {
				    // error
					console.log("500")
				}
			},
		}
	}
</script>

<style>
@import "../../common/form.css";
</style>
