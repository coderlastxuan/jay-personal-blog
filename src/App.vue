<template>
  <div id="app">
    <Home />
    <canvas id="snowDown"></canvas>
  </div>
</template>

<script>
import Home from './views/Home'
import snow from './utils/canvas'

export default {
  name: 'app',
  data() {
    return {

    }
  },
  components: {
    Home
  },
  mounted() {
    snow('snowDown')
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  // background-color: #232420;
}
#snowDown {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 99999;
    // background: rgba(125,137,95,0.1);
    pointer-events: none;
}
// @media screen and (max-width: 1920px) {
//   html {
//     font-size: 19.2px;
//   }
// }
// @media screen and (max-width: 1680px) {
//   html {
//     font-size: 16.8px;
//   }
// }
// @media screen and (max-width: 1380px) {
//   html {
//     font-size: 14.4px;
//   }
// }
/* @media screen and (max-width: 1300px) {
  html {
    font-size: 12.8px;
  }
}
@media screen and (max-width: 1200px) {
  html {
    font-size: 10.8px;
  }
}
@media screen and (max-width: 992px) {
  html {
    font-size: 8.8px;
  }
}
@media screen and (max-width: 768px) {
  html {
    font-size: 7.8px;
  }
}
@media screen and (max-width: 668px) {
  html {
    font-size: 6.8px;
  }
} */
</style>
