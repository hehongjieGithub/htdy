<template>
	<view :class="style">
		<view class="alert">
			<view class="text">
				{{msg}}
			</view>
			<button @tap="StateChange">确定</button>
		</view>
	</view>
</template>

<script>
export default {
  name: 'Alert',
  props: {
    msg:String,//显示的文字
  },
  data(){
	 return{
		 style:'alert_wrap_hidden'
	 }
  },
  methods:{
	  //通过父组件的调用，改变组件的显示与隐藏
	  StateChange:function(){
		  if(this.style==='alert_wrap'){
			 this.style='alert_wrap_hidden'
		  }else if(this.style==='alert_wrap_hidden'){
			 this.style="alert_wrap"
		  }
	  }
  }
}
</script>

<style>
.alert_wrap{
	width: 100%;
	height: 100%;
	background-color: rgba(0,0,0,.2);
	position: absolute;
	z-index: 2;
	top: 0;
	left: 0;
}
.alert_wrap_hidden{
	width: 100%;
	height: 100%;
	background-color: rgba(0,0,0,.2);
	position: absolute;
	z-index: 2;
	top: 0;
	left: 0;
	display: none;
}
.alert{
	width: 604rpx;
	height: 244rpx;
	background: white;
	border-radius: 20rpx;
	background-color: white;
	position: absolute;
	z-index: 3;
	top: 41%;
	left: 50%;
	margin-left: -302rpx;
	margin-top: -122rpx;
}
.text{
	font-size: 36rpx;
	color: #808080;
	text-align: center;
	height: 140rpx;
	line-height: 140rpx;
	border-bottom: 2rpx solid #efefef;
}
button{
	height: 104rpx;
	font-size: 36rpx;
	background-color: white;
	color: #00adef;
	border: none;
}
uni-button:after{
	border: none;
}
</style>
