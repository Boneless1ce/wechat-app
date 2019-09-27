<template>
	<administration :info="info"></administration>
</template>

<script>
	import administration from '../../components/administration.vue'
	export default {
		data(){
			return {
				info:{
					list: 'collectionList',
					nullTitle: '还没有收藏的视频哦~'
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
