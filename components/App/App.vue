<template>
  <div class="app">
    <div class="main-wrap">
      <Header />
      <SectionMain />
    </div>
    <Cases />
    <About />
    <Projects />
    <Footer />
  </div>
</template>

<script>
import Header from './Header'
import SectionMain from './SectionMain'
import Cases from './Cases'
import About from './About'
import Projects from './Projects'
import Footer from './Footer'
import AOS from 'aos'
import 'aos/dist/aos.css'

export default {
  name: 'App',
  components: {
    Header,
    SectionMain,
    Cases,
    About,
    Projects,
    Footer
  },
  mounted () {
    AOS.init()
  }
}
</script>

<style lang="scss">
@import "app";
</style>