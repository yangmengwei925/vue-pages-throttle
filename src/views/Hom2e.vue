<template>
  <div class="swiper">
      <div class="moveL" @click="switchImg(-1)"><</div>
      <div 
      class="container" 
      @mouseenter="stopAuto"
      @mouseleave="startAuto">
        <ul ref="showImg">
          <li 
          v-for="(item, index) in imgArr" 
          :key="index" 
          :class="{'currentImg': index === selected}">
            <img :src="item.src" alt="">
          </li>
          <!-- 把第一张图片复制一份到最后，实现循环滚动无回滚 -->
          <li><img :src="imgArr[0].src" alt=""></li>
        </ul>
      </div>
      <div class="moveR" @click="switchImg(-2)">></div>
      <div class="footer">
        <ol>
          <li 
          v-for="(item, index) in imgArr" 
          :key="index" 
          :class="{'currentCircle': index === selected}"
          @click="switchImg(index)">
          </li>
        </ol>
      </div>
    </div>

</template>
<script>
export default{
     data(){
       return {

       }
   }
}
  
</script>