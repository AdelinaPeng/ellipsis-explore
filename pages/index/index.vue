<template>
	<view class="content">
		<view>
			<view class='title-box'>
				<label>content:</label>
				<button type='primary' class="mini-btn" size='mini' v-show="isOverflowed" @click="changeOverflowStatus">
					{{isCollapsed?'Collapse &uarr;':'Open &darr;'}}
				</button>
			</view>
			<view class="text-wrapper" :class="{'not-overflow':isCollapsed}">
				<!-- is overflowed -->
				<text class="text">
					This is a demo to use a button to control whether it shows the whole content text or show part text with the ellipsis, thanks for my efforts, I make it,I make it,I can make it
				</text>
				<!-- not overflowed -->
				<!-- <text class="text">
					This is a demo
				</text>	 -->
			</view>	
		</view>				
	</view>
</template>

<script>
	export default {
		data() {
			return {
				isOverflowed: false,
				isCollapsed: false				
			}
		},
		onLoad() {
			let query = uni.createSelectorQuery();
			let textHeight,wrapperHeight;
			
			query.select(".text-wrapper").boundingClientRect(data=>{
				wrapperHeight = data.height;
			});			
			
			query.select(".text").boundingClientRect(data=>{
				textHeight = data.height;
			});
			
			query.exec(()=>{
				if(textHeight > wrapperHeight){
					this.isOverflowed = true;
				}else{
					this.isOverflowed = false;
				}				
			});
		},
		methods: {
			changeOverflowStatus(){
				this.isCollapsed = !this.isCollapsed;
			},			
		}
	}
</script>

<style scoped lang='scss'>
	.content {
		padding: 25rpx;
	}	
	.title-box {
		display: flex;
		.mini-btn {
			margin-left: auto;
			margin-right: 0;
		}
	}
	.text-wrapper {
		font-size: 30rpx;
		margin-top: 30rpx;
		display:-webkit-box;
		-webkit-line-clamp:2;
		-webkit-box-orient:vertical;
		overflow:hidden;
		
		&.not-overflow {
			-webkit-line-clamp: unset;
			overflow: auto;
		}		
	}

</style>
