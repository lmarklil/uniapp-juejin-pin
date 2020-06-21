<template>
	<view class="pin">
		<view class="pin-user">
			<image class="pin-user-avatar" :src="pin.user.avatarLarge"></image>
			<view class="pin-user-info">
				<view class="pin-user-name">{{pin.user.username}}</view>
				<view class="pin-user-job"><text>{{pin.user.jobTitle}}</text></view>
			</view>
		</view>
		<view class="pin-content">{{pin.content}}</view>
		<view class="pin-pictures">
			<image v-for="(picture,index) in pin.pictures" :key="index" :class="['pin-pictures-item',{'__single':pin.pictures.length===1}]"
			 :src="picture" mode="aspectFill" lazy-load></image>
		</view>
		<view class="pin-actions">
			<view class="pin-actions-item"><text class="iconfont icon-praise" style="margin-right:10rpx;"></text>{{pin.likeCount}}</view>
			<view class="pin-actions-item" @tap="viewComments"><text class="iconfont icon-message" style="margin-right:10rpx;"></text>{{pin.commentCount}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			pin: {
				type: Object,
				required: true
			}
		},
		methods: {
			viewComments() {
				uni.navigateTo({
					url: `/pages/comments/comments?id=${this.pin.id}`
				});
			}
		}
	}
</script>

<style lang="scss">
	.pin {
		margin-bottom: 20rpx;
		padding: 30rpx;
		background: #fff;

		&-user {
			display: flex;
			align-pins: flex-start;
			margin-bottom: 20rpx;

			&-avatar {
				margin-right: 20rpx;
				width: 69rpx;
				height: 69rpx;
				background: #ddd;
				border-radius: 50%;
			}

			&-name {
				margin-bottom: 10rpx;
				font-size: 28rpx;
				font-weight: bold;
			}

			&-job {
				color: #999;
				font-size: 22rpx;
			}
		}

		&-content {
			margin-bottom: 20rpx;
			color: #333;
			font-size: 28rpx;
			letter-spacing: 0.04em;
			line-height: 1.5em;
		}

		&-pictures {
			display: flex;
			flex-wrap: wrap;
			margin: -5rpx;

			&-item {
				margin: 5rpx;
				width: 200rpx;
				height: 200rpx;
				background: #ddd;
				
				&.__single {
					width:100%;
					height:400rpx;
				}
			}
		}

		&-actions {
			display: flex;
			justify-content: space-between;

			&-item {
				flex-grow: 1;
				display: flex;
				justify-content: center;
				align-items: center;
				margin-top: 20rpx;
				font-size: 20rpx;
			}
		}
	}
</style>
