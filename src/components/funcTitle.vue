<template>
    <view class="func-title">  
        <slot></slot>
    </view>
</template>

<script>
export default {

}
</script>

<style>
    .func-title{
        font-size: 50upx;
        background: linear-gradient(35deg,#FB893A,#F5E3E3);
        -webkit-text-fill-color: transparent;
        background-clip: text;
        margin: 30px 0;
    }
</style>
