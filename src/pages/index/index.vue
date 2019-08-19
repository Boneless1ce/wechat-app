<template>
	<view class="content">
		<swiperComponent></swiperComponent>
		<search-text></search-text>
		<daily-video></daily-video>
	</view>
</template>

<script>
import tianxing from '../../tianxing'
import swiperComponent from '../../components/swiper'
import searchText from '../../components/searchText'
import dailyVideo from '../../components/dailyVideo'

export default {
	components: {
		swiperComponent,
		searchText,
		dailyVideo
	}
}
</script>

<style>
	.content {
		text-align: center;
	}
</style>
