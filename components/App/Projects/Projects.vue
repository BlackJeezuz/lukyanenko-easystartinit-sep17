<template>
  <section class="section section--dark" id="Projects">
    <div class="container">
      <h2 class="section-title" data-aos="fade-down" data-aos-anchor-placement="top-center">Projects</h2>
      <div class="projects">
        <div class="filters-wrap">
          <div v-if="activeFilter" :style="{width: `${activeFilter.size}px`, left: `${activeFilter.distance}px`}" class="filters-bg"/>
          <ul class="filters">
            <li v-for="filter in filters" :key="filter.name" class="filters__item">
              <button
                :data-filter="filter.id"
                class="filters__btn btn-default"
                type="button"
                @click="activeFilter = filter"
              >
                {{ filter.name }}
              </button>
            </li>
          </ul>
        </div>
        <ul class="projects-list">
          <li
            v-for="(project, index) in projects"
            :key="project.name"
            :class="['projects-list__item', 'mix', project.filter]"
          >
            <div
              class="projects-list__img"
              :style="{ backgroundImage: `url(\'${project.image}\')` }"
              data-aos="fade-up"
              :data-aos-delay="index * 100"
              data-aos-once="true"
            />
            <main class="projects-list__content">
              <div class="projects-list__head">
                <h4 class="projects-list__title">{{ project.name }}</h4>
                <p class="projects-list__info">{{ project.subtitle }}</p>
              </div>
              <button type="button" class="projects-list__btn" @click="activeProject = project">Learn more</button>
            </main>
          </li>
        </ul>
      </div>
    </div>
    <Popup v-if="activeProject" :project="activeProject" @close="activeProject = null"/>
  </section>
</template>

<script>
import Popup from '~/components/Popup'

export default {
  name: 'Projects',
  components: {
    Popup
  },
  data () {
    return {
      filters: [{
        name: 'all',
        id: 'all',
        size: 0,
        distance: 0
      }, {
        name: 'js',
        id: '.js',
        size: 0,
        distance: 0
      }, {
        name: 'vue',
        id: '.vue',
        size: 0,
        distance: 0
      }, {
        name: 'react',
        id: '.react',
        size: 0,
        distance: 0
      }],
      activeFilter: null,
      activeProject: null
    }
  },
  computed: {
    projects () {
      return [{
        name: 'Astorun',
        subtitle: 'Vue.js',
        filter: 'vue',
        image: require('~/assets/images/Mogo.jpg'),
        slides: [{
          img: require('~/assets/images/Mogo.jpg'),
          title: 'Astorun',
          info: '<p>Astorun it is the shop</p>'
        }, {
          img: require('~/assets/images/Mogo.jpg'),
          title: 'Astorun',
          info: '<p>Astorun is the best</p>'
        }, {
          img: require('~/assets/images/Mogo.jpg'),
          title: 'Astorun',
          info: '<p>Astorun is adssad</p>'
        }]
      }, {
        name: 'Express Finance',
        subtitle: 'Pure JS',
        filter: 'js',
        image: require('~/assets/images/Mogo.jpg')
      }, {
        name: 'AnyCash',
        subtitle: 'Vue.js',
        filter: 'vue',
        image: require('~/assets/images/Mogo.jpg')
      }, {
        name: 'News portal',
        subtitle: 'React.js',
        filter: 'react',
        image: require('~/assets/images/Mogo.jpg')
      }]
    }
  },
  mounted () {
    const containerEl = document.querySelector('.projects-list')
    const mixer = mixitup(containerEl)
    this.calcFilter()
    window.addEventListener('resize', this.calcFilter)
    this.activeFilter = this.filters[0]
  },
  destroyed () {
    window.removeEventListener('resize', this.calcFilter)
  },
  methods: {
    calcFilter () {
      const filters = document.querySelectorAll('.filters__btn')
      Array.prototype.map.call(filters, (btn, index) => {
        const leftDist = btn.offsetLeft - btn.parentElement.parentElement.offsetLeft

        const width = btn.clientWidth

        this.filters[index].distance = leftDist
        this.filters[index].size = width
      })
    }
  }
}
</script>
<style lang="scss">
@import "projects";
</style>