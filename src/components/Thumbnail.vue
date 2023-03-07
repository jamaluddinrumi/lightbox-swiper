<script>
import { Thumbs } from 'swiper'
import { Swiper, SwiperSlide } from 'swiper/vue/swiper-vue.js'

export default {
  components: {
    Swiper, 
    SwiperSlide
  },
  props: {
    currentSlide: Number
  },
  emits: ['thumbs', 'update:currentSlide'],
  setup(props, { emit }) {
    const onSwiper = (swiper) => {
      emit('thumbs', swiper)
    }

    return {
      onSwiper,
      Thumbs
    }
  }
}
</script>

<template>
  <Swiper @swiper="onSwiper" :slides-per-view="10" :space-between="50" :modules="[Thumbs]" watch-slides-progress>
    <SwiperSlide v-for="n in 20" :key="n" @click.stop="$emit('update:currentSlide', Number(n) - 1)">
      <img :src="'https://picsum.photos/id/'+n+'/640/480'" style="height: 100px" />
    </SwiperSlide>
  </Swiper>
</template>