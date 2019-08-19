<template>
    <view class="func">
        <view class="func-content">
            <view class="func-item" v-for="item in dataList" :key="item.page" @click="moreFunc(item.page)">
                {{item.name}}
            </view>
        </view>
    </view>
</template>

<script>
export default {
    data(){
        return {
            dataList:[
                {
                    name: '垃圾分类',
                    page: 'garbage'
                },
                {
                    name: '天气预报',
                    page: 'weather'
                },
                {
                    name: '老黄历',
                    page: 'calendar'
                }
            ]
        }
    },
    methods: {
        moreFunc(route){
            uni.navigateTo({
                url: '../' + route +'/'+ route
            })
        }
    }
}
</script>

<style>
    .func-content{
        margin: 20px;
    }
    .func-content .func-item{
        background: rgb(245, 227, 227);
        padding: 30upx;
        text-align: center;
        margin: 30upx 0;
        border: 5px solid #FB893A;
        border-radius: 30upx;
    }
</style>
