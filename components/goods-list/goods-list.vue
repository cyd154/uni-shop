<template>
	<view class="goods_list">
		<view 
			class="goods_item" 
			v-for="(item,index) in goods" 
			:key="index"
			@click="navigator(item.goods_id)"
			>
			<image :src="item.goods_small_logo"></image>
			<view class="price">
				<text>￥{{item.goods_price}}</text>
				<text>￥{{item.goods_price}}</text>
			</view>
			<view class="name">{{item.goods_name}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:['goods'],
		data() {
			return {
				
			}
		},
		methods: {
			navigator(id) {
				this.$emit('navigator',id)
			}
		}
	}
</script>

<style lang="scss">
.goods_list{
	padding: 0 15rpx;
	display: flex;
	flex-wrap: wrap;
	justify-content: space-between;
	.goods_item{
		background-color: #fff;
		width: 355rpx;
		margin-bottom: 15rpx;
		padding: 15rpx;
		box-sizing: border-box;
		image{
			width: 80%;
			height: 150px;
			display: block;
			margin: auto;
		}
		.price{
			color: $shop-color;
			font-size: 35rpx;
			text:nth-child(2){
				color: #ccc;
				font-size: 28rpx;
				margin-left: 10rpx;
				text-decoration: line-through;
			}
		}
		.name{
			font-size: 28rpx;
			line-height: 45rpx;
			padding-top: 10rpx;
			display: -webkit-box;
			overflow: hidden;
			text-overflow: ellipsis;
			word-wrap: break-word;
			white-space: normal !important;
			-webkit-line-clamp: 2;
			-webkit-box-orient: vertical;
		}
	}
}
</style>
