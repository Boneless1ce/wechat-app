<template>
    <view>
        <view class="videolist">
            <view class="videolist-item" v-for="item in videoList" :key="item.data.content.data.id">
                <daily-video-item :item="item"></daily-video-item>
            </view>
        </view>
    </view>
</template>

<script>
import dailyVideoItem from './dailyVideoItem'
export default {
    data(){
        return {
            videoList: []
        }
    },
    components: {
        dailyVideoItem
    },
    onReady() {
        uni.request({
            url: 'https://api.apiopen.top/videoCategoryDetails?id=14',
            method: 'GET',
            success: (res)=>{
                this.videoList = res.data.result;
            }
        })
    }
}
</script>

<style>
    .videolist{
        width: 85%;
        margin: 0 auto 20px;
        text-align: left;
    }
    .videolist-item{
        margin: 20upx 0;
    }
</style>
