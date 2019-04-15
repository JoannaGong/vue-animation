<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1>Animations</h1>
        <button class="btn btn-primary" @click="show = !show">点击</button><br><br>
        
        <select v-model="animatedName" class="form-control">
          <option value="fade">Fade</option>
          <option value="slide">Slide</option>
        </select><br>

        <transition :name="animatedName" appear>   // 提示该标签内部是动画效果，且只能使用一个元素标签
          <div class="alert alert-info" v-show="show">alert 1</div>
        </transition>

        <transition name="slide" type="animation">   // 提示该标签内部是动画效果，且只能使用一个元素标签
          <div class="alert alert-info" v-show="show">alert 2</div>
        </transition>

        <transition
          enter-class="enter"
          enter-active-class="animated bounce"
          leave-active-class="animated shake"
          enter-to-class="to">        // 自定义动画过渡的类名，通常与第三方css库使用，例如animation.css库
          <div class="alert alert-info" v-show="show">alert 3</div>
        </transition>

        
        <transition :name="animatedName" appear mode="out-in">   // 提示该标签内部是动画效果，且只能使用一个元素标签
          // 使用mode，可以使下面两个div的内容先出后进，错开出现
          // 设置不同的key值，可以使div的内容不只是简单的文字替换
          <div class="alert alert-info" v-if="show" key="info">alert 4</div>
          <div class="alert alert-info" v-else key="warning">alert 5</div>
        </transition>

      </div>
    </div>
    
  </div>
</template>

<script>
export default {
  data(){
    return {
      show: true,
      animatedName: 'fade'
    }
  }
}
</script>


<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

.fade-enter {
  opacity: 0;
}
.fade-enter-active {   // 如何运动
  transition: opacity 1s;
}
.fade-enter-to {
  opacity: 1;
}
.fade-leave {
  opacity: 1;
}
.fade-leave-active {   // 如何运动
  transition: opacity 1s;
}
.fade-leave-to {
  opacity: 0;
}

.slide-enter {
  transform: translateY(20px);
}
.slide-enter-active {
  animation: slide-in 1s ease-in-out;
}
.slide-enter-to {
  transform: translateY(0);
}
.slide-leave {
  transform: translateY(0);
}
.slide-leave-active {
  animation: slide-out 1s ease-in-out;
}
.slide-leave-to {
  transform: translateY(20px);
}

@keyframes slide-in {
  from {
    transform: translateY(0);
  }
  to{
    transform: translateY(20px);
  }
}
@keyframes slide-out {
  from {
    transform: translateY(20px);
  }
  to{
    transform: translateY(0);
  }
}

.enter {
  opacity: 0;
}
.active {
  transition: opacity 3s;
}
.to {
  opacity: 1;
}
</style>
