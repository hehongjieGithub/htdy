<template>
	<view class="content">
		<!-- logo -->
		<image src="/static/logo_03.png" class="logo" mode=""></image>
		<!-- 手机号 -->
		<input type="text" maxlength="11" @input="onInput" :value="phone" placeholder="请输入手机号" placeholder-class="placehold" class="getphone" />
		<!-- 下一步 -->
		<button class="nextControl" :disabled="isDisab" @tap="GoNext">下一步</button>
		<!-- 协议 -->
		<view class="agreement_wrap">
			<text :class='choose'>√</text>
			<text class="read_aggre" @tap="AgreeChange">{{pass}}</text>
		</view>
		<Alert msg="123" ref="alert"></Alert>
	</view>
</template>

<script>
	// 全局变量
	let globalData = getApp().globalData;
	import Alert from "../../components/Alert/Alert.vue"
	
	export default {
		components:{
			Alert
		},
		data() {
			return {
				// 用户协议
				pass:"我已阅读航天电液的<用户服务协议>与<隐私政策>",
				choose:"choose_true",
				isDisab:true,
				phone:""
			}
		},
		onLoad() {
		
		},
		mounted(){
			// const that = this
			//         window.onresize = () => {
			//           return (() => {
			//             window.screenWidth = document.body.clientWidth;
			//             that.screenWidth = window.screenWidth;
			// 			console.log(window.screenWidth)
			//           })()
			//         }
		},
		methods: {
			// 改变协议选中状态
			AgreeChange:function(e){
				if(this.choose==="choose_true"){
					this.choose="choose_false";
				}else if(this.choose==="choose_false"){
					this.choose="choose_true";
				}
				// this.$refs.alert.StateChange()
			},
			// 点击下一步
			GoNext:function(){
				// 手机号码验证
				if(!(/^1[3456789]\d{9}$/.test(this.phone))){ 
				    // 判断用户是否输入正确11位手机号
					uni.showModal({
					    title: '提示',
					    content: '手机号码有误，请重新输入',
						showCancel:false
					});
					return false;
				}else if(this.choose==="choose_false"){
					// 判断用户是阅读协议
						uni.showModal({
						    title: '提示',
						    content: '请阅读协议后进行勾选',
							showCancel:false
						});
					return false;
				}
				// 输入正确11位手机号直接到这里
				uni.showModal({
				    title: '提示',
				    content: '这是一个模态弹窗',
				    success: function (res) {
				        if (res.confirm) {
				            console.log('用户点击确定');
							uni.navigateTo({
								url:"../loginAndRegist/regist/regist"
							})
				        } else if (res.cancel) {
				            console.log('用户点击取消');
							uni.navigateTo({
								url:"../loginAndRegist/login/login"
							})
				        }
				    }
				});
			},
			// 判断手机号码输入是否达到11位
			onInput:function(e){
				if(e.detail.value.length===11){
					// 获取输入电话号码
					this.phone = e.detail.value;
					// 改变button按钮禁用状态
					this.isDisab=false;
					// 设置phone值
					globalData.phone=e.detail.value;
				}else{
					// 如果输入手机号未到11位，按钮禁用
					this.isDisab=true;
				}
			},
		}
	}
</script>

<style>
	.logo {
		height: 144rpx;
		width: 208rpx;
		margin-top: 136rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 104rpx;
	}

	.getphone{
		font-size: 32rpx;
		border-bottom: 2rpx solid #e6e6e6;
		width: 550rpx;
		height: 72rpx;
		margin-bottom: 88rpx;
	}
	
	.placehold{
		font-size: 32rpx;
		color: #808080;
	}
	.nextControl{
		width: 570rpx;
		height: 88rpx;
		background: #00adef;
		color: white;
		border-radius: 44rpx;
		margin-bottom: 20rpx;
		line-height: 88rpx;
	}
	.agreement_wrap{
		display: flex;
	}
	.read_aggre{
		font-size: 24rpx;
		color: #808080;
		display: flex;
		line-height: 24rpx;
	}
	.choose_true{
		width: 20rpx;
		height: 20rpx;
		color: white;
		background: #00adef;
		line-height: 20rpx;
		text-align: center;
		margin-right: 10rpx;
		font-size: 24rpx;
		border: 2rpx solid #00adef;
		font-family: 宋体;
	}
	.choose_false{
		width: 20rpx;
		height: 20rpx;
		color: white;
		border: 2rpx solid #808080;
		line-height: 20rpx;
		text-align: center;
		font-size: 24rpx;
		margin-right: 10rpx;
		font-family: 宋体;
	}
	button[disabled]:not([type]){
		background-color: #7FD6F7;
		color: white;
	}
</style>
