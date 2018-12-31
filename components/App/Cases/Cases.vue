<template>
  <section class="section" id="Cases">
    <div class="container">
      <h2 class="section-title" data-aos="fade-down" data-aos-anchor-placement="top-center">My cases</h2>
      <ul class="cases">
        <li
          v-for="(item, index) in cases"
          :key="item.id"
          class="cases__item"
          data-aos="fade-flip"
          data-aos-duration="1000"
          :data-aos-delay="index * 200"
        >
          <button
            class="cases__btn btn-default"
            @click="handleFlip"
          >
            <div class="cases__flipper">
              <div class="cases__container cases__container--front">
                <div class="cases__icon">
                  <span v-for="icon in item.icons" :key="icon" :class="['cases__ico', icon]" />
                </div>
                <h3 class="cases__title">{{ item.title }}</h3>
                <div class="cases__details">Details <span class="fas fa-arrow-circle-right" /></div>
              </div>
              <div class="cases__container cases__container--back">
                <div v-html="item.text" />
                <span class="cases__icon-back fas fa-arrow-circle-left" />
              </div>
            </div>
          </button>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Cases',
  data () {
    return {
      flippedCases: []
    }
  },
  computed: {
    cases () {
      return [{
        id: 'responsive',
        title: 'Responsive',
        icons: ['fas fa-mobile-alt', 'fas fa-desktop', 'fas fa-tablet-alt'],
        text: '<p>My layouts will work on any device, big or small.</p><p>The range of supported extensions from small 320px screen devices to large 1920px+ monitor wide screens.</p>'
      }, {
        id: 'fast',
        title: 'Fast',
        icons: ['fas fa-bolt', 'fas fa-tachometer-alt', 'fas fa-rocket'],
        text: '<p>Fast load times my highest priority.</p><p>Optimization with the help of various auditors using best practices of image optimization, minification and compression, code splitting, etc.</p>'
      }, {
        id: 'browser',
        title: 'Cross-browser',
        icons: ['fab fa-firefox', 'fab fa-edge', 'fab fa-chrome'],
        text: '<p>Providing all of required features in your browser list</p><p>Supporting of all modern browsers including Edge and IE11 with helping of Post CSS, Babel and different polyfills</p>'
      }, {
        id: 'code',
        title: 'Code quality',
        icons: ['fab fa-node-js', 'fab fa-css3-alt', 'fab fa-html5'],
        text: '<p>Scalable, structured, clean and well organized code.</p><p>My main goal during development process and I always try to achieve it with DRY, KISS, YAGN principes and using code best practices.</p>'
      }]
    }
  },
  methods: {
    handleFlip (e) {
      let element = e.target
      for (let i = 0; i <= 5; i++) {
        if(element.classList.contains('is-flipped')) {
          element.classList.remove('is-flipped')
          return
        } else if (element.tagName === 'BUTTON') {
          element.classList.add('is-flipped')
          break
        } else if (element.tagName === 'BODY') break
        
        element = element.parentNode
      }
    }
  }
}
</script>

<style lang="scss">
@import "cases";
</style>