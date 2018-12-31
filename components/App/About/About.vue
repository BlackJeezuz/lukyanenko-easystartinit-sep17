<template>
  <section class="section" id="About">
    <div class="container">
      <h2 class="section-title" data-aos="fade-down" data-aos-anchor-placement="top-center">About me</h2>
      <main class="about">
        <div class="about__content" data-aos="fade-right" data-aos-anchor-placement="top-center">
          <figure class="about__person">
            <img class="about__img" src="~/static/me.jpg" alt="Ruslan Lukianenko">
            <figcaption class="about__caption">Who is this guy?</figcaption>
          </figure>
          <p>I'm the Front-End Developer for <a href="#" class="link">jCash.co</a> in Kyiv.<br>I have serious passion for creating web interfaces and their development. Details about my education or work experience you can find in my <a href="#" class="link">CV</a></p>
        </div>
        <div class="about__skills" data-aos="fade-left" data-aos-anchor-placement="top-center">
          <ul class="skills-list">
            <li
              v-for="skill in skills"
              :key="skill.name"
              class="skills-list__item"
            >
              <div class="skills-list__name">{{ skill.name }}</div>
              <div class="skills-list__percent">
                <div :style="`width: ${skill.percent}%`" class="skills-list__percent-line">{{ skill.percent }}%</div>
              </div>
            </li>
          </ul>
        </div>
      </main>
    </div>
  </section>
</template>

<script>
export default {
  name: 'About',
  computed: {
    skills () {
      return [{
        name: 'CSS',
        percent: '80'
      }, {
        name: 'HTML',
        percent: '90'
      }, {
        name: 'JavaScript',
        percent: '80'
      }, {
        name: 'Vue',
        percent: '80'
      }, {
        name: 'React',
        percent: '30'
      }, {
        name: 'SASS/SCSS',
        percent: '90'
      }, {
        name: 'GIT',
        percent: '40'
      }, {
        name: 'Photoshop',
        percent: '40'
      }, {
        name: 'Webpack/Gulp',
        percent: '60'
      }, {
        name: 'SSR',
        percent: '30'
      }]
    }
  }
}
</script>

<style lang="scss">
@import "about";
</style>
