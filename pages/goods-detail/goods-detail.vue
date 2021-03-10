<template>
	<view class="goods_detail">
		<swiper indicator-dots>
			<swiper-item v-for="(item,index) in goodsDetail.pics" :key="index">
				<image mode="aspectFit" :src="item.pics_mid"></image>
			</swiper-item>
		</swiper>
		<view class="box1">
			<view class="price">
				<text> ￥{{goodsDetail.goods_price}}</text>
				<text>库存：{{goodsDetail.goods_number}}</text>
			</view>
			<view class="goods_name">{{goodsDetail.goods_name}}</view>
		</view>
		<rich-text :nodes="goodsDetail.goods_introduce"></rich-text>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				goodsDetail:[]
			}
		},
		onLoad(op) {
			this.getGoodsDetail(op.id)
		},
		methods: {
			async getGoodsDetail(id) {
				const res = await this.$http({
					url:'/goods/detail',
					data: {
						goods_id: id
					}
				})
				// console.log(res)
				this.goodsDetail = res.data.message
			}
		}
	}
</script>

<style lang="scss">
.goods_detail{
	swiper{
		width: 750rpx;
		height: 480rpx;
		image{
			width: 100%;
			height: 100%;
		}
	}
	.box1{
		padding: 20rpx;
		.price{
			font-size: 40rpx;
			color: $shop-color;
			line-height: 70rpx;
			text:nth-child(2){
				color: #333333;
				font-size: 25rpx;
				margin-left: 40rpx;
			}
		}
		.goods_name{
			font-size: 32rpx;
			line-height: 60rpx;
		}
	}
}
</style>
