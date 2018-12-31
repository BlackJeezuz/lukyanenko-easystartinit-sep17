<template>
  <transition name="modal">
    <div class="overlay" @click.self="handleClose(event)">
      <div class="popup">
        <header class="popup__header">
          <Carousel
            class="slider"
            :perPage="1"
            :navigationEnabled="true"
            :paginationEnabled="false"
            :loop="true"
            :paginationPosition="'bottom-overlay'"
            @pageChange="handleChange"
          >
            <Slide
              v-for="(slide, index) in project.slides"
              :key="`slide-${index}`"
              class="slider__item"
            >
              <div class="slider__img" :style="{ backgroundImage: `url(${slide.img})`}" />
            </Slide>
          </Carousel>
        </header>
        <transition name="slide-fade" mode="out-in">
          <main class="popup__content" :key="activeSlide" v-html="project.slides[activeSlide].info" />
        </transition>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'Popup',
  props: {
    project: {
      type: Object,
      default: () => { return {} }
    }
  },
  data () {
    return {
      activeSlide: 0
    }
  },
  methods: {
    handleChange (slideNumber) {
      this.activeSlide = slideNumber
    },
    handleClose (event) {
      this.$emit('close')
    }
  }
}
</script>

<style lang="scss">
@import "popup";
</style>