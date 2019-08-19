<template>
    <view class="datalist">
        <view class="datalist-item" v-for="item in dataList" :key="item.colid" @click="goRouter(item.name,item.nameid)">
            <view class="datalist-logo">
                <image src="../../static/news.png"></image>
            </view>
            <view datalist-title>
                {{item.name}}
            </view>
        </view>
    </view>
</template>

<script>
import tianxing from '../../tianxing'
export default {
    data(){
        return {
            dataList: []
        }
    },
    onLoad(){
        uni.request({
            url: tianxing.TXAPI_BASE_URL + '/channellist/',
            method: 'GET',
            data:{
                key: tianxing.TXAPI_KEY
            },
            success: (res)=>{
                this.dataList = res.data.newslist.slice(7);
            }
        })
    },
    methods:{
        goRouter(name,nameid){
            uni.navigateTo({
                url: "../news/news?id=" + nameid +'&name='+ name 
            })
        }
    }
}
</script>

<style>
    .datalist{
        width: 100%;
        margin-top: 10px;
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
    }
    .datalist-item{
        width: 33.33%;
        margin: 10px 0;
        display: flex;
        flex-direction: column;;
        justify-content: center;
        align-items: center;
    }

    .datalist-logo image{
        width: 100upx;
        height: 100upx;
    }
</style>
