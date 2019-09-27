<template>
	<administration :info="info"></administration>
</template>

<script>
	import administration from '../../components/administration.vue'
	export default {
		data(){
			return {
				info:{
					list: 'watchLaterList',
					nullTitle: '暂无可观看的视频，请添加'
				}
			}
		},
		components: {
			administration,
		}

	}
</script>

<style>
	page{
		background: #F2F2F2;
	}
</style>
