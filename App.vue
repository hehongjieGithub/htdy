<script>
	export default {
		globalData: {
		            phone:"",//用户账号
		        },
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
			const { windowWidth, windowHeight } = uni.getSystemInfoSync();
			console.log(windowWidth, windowHeight)
		},
		onHide: function() {
			console.log('App Hide')
		},
		onPageScroll(e){
		        console.log(e)  
		    },
	}
</script>

<style>
	/*每个页面公共css */
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
</style>
