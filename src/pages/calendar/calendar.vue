<template>
    <view class="container">
        <func-title>
            老黄历
        </func-title>

        <view class="func-content">
            <text>
                选择日期:
            </text>
            <view class="func-input">
                <picker mode="date" :value="date" @change="bindChange">
                    <view>{{date}}</view>
                </picker>
            </view>
        </view>
        <hr>
        <view>
            <view v-for="(item,id) in res" :key="id">
                {{item}}
            </view>
        </view>
    </view>
</template>

<script>
import funcTitle from '../../components/funcTitle'
import tianxing from '../../tianxing'
import { setTimeout } from 'timers';
export default {
    components: {
        funcTitle
    },
    data(){
        return {
            date: '',
            res: ''
        }
    },
    methods: {
        getDate(){
            const getDate = new Date();
            let year = getDate.getFullYear();
            let month = getDate.getMonth() + 1;
            let day = getDate.getDate();

            this.date = `${year}-${month}-${day}`;
        },
        removeZero(str){
            let arr = str.split('');
            if(arr[5] == 0){
                arr.splice(5,1);
                if(arr[7] == 0){
                    arr.splice(7,1);
                }
            } else if(arr[8] == 0){
                arr.splice(8,1);
            }
            let str2 = arr.join('');
            this.date = str2;
        },
        bindChange(e){
            let str = e.target.value;
            this.removeZero(str);
            this.getSearch();
        },
        getSearch(){
            let that = this;
            uni.request({
                url: tianxing.TXAPI_BASE_URL +'/txapi/lunar/',
                data: {
                    key: tianxing.TXAPI_KEY,
                    date: that.date,
                },
                success(pop){
                    if(pop.data.code == 200){
                        const data = pop.data.newslist;
                        let dataList = [];
                        for(let k in data[0]){
                            dataList.push(data[0][k])
                        }
                        that.res = dataList.splice(1);
                    } else {
                        uni.showToast({
                            title:pop.data.msg,
                            icon:'none',
                            duration:2000
                        })
                    }
                }
            })
        }
    },
    onLoad(){
        this.getDate();
        this.getSearch();
    }
}
</script>

<style scoped>
    .container{
        margin: 0 20px;
    }
    .func-content{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
    }
    .func-content text{
        font-size: 56upx;
    }
    .func-input{
        flex: 1;
        border: 1px solid #000;
        border-radius: 10upx;
        padding: 20upx;
        margin: 0 20upx;
    }
</style>
