<template>
	<view>
		<Lines />
		
		<view class='list'>
			
			<!--左侧滑动-->
			<scroll-view scroll-y="true" class='list-left' :style="'height:'+clentHeight+'px;'">
				<view v-for='(i,index) in leftData' :key="i.id" class='left-item' @tap="changeLeftTab(i.id)">
					<view class='left-name' 
						:class=' activeIndex ===i.id ?"left-name-active":"" '
					>{{i.name}}</view>
				</view>
			</scroll-view>
			
			<!--右侧滑动-->
			<scroll-view scroll-y="true" class='list-right' :style="'height:'+clentHeight+'px;'">
				
				<view class='righ-list' v-for="(k,i) in rightData" :key="i">
					<view class='list-title'>{{k.name}}</view>
					<view class='right-content'>
						<view class='right-item' v-for="(k1,index) in k.list" :key="index">
							<image class='right-img' :src="k1.imgUrl" mode=""></image>
							<view class='right-name'>{{k1.name}}</view>
						</view>
						
					</view>
				</view>
				
			</scroll-view>
		</view>
		<Tabbar cureentPage='list'></Tabbar>
	</view>
</template>

<script>
	import $http from '@/common/api/request.js'
	import Lines from '@/components/common/Lines.vue'
	import Tabbar from '@/components/common/Tabbar.vue'
	export default {
		data() {
			return {
				clentHeight:0,
				activeIndex:1,
				leftData:[],
				rightData:[]
			}
		},
		onLoad() {
			this.getData()
		},
		//获取可视高度
		onReady() {
			uni.getSystemInfo({
				success: (res) => {
					this.clentHeight = res.windowHeight - this.getClientHeight();
				}
			})
		},
		components:{
			Lines,
			Tabbar
		},
		methods: {
			//请求数据方法
			getData(id){
				if(id===this.activeIndex)
				{
					return ;
				}
				$http.request({
					url:'/goods/list'
				}).then((res)=>{
					let leftData = [];
					res.forEach(v=>{
						leftData.push({
							id:v.id,
							name:v.name
						})
						if(v.id===this.activeIndex){
							this.rightData=v.data
						}
					})
					this.leftData=leftData
				}).catch(()=>{
					uni.showToast({
						title:'请求失败',
						icon:'none'
					})
				})
			},
			
			//获取可视区域高度【兼容】
			getClientHeight(){
				const res = uni.getSystemInfoSync();
				const system = res.platform;
				if( system ==='ios' ){
					return 44+res.statusBarHeight;
				}else if( system==='android' ){
					return 48+res.statusBarHeight;
				}else{
					return 0;
				}
			},
			//左侧点击事件
			changeLeftTab(index){
				this.getData(index)
				this.activeIndex = index;
			}
		},
		//input输入框点击事件
		onNavigationBarSearchInputClicked(){
			uni.navigateTo({
				url:'../search/search'
			})
		}
	}
</script>

<style scoped>
.list{
	display: flex;
}
.list-left{
	width: 200rpx;
}
.left-item{
	border-bottom:2rpx solid #FFFFFF;
	font-size:28rpx;
	font-weight: bold;
	background-color: #F7F7F7;
}
.left-name{
	padding:30rpx 6rpx;
	text-align: center;
}
.left-name-active{
	border-left:8rpx solid #49BDFB;
	background-color: #FFFFFF;
}
.list-right{
	flex:1;
	padding-left:30rpx;
}
.list-title{
	font-weight: bold;
	padding:30rpx 0;
}
.right-content{
	display: flex;
	flex-wrap: wrap;
}
.right-item{
	width: 150rpx;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	padding:10rpx;
}
.right-name{
	padding:16rpx 0;
}
.right-img{
	width: 150rpx;
	height: 150rpx;
}


</style>
