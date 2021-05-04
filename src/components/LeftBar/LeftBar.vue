<template>
    <div class="left" ref="left">
        <div class="info">
            <div class="img">
                <img src="@/assets/images/baby.jpg">
            </div>
            <div class="intro">
                <p class="name">JWTBryant</p>
                <p class="desc">一期一会</p>
            </div>
        </div>
        <div class="scroll">
            <div class="nav">
                <el-row style="height:100%">
                    <el-col :span="8" style="height:100%; width:232px; background:rgba($color:#2b2c28,$alpha:0.6)">
                        <el-menu
                                class="el-menu-vertical-demo"
                                text-color="#cbced4"
                                active-text-color="#fff"
                        >
                            <div class="navTitle">
                                <span>导航</span>
                            </div>
                            <el-menu-item index="1" @click="$router.push('/article')">
                                <i class="el-icon-menu"></i>
                                <span slot="title">首页</span>
                            </el-menu-item>
                            <el-menu-item index="2" @click="$router.push('/demo')">
                                <i class="el-icon-video-camera"></i>
                                <span slot="title">Demo</span>
                            </el-menu-item>
                            <el-menu-item index="3" @click="$router.push('/photos')">
                                <i class="el-icon-picture-outline"></i>
                                <span slot="title">云相册</span>
                            </el-menu-item>
                            <el-menu-item index="4" @click="$router.push('/message')">
                                <i class="el-icon-chat-dot-round"></i>
                                <span slot="title">留言板</span>
                            </el-menu-item>
                            <el-menu-item index="5" @click="$router.push('/profile')">
                                <i class="el-icon-user"></i>
                                <span slot="title">个人信息</span>
                            </el-menu-item>
                            <div class="navTitle">
                                <span>其他</span>
                            </div>
                            <!-- <el-submenu index="4">
                                <template slot="title">
                                <i class="el-icon-menu"></i>
                                    <span slot="title">文章分类</span>
                                </template>
                                <el-menu-item @click.native="$router.push('/admin/article/upload/users')" index="2-1">用户列表管理</el-menu-item>
                            </el-submenu> -->
                            <Category/>
                            <el-menu-item index="7" @click="goAdmin" v-if="showSome">
                                <i class="el-icon-setting"></i>
                                <span slot="title">后台管理</span>
                            </el-menu-item>
                            <el-menu-item index="7" @click="goGithub">
                                <i class="iconfont icon-github" style="padding: 5px;padding-right:8px"></i>
                                <span slot="title">Github</span>
                            </el-menu-item>
                        </el-menu>
                    </el-col>
                </el-row>
            </div>
        </div>
        <!-- <div class="bottom">
            <i class="el-icon-setting"></i>管理后台
        </div> -->
    </div>
</template>

<script>
    import eventBus from '../../utils/eventBus'
    import Category from '../ArticleComponents/Category'
    export default {
        name: "LeftBar",
        components: {
            Category
        },
        props: {
            showSome: Boolean
        },
        data() {
            return {
                screenWidth: document.documentElement.clientWidth,//屏幕宽度
            }
        },
        watch: {
            'screenWidth':function(val){
                if(val>1200){
                    this.$refs.left.style.left = "";
                } else {
                    this.$refs.left.style.left = '0px'
                }
            }
        },
        async mounted() {
            let that = this;
            if(this.screenWidth<1200){
                this.$refs.left.style.left = '-232px'
            }
            window.onresize = function(){
                that.screenWidth = document.documentElement.clientWidth;
            }
        },
        beforeUpdate() {
            // 接受Header的控制参数
            const that = this
            eventBus.$on('eventFromHeader', function(val) {
                if (val) {
                    that.$refs.left.style.left = '0'
                } else {
                    that.$refs.left.style.left = '-232px'
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
            // 跳转到github
            goGithub() {
                window.open='https://github.com/Chen-12138'
            },
            // 跳转到后台管理
            goAdmin() {
                this.$router.push('/admin');
            }
        }
    }
</script>

<style lang="scss" scoped>
    .left{
        position: fixed;
        transition: all 1s;
        margin-top: 50px;
        width: 232px;
        height: 100%;
        min-height: 100vh;
        background-color: rgba($color: #2b2c28, $alpha: 0.6);
        .info{
            height: 96px;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 15px;
            border-bottom: 2px solid #dae0de;
            .img{
                margin-right: 15px;
                width: 50px;
                height: 50px;
                border-radius: 50%;
                box-shadow: 0 0 5px #ccc;
                overflow: hidden;
                img{
                    width: 100%;
                    height: 100%;
                    transition: all 1s;
                }
                :hover{
                    transform: rotate(360deg);
                }

            }
            .intro{
                .name{
                    font-size: 14px;
                    margin-bottom: 5px;
                    color: lightblue;
                    font-weight: bold;
                }
                .desc{
                    color: #a0a0a0;
                    font-size: 12px;
                }
            }
        }
        .scroll{
            top: 148px;
            bottom: 0;
            position: fixed;
            height: 100%;
            overflow-y: scroll;
            overflow-x: scroll;
        }
        .nav{
            position: relative;
            ::v-deep .el-menu-vertical-demo {
                background-color: rgba($color: #2b2c28, $alpha: 0.6);
            }
            .navTitle{
                height: 18px;
                padding: 0 15px;
                margin-top: 10px;
                margin-bottom: 15px;
                color: #a0a0a0;
            }
        }
        ::-webkit-scrollbar {
            display: none;
        }
        ::-webkit-scrollbar-thumb{
            display: none;
        }
    }
</style>