<script>
	export default {
		onLaunch: function() {
			//读取本地存储的用户信息
			this.$store.commit('initUser')
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	/*每个页面公共css */
	@import "uview-ui/index.scss";
	@import url('@/common/iconfont.css');
	@import url('@/common/uni.css');
	@import url('@/common/common.css');
</style>
