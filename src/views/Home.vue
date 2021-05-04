<template>
  <div id="index">
      <div class="container" v-if="!isAdmin">
        <Header :showSome="showSome"></Header>
        <div v-show="!TypeChange" class="moon"></div>
        <div v-show="TypeChange"  class="night"></div>
        <Light @changeBackground="changeBG"/>

        <div class="content">
            <LeftBar :showSome=showSome />

            <div class="main" :style="{backgroundColor: bgColor}" ref="main">
                <!-- <div class="header">
                    <h1>Heartless</h1>
                    <h3>迷失的人迷失了，相逢的人会再相逢</h3>
                </div> -->
                <keep-alive>
                    <router-view class="router" :style="{backgroundColor: bgColor}"/>
                </keep-alive>
                <div class="foot">
                    粤ICP备2021032727号
                </div>
            </div>

            <RightBar v-if="showSome"/>
        </div>
        <Music v-if="!showSome"/>
      </div>

      <div v-if="isAdmin">
            <div class="moon"></div>
            <keep-alive>
                <router-view class="router_content"></router-view>
            </keep-alive>
      </div>
  </div>
</template>

<script>
import eventBus from '../utils/eventBus'
import Header from '../components/Header/Header'
import Light from '../components/highlight/light'
import RightBar from '../components/RightBar/RightBar'
import LeftBar from '../components/LeftBar/LeftBar'
import Music from '../components/Index/IndexMusic'

export default {
    components: {
        Header,
        Light,
        RightBar,
        LeftBar,
        Music,
    },
    data() {
        return {
            screenWidth: document.documentElement.clientWidth,//屏幕宽度
            showSome: true,
            isAdmin: false
        }
    },
    watch: {
        'screenWidth':function(val){
            if(val>1200){
                this.$refs.main.style.marginLeft = "232px"
                this.showSome = true
            } else {
                this.$refs.main.style.marginLeft = "232px"
                this.showSome = false
            }
        }
    },
    computed: {
        Color() {
            return this.$store.state.Color
        },
        TypeChange() {
            return this.$store.state.fontColor
        },
        bgColor() {
            return this.$store.state.bgColor
        }
    },
    async beforeMount() {
        if(!window.location.href.includes('admin')){
            this.isAdmin = false
        } else {
            this.isAdmin = true
        }
        if(this.screenWidth<1200){
            this.showSome = false
        } else {
            this.showSome = true
        }
    },
    beforeUpdate() {
        if(!this.$route.path.includes('admin')){
            this.isAdmin = false
        } else {
            this.isAdmin = true
        }
        // 接受Header的控制参数
        const that = this
        eventBus.$on('eventFromHeader', function(val) {
            if (val) {
                that.$refs.main.style.marginLeft = "232px"
            } else {
                that.$refs.main.style.marginLeft = "0"
            }
        })
    },
    methods: {
        changeBG() {
            this.$store.commit('updatefont', !this.$store.state.fontColor)
            // console.log(this.$store.state.backgroundColor)
            // console.log(this.$store.state.bgColor)
            this.$store.commit('updateBgColor', !this.$store.state.backgroundColor)
        },
    }
}
</script>

<style lang='scss' scoped>
body,html{
    width: 100%;
    height: 100%;
}
#index{
    display: flex;
    flex-direction: column;
    width: 100%;
    .moon,.night {
        width: 100%;
        height: 100%;
        position: fixed;
        left: 0;
        top: 0;
        z-index: -1;
    }
    .night {
        background: url('../assets/images/night.gif') center;
    }
    .moon {
        background: url('../assets/images/meinv.jpg') no-repeat;
        background-size: 100% 100%;
    }
}
.container{
    width: 1380px;
    margin: 0 auto;
    .content{
        display: flex;
        flex-direction: row;
        .main{
            margin-top: 50px;
            margin-left: 232px;
            width: 900px;
            min-height: 100vh;
            position: relative;
            transition: all 1s;
            background-color: rgba($color: #f2f2f2, $alpha: 0.6);
            .header{
                height: 102px;
                width: 900px;
                padding: 20px;
                // background-color: #edeeea;
                h1{
                    font-weight: 700;
                }
                h3{
                    font-weight: 600;
                }
            }
            .router{
                width: 100%;
                padding: 10px;
                min-height: 95vh;
                box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
                background-color: rgba($color: #f2f2f2, $alpha: 0.6);
                animation: animate 2s;
            }
            .foot{
                // width: 96%;
                height: 36px;
                line-height: 36px;
                margin: 0 auto;
                text-align: center;
                background-color: rgba($color: #f2f2f2, $alpha: 0.6);
            }
        }
    }
}

/* @media screen and (max-width:992px) {
    #index{
        overflow: hidden;
    }
} */

@media screen and (max-width:1200px) {
  .container{
    width: 100%;
    // overflow: hidden;
    position: relative;
    .content{
        height: 100%;
        .left{
            height: calc(100% - 52px);
            min-height: 100vh;
            position: fixed;
            .scroll{
                height: auto;
            }
        }
        .main{
            min-width: 100%;
            margin-left: 0;
        }
    }
    // .right{
    //     display: none;
    // }
  }
}

.el-menu-vertical-demo{
    background-color: rgba($color: #2b2c28, $alpha: 0.6);
    el-menu-item{
        background-color: rgba($color: #2b2c28, $alpha: 0.6);
    }
    el-menu-item:hover{
        background-color: rgba($color: #2b2c28, $alpha: 0.6);
    }
    .el-menu-item:focus, .el-menu-item:hover{
        background-color: rgba($color: #2b2c28, $alpha: 0.6);
    }
}

.router_content {
    animation: animate 2s;
}

@keyframes animate {
    0% { opacity: 0; transform: translateY(-50px);}
    100% { opacity: 1; transform: translateY(0);}
}

</style>