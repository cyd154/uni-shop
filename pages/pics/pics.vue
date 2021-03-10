<template>
	<view class="pics">
		<scroll-view class="left" scroll-y>
			<view 
				:class="active===index ? 'active' : ''" 
				v-for="(item,index) in categoriesList" 
				:key="index"
				@click="leftClickitem(index)"
				>{{item.cat_name}}</view>
		</scroll-view>
		<scroll-view class="right" scroll-y>
			<view v-for="(item,index) in itemList" :key="index">
				<view class="item-a">
					<h4>{{item.cat_name}}</h4>
				</view>
				<view class="flexa">
				<view class="item-b" v-for="(itema,index) in item.children">
					<image :src="itema.cat_icon"></image>
					<text>{{itema.cat_name}}</text>
				</view>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				categoriesList:[],
				itemList:[],
				active: 0
			}
		},
		onLoad() {
			this.getCategories()
		},
		methods: {
			async getCategories() {
				const res = await this.$http({
					url:'/categories'
				})
				this.categoriesList = res.data.message
				// console.log(this.categoriesList)
				this.itemList = this.categoriesList[0].children
				// console.log(this.itemList)
			},
			leftClickitem(index) {
				this.active = index
				this.itemList = []
				this.itemList = this.categoriesList[index].children
			}
		}
	}
</script>

<style lang="scss">
page{
	height: 100%;
}
.pics{
	height: 100%;
	display: flex;
	.left{
		width: 170rpx;
		height: 100%;
		view{
			height: 46px;
			line-height: 46px;
			text-align: center;
			color: #333;
			font-size: 30rpx;
		}
		.active{
			color: $shop-color;
		}
	}
	.right{
		height: 100%;
		width: 540rpx;
		margin: 0 auto;
		margin: 28rpx 14rpx 0;
		.item-a{
			margin: 30rpx 14rpx 0;
		}
		.flexa{
			display: flex;
			flex-wrap:wrap;
			justify-content: space-between;
			.item-b{
				width: 140rpx;
				height: 140rpx;
				text-align: center;
				padding: 14rpx 20rpx 0;
				margin-bottom: 50rpx;
				image{
					width: 140rpx;
					height: 140rpx;
				}
				text{
					font-size: 24rpx;
				}
			}
		}
	}
	/deep/.uni-scroll-view::-webkit-scrollbar {
	/* 隐藏滚动条，但依旧具备可以滚动的功能 */
		display: none
	}
}
</style>
