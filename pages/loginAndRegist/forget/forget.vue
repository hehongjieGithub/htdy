<template>
	<view class="content">
		<image src="../../../static/user_03.png" class="logo"></image>
		<text class="username">{{phone}}</text>
		<!-- 修改密码验证码 -->
		<view class="codeWrap">
			<input type="text" class="code" @input="onCode" :value="code" placeholder-class="place" placeholder="请输入验证码" />
			<button class="getCode" :disabled="isDisable" @tap="gotCode">{{getCode}}</button>
		</view>
		<!-- 输入新密码 -->
		<view class="passWrap">
			<input :type="passType" :value="password" @input="onPassword" placeholder="请输入新密码" placeholder-class="place" class="password"/>
			<image :src="isSee" class="password_isApprence" @tap="ImageChange"></image>
		</view>
		<!-- 登录按钮 -->
		<button class="regist" :disabled="login_btn" @tap="Login">登录</button>
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
				// 用户手机号码
				phone:"",
				getCode:"获取验证码",
				// 用户协议
				pass:"我已阅读航天电液的<用户服务协议>与<隐私政策>",
				choose:"choose_true",
				// 获取验证码按钮是否禁用
				isDisable:false,
				// 验证码
				code:"",
				// 密码
				password:"",
				// 计数器
				num:60,
				passType:"password",
				// 登录按钮是否禁用
				login_btn:true,
				// 密码框显示与隐藏图片变化
				isSee:"../../../static/notSee_03.png"
			}
		},
		mounted() {
			// 设置phone值
			this.phone=globalData.phone;
		},
		methods: {
			// 获取验证码
			gotCode:function(){
				let _that=this;
				// 点击获取验证码后，禁用按钮
				this.isDisable=true;
				_that.getCode=_that.num+"s重新获取";
				let time = setInterval(()=>{
					if(_that.num>0){
					// 时间每秒减1
					_that.num=_that.num-1;
					//显示字符拼接 
					_that.getCode=_that.num+"s重新获取";
					}else if(_that.num===0){
						_that.getCode="获取验证码"
						// 按钮启用
						_that.isDisable=false;
						// 重新赋值num
						_that.num=60
						// 清理事件函数
						clearInterval(time)
					}
				},1000);
			},
			// 改变协议选中状态
			AgreeChange:function(e){
				// 如果为已选中，点击后变成未选中
				if(this.choose==="choose_true"){
					this.choose="choose_false";
				}else if(this.choose==="choose_false"){
					this.choose="choose_true";
				}
			},
			// 注册
			Login:function(){
				if(this.choose==="choose_false"){
					// 判断用户是阅读协议
						uni.showModal({
						    title: '提示',
						    content: '请阅读协议后进行勾选',
							showCancel:false
						});
					return false;
				}
			},
			// 验证码
			onCode:function(e){
				this.code=e.detail.value;
				// 判断输入框是否为空
				if(this.phone!=""&&this.code!=""&&this.password!=""){
					this.login_btn=false;
				}else{
					this.login_btn=true;
				};
			},
			// 密码
			onPassword:function(e){
				this.password=e.detail.value;
				// 判断输入框是否为空
				if(this.phone!=""&&this.code!=""&&this.password!=""){
					this.login_btn=false;
				}else{
					this.login_btn=true;
				};
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
	.codeWrap{
		position: relative;
		display: flex;
		margin-bottom: 12rpx;
	}
	.code{
		border-bottom: 2rpx solid #e6e6e6;
		width: 550rpx;
		height: 76rpx;
		font-size: 36rpx;
	}
	.place{
		font-size: 32rpx;
		color: #808080;
	}
	.getCode{
		width: 160rpx;
		height: 56rpx;
		background-color: #00ADEF;
		color: white;
		font-size: 24rpx;
		border-radius: 0;
		text-align: center;
		line-height: 56rpx;
		position: absolute;
		right: 0;
		bottom: 0;
		padding: 0;
		z-index: 30;
	}
	button[disabled]:not([type]){
		background-color: #7fd6f7;
		color: white;
	}
	.getCode::after{
		border: none;
	}
	.passWrap{
		margin-bottom: 44rpx;
		position: relative;
	}
	.password_isApprence{
		width: 50rpx;
		height: 40rpx;
		position: absolute;
		right: 0;
		top: 24rpx;
		z-index: 20;
	}
	.password{
		width: 550rpx;
		height: 76rpx;
		font-size: 36rpx;
		border-bottom: 2rpx solid #e6e6e6;
	}
	.regist{
		width: 570rpx;
		height: 88rpx;
		line-height: 88rpx;
		border-radius: 44rpx;
		background: #00ADEF;
		color: white;
		margin-bottom: 20rpx;
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
