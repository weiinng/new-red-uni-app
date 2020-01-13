<template>
	<view class="container">
		<view class="left-bottom-sign"></view>
		<view class="back-btn yticon icon-zuojiantou-up" @click="navBack"></view>
		<view class="right-top-sign"></view>
		<view class="header">
			<image src="../../static/logo.jpg"></image>
		</view>
		
		<view class="list">
			<view class="list-call">
				<image class="img" src="/static/shilu-login/1.png"></image>
				<input class="biaoti" v-model="phoneno" type="number" maxlength="11" placeholder="输入手机号" />
			</view>
			<view class="list-call">
				<image class="img" src="/static/shilu-login/2.png"></image>
				<input class="biaoti" v-model="password" type="text" maxlength="32" placeholder="输入密码" password="true" />
			</view>
		</view>
		<view class="dlbutton" hover-class="dlbutton-hover" @tap="bindLogin()">
			<text>登录</text>
		</view>
		<!-- 第三方登录 -->
		<view class="elseLogin u-f-ajc">
			<!-- <image src="../../static/shilu-login/qq.png" @tap="login_qq"></image> -->
			<image src="../../static/shilu-login/weixin.png" @tap="login_weixin"></image>
			<!-- <image src="../../static/shilu-login/weibo.png" @tap="login_weibo"></image> -->
		</view>
		<view class="xieyi">
			<navigator url="forget" open-type="navigate">忘记密码</navigator>
			<text>|</text>
			<navigator url="reg" open-type="navigate">注册账户</navigator>
		</view>
	</view>
</template>

<script>
	
	import request from "@/common/request.js"
	
	
	var tha;
	import {
	    mapMutations  
	} from 'vuex';
	export default {
		onLoad(){
			tha = this;
		},
		data() {
			return {
				phoneno:'',
				password:'',
				userid:{},
				logining: false
			};
		},
		methods: {
			...mapMutations(['login']),
			navBack(){
				uni.navigateBack();
			},
		    async bindLogin() {
				this.logining = true;
				if (this.phoneno.length != 11) {
				     uni.showToast({
				        icon: 'none',
				        title: '手机号不正确'
				    });
				    return;
				}
		        if (this.password.length < 6) {
		            uni.showToast({
		                icon: 'none',
		                title: '密码不正确'
		            });
		            return;
		        }
				var result = await this.$api.json('userInfo');
				if(result.status === 1){
					request.request({
						url:'/app/post/mine/user_login',
						data: {
							phoneno:this.phoneno,
							password:this.password
						},
						method: 'POST',	
					}).then(res => {
						console.log("进来了！");
						if(res.data.status != 200){
							console.log("所取到的值 !=200"+res.data.code);
							uni.showToast({title:res.data.msg,icon:'none'});
						}else{
							console.log("所取到的值==200");
							console.log(result.data)
							console.log(res.data.user_info)
							result.data = res.data.user_info
							this.login(result.data);
							// uni.navigateBack();  
							// 将user缓存
							// uni.setStorageSync('user_data',res.data.user_info);
							uni.reLaunch({
								url: '../user/user'
							});
						}
					}).catch(err =>{
						uni.showToast({
							title:"服务器出了点问题，请稍后重试！",
							icon:"none"
						})
					})
					
				}else{
					this.$api.msg(result.msg);
					this.logining = false;
				}
		    },
			jumpMin(){
				uni.redirectTo({
					url:"../demo/demo"
				})
			},
			login_weibo() {
				//微博登录
				uni.showToast({
					icon: 'none',
					position: 'bottom',
					title: '...'
				});
			},
			login_qq() {
				//qq登录
				uni.showToast({
					icon: 'none',
					position: 'bottom',
					title: '...'
				});
			},
			login_weixin() {
				//微信登录
				uni.showToast({
					icon: 'none',
					position: 'bottom',
					title: '...'
				});
			}
		}
	}
</script>

<style>
	.container{
		padding-top: 115px;
		position:relative;
		width: 100vw;
		height: 100vh;
		overflow: hidden;
		background: #fff;
	}
	.content {
		display: flex;
		flex-direction: column;
		justify-content:center;
	}
	.header {
		width:161upx;
		height:161upx;
		background:rgba(63,205,235,1);
		box-shadow:0upx 12upx 13upx 0upx rgba(63,205,235,0.47);
		border-radius:50%;
		margin-top: 30upx;
		margin-left: auto;
		margin-right: auto;
	}
	.header image{
		width:161upx;
		height:161upx;
		border-radius:50%;
	}
	
	.list {
		display: flex;
		flex-direction: column;
		padding-top: 50upx;
		padding-left: 70upx;
		padding-right: 70upx;
	}
	.list-call{
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		height: 100upx;
		color: #333333;
		border-bottom: 1upx solid rgba(230,230,230,1);
	}
	.list-call .img{
		width: 40upx;
		height: 40upx;
	}
	.list-call .biaoti{
		flex: 1;
		text-align: left;
		font-size: 32upx;
		line-height: 100upx;
		margin-left: 16upx;
	}

	.dlbutton {
		color: #FFFFFF;
		font-size: 34upx;
		width:470upx;
		height:100upx;
		background:linear-gradient(-90deg,rgba(63,205,235,1),rgba(188,226,158,1));
		box-shadow:0upx 0upx 13upx 0upx rgba(164,217,228,0.2);
		border-radius:50upx;
		line-height: 100upx;
		text-align: center;
		margin-left: auto;
		margin-right: auto;
		margin-top: 100upx;
	}
	.dlbutton-hover {
		background:linear-gradient(-90deg,rgba(63,205,235,0.9),rgba(188,226,158,0.9));
	}
	.xieyi{
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		font-size: 30upx;
		margin-top: 80upx;
		color: #FFA800;
		text-align: center;
		height: 40upx;
		line-height: 40upx;
	}
	.xieyi text{
		font-size: 24upx;
		margin-left: 15upx;
		margin-right: 15upx;
	}
	.elseLogin{
		
	}
	.elseLogin>image{
		height: 70upx;
		width: 70upx;
		margin:70upx 30upx 30upx 30upx;
	}
	.left-bottom-sign{
		position:absolute;
		left: -270upx;
		bottom: -320upx;
		border: 100upx solid #d0d1fd;
		border-radius: 50%;
		padding: 180upx;
	}
	.back-btn{
		position:absolute;
		left: 40upx;
		z-index: 9999;
		padding-top: var(--status-bar-height);
		top: 40upx;
		font-size: 40upx;
		color: $font-color-dark;
	}
</style>
