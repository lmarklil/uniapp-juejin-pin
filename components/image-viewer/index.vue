<template>
	<view class="image_viewer">
		<view class="image_viewer-toolbar">
			<view class="image_viewer-toolbar-page">{{page}}/{{imageCount}}</view>
			<view class="image_viewer-toolbar-action">
				<text class="iconfont icon-close"></text>
			</view>
		</view>
		<swiper class="image_viewer-content">
			<swiper-item v-for="(image,index) in images" :key="index">
				<image class="image_viewer-content-image" :src="image"></image>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		name: "ImagePreview",
		props: {
			images: {
				type: Array,
				default () {
					return [];
				}
			},
			page: {
				type: Number,
				default: 1
			}
		},
		computed: {
			imageCount() {
				return this.images.length;
			}
		}
	}
</script>

<style lang="scss">
	.image_viewer {
		position: absolute;
		top: 0;
		left: 0;
		z-index: 1;
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, .9);

		&-toolbar {
			display: flex;
			justify-content: space-between;
			align-items: center;
			padding: 0rpx 40rpx;
			height: 160rpx;
			color: #fff;
			font-size: 32rpx;

			&-page {}
		}

		&-content {
			display: flex;
			height: 100%;

			&-image {
				width: 100%;
				max-height: 100%;
				background: #ddd;
			}
		}
	}
</style>
