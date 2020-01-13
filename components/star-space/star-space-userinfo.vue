<template>
	<view class="user-space-userinfo">
		<view class="user-space-userinfo-item">
			<view>基本信息</view>
			<view v-if="userinfo.english_name">{{userinfo.english_name}}</view>
			<view>性别：{{userinfo.gender}}</view>
			<view>生日：{{userinfo.year}}</view>
			<view>故乡：{{userinfo.director}}</view>
			<view>民族：{{userinfo.nation}}</view>
			<view>国籍：{{userinfo.nationality}}</view>
			<view>星座：{{userinfo.constellation}}</view>
			<view>毕业院校：{{userinfo.graduate_academy}}</view>
		</view>
		<view class="user-space-userinfo-item">
			<view>简介</view>
			<view>{{userinfo.region}}</view>
		</view>
		<view class="user-space-userinfo-item">
			<view>职业</view>
			<view class="zhiyelist u-f-wrap">
				<block v-for="(val,index) in userinfo.profession" :key='index'>
					<view class="zhiye">{{val}}</view>
				</block>
			</view>
		</view>
		<view class="user-space-userinfo-item">
			<view>主要成就</view>
				<block v-for="(val,index) in userinfo.main_achievements" :key='index'>
					<view>{{val}}</view>
				</block>
		</view>
		<view class="user-space-userinfo-item">
			<view>代表作品</view>
			<block v-for="(val,index) in userinfo.in_work" :key='index'>
				<view>{{val}}</view>
			</block>
		</view>
	</view>
</template>

<script>
	import t from "../../common/time.js";
	export default {
		props:{
			userinfo:Object
		},
		computed:{
			getRegAge(){
				return t.gettime.sumAge(this.userinfo.regtime)
			},
			getXingZuo(){
				return t.gettime.getHoroscope(this.userinfo.birthday)
			}
		}
	}
</script>

<style scoped>
.zhiye{
	background: #03A9F4;
	padding: 0 23upx;
	border-radius: 15upx;
	color: #FFFFFF;
	font-size: 25upx;
	font-weight: 700;
	margin-right: 20upx;
}
.user-space-userinfo{
	padding: 0 30upx;
}
.user-space-userinfo-item{
	padding: 20upx 0;
	border-bottom: 1upx solid #EEEEEE;
}
.user-space-userinfo-item>view{
	color: #AAAAAA;
}
.user-space-userinfo-item>view:first-child{
	color: #333333;
	font-size: 35upx;
	padding: 15upx 0;
}
</style>
