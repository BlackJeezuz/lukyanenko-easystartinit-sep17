<template>
  <header :class="['header', { 'is-floating': isFloating }]">
    <div class="container header__container">
      <nav class="header__nav" id="nav">
        <ul class="header__nav-list">
          <li class="header__nav-item" v-for="section in sections" :key="section.id">
            <a :class="['header__nav-link', {'is-active': activeSection === section.id}]" :href="`#${section.id}`" @click.prevent="scrollTo(section.id)">{{ section.id }}</a>
          </li>
        </ul>
      </nav>
    </div>
    <span class="progress" :style="{ width: `${progress}%` }"/>
  </header>
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {
      isFloating: false,
      activeSection: 'Home',
      progress: 0,
      sections: [{
        id: 'Home',
        scrollStart: 0,
        height: 0
      }, {
        id: 'Cases',
        scrollStart: 0,
        height: 0
      }, {
        id: 'About',
        scrollStart: 0,
        height: 0
      }, {
        id: 'Projects',
        scrollStart: 0,
        height: 0
      }]
    }
  },
  mounted () {
    window.addEventListener('scroll', this.handleScroll)
    window.addEventListener('resize', this.resizeHandler)
    this.getSectionsRect()
  },
  destoryed () {
    window.removeEventListener('scroll', this.handleScroll)
    window.removeEventListener('resize', this.resizeHandler)
  },
  methods: {
    resizeHandler () {
      this.handleScroll()
      this.getSectionsRect()
    },
    handleScroll () {
      this.isFloating = window.scrollY > window.innerHeight
      this.sections.map(section => {
        if (window.scrollY >= section.scrollStart && window.scrollY <= section.scrollEnd) this.activeSection = section.id
      })
      this.scrollProgress()
    },
    scrollTo (to, duration = 500) {
      let element = document.documentElement
      let start = element.scrollTop
      let change = document.getElementById(to).offsetTop - start
      let currentTime = 0
      let increment = 20

      let animateScroll = function () {        
        currentTime += increment
        let val = easeInOutQuad(currentTime, start, change, duration)
        element.scrollTop = val
        if (currentTime < duration) setTimeout(animateScroll, increment)
      }

      animateScroll()

      function easeInOutQuad (t, b, c, d) {
        t /= d/2
        if (t < 1) return c/2*t*t + b
        t--
        return -c/2 * (t*(t-2) - 1) + b
      }
    },
    getSectionsRect() {
      this.sections.map(item => {
        let section = document.getElementById(item.id)
        item.scrollStart = section.offsetTop
        item.scrollEnd = section.clientHeight + section.offsetTop
      })
    },
    scrollProgress() {
      const currentState = document.body.scrollTop || document.documentElement.scrollTop
      const pageHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight
      this.progress = (currentState / pageHeight) * 100
    }
  }
}
</script>

<style lang="scss">
@import "header";
</style>
