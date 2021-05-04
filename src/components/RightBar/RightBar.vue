<template>
    <div class="right" :style="{backgroundColor: bgColor}">
        <div class="recent">
            <!-- <div class="title">最近文章</div> -->
            <Recent/>
        </div>
        <div class="aboutBlog">
            <Blog/>
        </div>
        <div class="contact">
            <Contact/>
        </div>
    </div>
</template>

<script>
    import Recent from './Recent'
    import Blog from './Blog'
    import Contact from './Contact'

    export default {
        name: "RightBar",
        components: {
            Recent,
            Blog,
            Contact
        },
        computed: {
            bgColor() {
                return this.$store.state.bgColor
            }
        }
    }
</script>

<style lang="scss" scoped>
    .right {
        margin-top: 50px;
        // padding: 15px;
        background-color: rgba($color: #edeeea, $alpha: 0.6);
        width: 250px;
        font-size: 17px;

        ul {
            list-style: none;
        }

        .title {
            margin-bottom: 10px;
        }

        .recent {
            padding-top: 12px;
        }

        .aboutBlog {
            padding-top: 12px;
        }

        .contact {
            padding-top: 12px;
        }
    }
</style>