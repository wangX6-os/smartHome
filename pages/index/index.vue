<template>
	<view  :style="{height: screenHeight+'px'}">
		<view id="title">{{ title }}</view>
		<view id="phoneNumberD"> 手机号码 </view>
		<view id="phoneNumberI">
			<input type="text" v-model="phoneNumber" placeholder="请输入手机号"/>
		</view>
		<!-- <view id="checkClick" @click="sendCheck()">点击发送验证码    </view>
		<view id="checks">
			<view>
				<input type="text" value="" />
			</view>
			<view>
				<input type="text" value="" />
			</view>
			<view>
				<input type="text" value="" />
			</view>
			<view>
				<input type="text" value="" />
			</view>
		</view> -->
		
		<button id="login" @click="login()"  type="default">登 录</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				screenHeight: "",
				title: "登  录",
				phoneNumber: "17732071393",
				
			}
		},
		mounted(){
			this.screenHeight = uni.getSystemInfoSync().windowHeight;
		},
		watch:{
			phoneNumber(nv){
				this.$store.commit("setPN", this.phoneNumber);
			}
		},
		methods: {
			sendCheck(){
				uni.showToast({
					title: "已发送验证码",
					duration: 1500
				})
			},
			login(){ 
				const _this = this
				if(this.phoneNumber.toString().length != 11){
					uni.showToast({
						title: "号码长度不对",
						duration: 1500
					})
					return;
				}
				// uni.request({
				// 	url: this.address + "/peopleUser/check",
				// 	data: {
				// 		phoneNumber: this.phoneNumber
				// 	},
				// 	success(res){
				// 		console.log(res)
				// 		const flag = res.data.result;
				// 		console.log(flag)
				// 		if(flag == 0){
				// 			uni.navigateTo({
				// 				url: '../firstInfo/firstInfo',
				// 				success: res => {},
				// 				fail: () => {},
				// 				complete: () => {}
				// 			});
				// 		}else{
				// 			_this.$store.commit("setUserInfo", res.data.userInfo);
				// 			uni.switchTab({
				// 				url: "../main/main"
				// 			})
				// 		}
				// 	}
				// })
				uni.switchTab({
					url: "/pages/device/device"
				})
				
				
				
			}
		}
	}
</script>

<style>
	#title{
		width: 750upx;
		height: 120upx;
		background-color: #dc3f44;
		text-align: center;
		line-height: 140upx;
		font-size: 60upx;
		font-weight: 700;
		color: white;
	}
	#phoneNumberD {
		width: 750upx;
		height: 80upx;
		/* background-color: #4CD964; */
		font-size: 35upx;
		line-height: 90upx;
		margin-top: 15%;
		padding-left: 60upx;
	}
	#phoneNumberI{
		width: 680upx;
		height: 120upx;
		margin: 0 50upx;
		border: 2upx solid #dc3f44;
		border-radius: 16upx;
		box-sizing: border-box;
		font-size: 50upx;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	#phoneNumberI input{
		width: 95%;
		height: 90%;
	}
	#checkClick{
		width: 700upx;
		height: 50upx;
		padding: 10upx 0 ;
		margin: 30upx 10upx;
		color: blue;
		font-size: 30upx;
		text-align: right;
	}
	#checks {
		width: 650upx;
		height: 200upx;
		/* background-color: #3F536E; */
		margin: 0 50upx;
		display: flex;
		flex-wrap: nowrap;
		justify-content: space-around;
		align-items: center;
	}
	#checks view{
		display: flex;
		width: 120upx;
		height: 150upx;
		background-color: #FFF;
		border-radius: 10upx;
		box-shadow: 0 0 10upx #dc3f44;	
	}
	#checks view input {
		width: 100upx;
		height: 100upx;
		/* background-color: #2C405A; */
		margin: 25upx 10upx;
		border-bottom: 6upx solid #dc3f44;
		font-size: 60upx;
		padding-left: 33upx;
	}
	#login {
		width: 650upx;
		height: 120upx;
		font-size: 50upx;
		background-color: #24324a;
		color: white;
		margin-top: 20%;
	}
</style>
