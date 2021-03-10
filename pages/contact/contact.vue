<template>
	<view class="contact"> 
		<image class="img" src="../../static/photo-1533922239335-e5ad4f9728f9.jpg" mode="aspectFill"></image>
		<view class="info">
			<view>联系电话：13988888888</view>
			<view>地址：湖北省仙桃市钱沟路59号</view>
		</view>
		<map class="map" :longitude="longitude" :latitude="latitude"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:'113.4545',
				latitude:'30.36251'
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss">
.contact{
	.img{
		width: 750rpx;
		height: 320rpx;
	}
	.info{
		padding: 10rpx 20rpx;
		font-size: 30rpx;
		view{
			line-height: 70rpx;
			border-bottom: 1px solid #eee;
		}
	}
	.map{
		width: 750rpx;
		height: 400rpx;
	}
}

</style>
