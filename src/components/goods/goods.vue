<template>
    <div class="goods">
        <div class="menu-wrapper">
            <ul>
                <li v-for="item in goods" :key="item.goods" class="menu-item">
                    <span class="text border-1px">
                        <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>
                        <span >{{item.name}}</span>
                    </span>
                </li>
            </ul>
        </div>
        <div class="foods-wrapper">
            <ul>
                <li v-for="item in goods" :key="item.id" class="food-list">
                    <h1 class="title">{{item.name}}</h1>
                    <ul>
                        <li v-for="food in item.foods" class="food-item  border-1px" :key="food.id">
                            <div class="icon">
                                <img :src="food.icon">
                            </div>
                            <div class="content">
                                <h2 class="name">{{food.name}}</h2>
                                <p class="desc">{{food.description}}</p>
                                <div class="extra">
                                    <span>月售{{food.sellCount}}份</span>
                                    <span>好评率{{food.rating}}%</span>
                                </div>
                                <div class="price">
                                    <span>￥{{food.price}}</span>
                                    <span v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                                </div>
                            </div>
                        </li>
                    </ul>
                </li>
            </ul>
        </div>
    </div>
</template>
<script type='text/ecmascript-6'>
    const ERR_OK = 0;
    export default{
        data(){
            return {
                goods:[]
            }
        },
        props:{
            seller:{
                type:Object
            }
        },
        created(){
            this.classMap = ['decrease','discount','special','invoice','guarantee'];
            this.$http.get('/api/goods').then((res)=>{
                var response = res.body;
                this.goods = response
            });
        }
    };
</script>
<style lang='stylus' rel='stylesheet/stylus'>
    @import '../../common/stylus/mixin';
    .goods
        position absolute 
        top 174px
        width 100%
        bottom 46px
        display flex
        overflow hidden
        .foods-wrapper
            flex 1
            .title
                padding-left 28px
                height 26px
                line-height 36px
                border-left 2px solid #d9dde1
                font-size 12px
                color rgb(147,153,159)
                background #f3f5f7
                padding-bottom 18px
            .food-item
                display flex
                margin 18px 
                border-1px(rgba(7,17,27,0.1))
                &:last-child
                    border-none()
        .menu-wrapper
            flex 0 0 80px
            width 80px
            background #f3f5f7
            .menu-item
                padding 0 12px
                display table
                height 54px
                width 56px
                line-height 14px
                .icon
                    display inline-block
                    vertical-align top
                    width 12px
                    height 12px
                    margin-right 2px
                    margin-right 4px
                    background-size 12px 12px
                    background-repeat no-repeat
                    &.decrease
                        bg-image('decrease_3')
                    &.discount
                        bg-image('discount_3')
                    &.invoice
                        bg-image('invoice_3')
                    &.guarantee
                        bg-image('guarantee_3')
                    &.special
                        bg-image('special_3')
                .text
                    font-size 12px
                    display table-cell
                    width 56px
                    vertical-align middle
                    border-1px(rgba(7,17,27,0.1))
        .foods-wrapper
            flex 1




</style>