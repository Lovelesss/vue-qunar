<template>
    <div class="header">
        <div class="header-left">
            <div class="iconfont back-icon">&#xe611;</div>
        </div>
        <div class="header-input">
            <span class="iconfont search-icon">&#xe679;</span>
            输入城市/景点/游玩主题
        </div>
        <router-link to="/city">
            <div class="header-right">
                {{this.city}}
                <span class="iconfont arrow-icon">&#xe64a;</span>
            </div>
        </router-link>
    </div>

</template>

<script>
    import {mapState} from 'vuex'
    export default {
        name: "HomeHeader",
        data() {
            return {
                height: 0
            }
        },
        computed: {
            ...mapState(['city'])
        },
        mounted() {

        }
    }
</script>

<style lang="stylus" scoped>
    @import '~style/iconfont.css'
    @import '~style/varibles.styl';
    html
    .header
        display: flex
        height $headerHeight
        line-height $headerHeight
        background $bgColor
        color: #fff
        .header-left
            width .64rem
            float left
            text-align center
            .back-icon
                text-align center
                font-size .4rem
        .header-input
            flex 1
            height .64rem
            line-height .64rem
            margin-top .12rem
            margin-left .2rem
            padding-left: .2rem
            background #fff
            border-radius .1rem
            color #ccc
        .header-right
            min-width 1.04rem
            padding 0 .1rem
            float right
            text-align center
            color #fff
            .arrow-icon
                font-size .2rem
                margin-left -.04rem
</style>