<template>
	<view class="content">
		<image src="../../../static/user_03.png" class="logo"></image>
		<text class="username">{{phone}}</text>
		<view class="input_wrap">
			<input :type="passType" placeholder="请输入密码" :value="password" @input="GetPassword" placeholder-class="place" class="password" />
			<image :src="isSee" class="password_isApprence" @tap="ImageChange"></image>
			<navigator url="../forget/forget" class="goForget">忘记密码？</navigator>
		</view>
		<!-- 登录 -->
		<button class="loginBtn" :disabled="canLogin" @tap="Login">登录</button>
		<!-- 协议 -->
		<view class="agreement_wrap">
			<text :class='choose'>√</text>
			<text class="read_aggre" @tap="AgreeChange">{{pass}}</text>
		</view>
	</view>
</template>

<script>
	// 全局变量，访问全局通用数据
	let globalData = getApp().globalData;
	export default {
		data() {
			return {
				phone:"",
				// 用户协议
				pass:"我已阅读航天电液的<用户服务协议>与<隐私政策>",
				choose:"choose_true",
				// 能否注册
				canLogin:true,
				// 用户密码
				password:"",
				// 密码框显示与隐藏图片变化
				isSee:"../../../static/notSee_03.png",
				passType:"password"
			}
		},
		mounted() {
			// 设置phone值
			this.phone=globalData.phone;
		},
		methods: {
			// 改变协议选中状态
			AgreeChange:function(e){
				// 如果为已选中，点击后变成未选中
				if(this.choose==="choose_true"){
					this.choose="choose_false";
				}else if(this.choose==="choose_false"){
					this.choose="choose_true";
				}
			},
			GetPassword:function(e){
				// 存入密码
				this.password = e.detail.value;
				// 如果密码存在
				if(e.detail.value.length>0){
					this.canLogin=false;
				}else{
					this.canLogin=true;
				}
			},
			Login:function(){
				// 如果协议已选择
				if(this.choose==="choose_true"){
					// 发送请求
				}else{
					// 判断用户是阅读协议
						uni.showModal({
						    title: '提示',
						    content: '请阅读协议后进行勾选',
							showCancel:false
						});
					return false;
				}
			},
			// 密码框显示与隐藏
			ImageChange:function(){
				if(this.isSee==="../../../static/notSee_03.png"){
					// 改变图片
					this.isSee="../../../static/couldSee_03.png";
					// 显示密码
					this.passType="text";
				}else if(this.isSee==="../../../static/couldSee_03.png"){
					this.isSee="../../../static/notSee_03.png";
					// 隐藏密码
					this.passType="password";
				}
			},
			
		}
	}
</script>

<style>
	.logo{
		width: 168rpx;
		height: 168rpx;
		margin: 64rpx auto;
		margin-bottom: 20rpx;
	}
	.username{
		font-size: 36rpx;
		color: #0d0d0d;
		margin-bottom: 104rpx;
	}
	.input_wrap{
		width: 550rpx;
		height: 72rpx;
		margin: 0 auto;
		border-bottom: 2rpx solid #e6e6e6;
		position: relative;
		margin-bottom: 88rpx;
	}
	.password{
		width: 380rpx;
		height: 40rpx;
		font-size: 32rpx;
		border-right: 2rpx solid #e6e6e6;
		position: absolute;
		left: 0;
		top: 14rpx;
	}
	.place{
		font-size: 32rpx;
		color: #808080;
	}
	.password_isApprence{
		width: 50rpx;
		height: 40rpx;
		position: absolute;
		right: 170rpx;
		top: 20rpx;
		z-index: 20;
	}
	.goForget{
		font-size: 32rpx;
		position: absolute;
		right: 0;
		top: 14rpx;
		z-index: 20;
	}
	.loginBtn{
		width: 570rpx;
		height: 88rpx;
		line-height: 88rpx;
		border-radius: 44rpx;
		background: #00ADEF;
		color: white;
		margin-bottom: 20rpx;
	}
	button[disabled]:not([type]){
		background-color: #7fd6f7;
		color: white;
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
</style>
