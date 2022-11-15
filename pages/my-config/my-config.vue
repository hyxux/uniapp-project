<template>
	<view class='my-config'>
		
		<view class='config-item'>
			<view>修改密码</view>
			<view class='config-mark'> > </view>
		</view>
		<view class='config-item'>
			<view>绑定手机号码</view>
			<view class='config-mark'> > </view>
		</view>
		<view class='config-item'@tap='goPathList'>
			<view>地址管理</view>
			<view class='config-mark'> > </view>
		</view>
		<view class='config-item'>
			<view>绑定第三方账号</view>
			<view class='config-mark'> > </view>
		</view>
		<view class='config-item'>
			<view>消息推送</view>
			<view class='config-mark'> > </view>
		</view>
		<view class='config-item'>
			<view>短信提醒</view>
			<view class='config-mark'> > </view>
		</view>
		<view class='config-item'>
			<view>图片显示</view>
			<view class='config-mark'> > </view>
		</view>
		<view class='config-item'>
			<view>清除缓存</view>
			<view class='config-mark'> > </view>
		</view>
		
		<view class='my-exit' @tap="outLogin">退出</view>
		
	</view>
</template>

<script>
	import {mapMutations} from 'vuex'
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			...mapMutations(['loginOut']),
			goPathList(){
				uni.navigateTo({
					url:'../my-path-list/my-path-list'
				})
			},
			outLogin(){
				uni.showToast({
					title:'退出成功',
					icon:'none'
				})
				this.loginOut()
				uni.reLaunch({
					url:'../index/index'
				})({
					delta:1
				})
			}
		}
	}
</script>

<style scoped>
.config-item{
	display: flex;
	justify-content: space-between;
	padding:20rpx 0 20rpx 20rpx;
	border-bottom: 2rpx solid #CCCCCC;
}
.config-mark{
	padding-right:10rpx;
}
.my-exit{
	background-color: #49BDFB;
	width:100%;
	line-height: 80rpx;
	color:#FFFFFF;
	text-align: center;
}
</style>
