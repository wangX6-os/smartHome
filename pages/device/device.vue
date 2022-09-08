<template>
	<view id = "frame" :style="{height: screenHeight+'px'}">
		<view id="head">
			<view class="info">
				1482532560的家
			</view>
			<view class="operation">
				<view class="addDeivce" @click="scanCodeQR()">
					<uni-icons type="scan" size="20"></uni-icons>
				</view>
			</view>
		</view>
		<uni-section class="mb-10" title="房间" type="line">
			<scroll-view class="scrollX" scroll-x="true">
				<view :class="[{'room': true}, {'roomActive': index == roomActiveIndex}]" @click="this.roomActiveIndex = index" v-for="(item, index) in rooms" :key="item.key">
					<img :src="item.icon">
					<text :class="[{'textActive': index == roomActiveIndex}]">{{ item.name }}</text>
				</view>
			</scroll-view>
		</uni-section>
		<uni-section class="mb-10" title="设备" type="line">
			<view class="devices">
				<view :class="[{'device': true}, {'deviceAc': item.isOpen}]" v-for="(item, index) in devices" :key="item.key">
					<view class="icon">
						<img :src="item.isOpen? item.icon2: item.icon1">
					</view>
					<text> {{ item.name }}</text>
					<view class="switch">
						<switch color="green" :checked="item.isOpen" @change="switchOpen(item)" />
					</view>
				</view>
			</view>
		</uni-section>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				screenHeight: 0,
				devices: [
					{
						key: 0,
						name: "空调",
						icon1: "../../static/devices/air.png",
						icon2: "../../static/devices/air1.png",
						isOpen: false
					},
					{
						key: 1,
						name: "电视",
						icon1: "../../static/devices/tv.png",
						icon2: "../../static/devices/tv1.png",
						isOpen: false
					},
					{
						key: 2,
						name: "冰箱",
						icon1: "../../static/devices/fri.png",
						icon2: "../../static/devices/fri1.png",
						isOpen: true
					},
					{
						key: 3,
						name: "洗衣机",
						icon1: "../../static/devices/wash.png",
						icon2: "../../static/devices/wash1.png",
						isOpen: true
					}
				],
				rooms: [
					{
						key: 0,
						name: "卧室1",
						icon: "../../static/room/wo.png",
					},
					{
						key: 1,
						name: "卧室2",
						icon: "../../static/room/wo.png",
					},
					{
						key: 2,
						name: "客厅",
						icon: "../../static/room/huan.png",
					},
					{
						key: 3,
						name: "浴室",
						icon: "../../static/room/ke.png",
					},
					{
						key: 4,
						name: "厨房",
						icon: "../../static/room/chu.png",
					}
				],
				roomActiveIndex: 0,
			}
		},
		mounted(){
			this.screenHeight = uni.getSystemInfoSync().windowHeight;
		},
		methods: {
			switchOpen(item){
				item.isOpen = !item.isOpen;
			},
			scanCodeQR(){
				uni.scanCode({
					onlyFromCamera: false,
					scanType: ['qrCode'],
					success(res){
						console.log(res)
					}
				})
			}
			
		}
	}
</script>

<style>
	#frame {
		width: 100%;
	}
	#head {
		width: 100%;
		height: 80upx;
	}
	.info {
		width: 300upx;
		height: 100%;
		float: left;
		margin: 0 50upx;
		line-height: 80upx;
		text-align: left;
		font-size: 25upx;
	}
	.operation {
		width: 200upx;
		height: 100%;
		float: right;
		margin: 0 20upx;
	}
	.operation .addDeivce {
		width: 60upx;
		height: 60upx;
		float: right;
		margin: 10upx 20upx;
		float: right;
		font-size: 50upx;
		line-height: 60upx;
		text-align: center;
	}
	.devices{
		width: 100%;
	}
	.device{
		width: 30%;
		height: 340upx;
		float: left;
		overflow: hidden;
		box-sizing: border-box;
		margin: 1.5%;
		border-radius: 16upx;
		box-shadow: 0 0 5upx #a1a1a1;
		background-color: white;
	}
	.devices .deviceAc {
		background-color: beige;
	}
	.device .icon{
		width: 100upx;
		height: 100upx;
		margin: 10upx auto;
		margin-top: 60upx;
	}
	.icon img {
		width: 100%;
		height: 100%;
	}
	.device text {
		display: block;
		width: 100%;
		text-align: center;
		font-size: 24upx;
	}
	.device .switch {
		width: 100%;
		height: 100upx;
		margin-top: 30upx;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.switch switch {
		/* display: block; */
		margin: 20upx auto;
		transform: scale(0.5);
	}
	.scrollX{
		width: 100%;
		white-space: nowrap;
		height: 200upx;
	}
	.scrollX .room {
		display: inline-block;
		width: 190upx;
		height: 170upx;
		margin: 5px;
		border-radius: 10upx;
		overflow: hidden;
		box-shadow: 0 0 3upx #e1e1e1;
		
	}
	.room img {
		display: block;
		width: 100upx;
		height: 100upx;
		margin: 10upx auto;
	}
	.room text {
		display: block;
		width: 100%;
		text-align: center;
		font-size: 25upx;
	}
	.roomActive {
		background-color: #34495e;
	}
	.room .textActive {
		color: white;
	}
</style>
