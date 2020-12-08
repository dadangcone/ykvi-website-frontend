<template>
  <div>
    <b-container fluid class="px-0">
      <div class="hero inner">
        <b-row class="no-gutters">
          <b-col md="6">
            <div class="red-sect blue">
              <div class="wrap">
                <h3>CME</h3>
                <!-- <p>Coming Soon</p> -->
              </div>
            </div>
          </b-col>
          <b-col md="6">
            <div v-if="dataBanner" class="image" :style="{ backgroundImage: `url('${dataBanner.url_banner_image}')`}"></div>
            <div v-else class="image"></div>
          </b-col>
        </b-row>
        <b-link to="" class="scroll" v-scroll-to="'.nav-page'"><img src="/chevron-down.png" alt=""></b-link>
      </div>
    </b-container>

    <div class="nav-page">
      <b-container>
        <b-row>
          <b-col>
            <b-link to="" v-scroll-to="'.webinar-cme'">
              Webinar
            </b-link>
            <b-link to="" v-scroll-to="'.kursus-live'">
              Live Course
            </b-link>
            <b-link to="" v-scroll-to="'.belajar-online'">
              Live Teaching
            </b-link>
          </b-col>
        </b-row>
      </b-container>
    </div>

    <div class="webinar-cme gray-wrap">
      <b-container>
        <b-row>
          <b-col md="12">
            <h3 class="section-title">Webinar</h3>
            <p class="section-subtitle">Penjelasan sedikit mengenai webinar</p>
          </b-col>
          <b-col md="4" v-for="item in dataWebinar" :key="item.id">
            <div class="item-webinar">
              <iframe class="small" :src="'https://www.youtube.com/embed/' + item.link_embed_youtube.slice(-11)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
              <h6>{{ item.title }}</h6>
              <b-link :to="item.link_url_zoom">Link Zoom Webinar</b-link>
            </div>
          </b-col>
        </b-row>
      </b-container>
    </div>

    <div class="kursus-live white-wrap">
      <b-container>
        <b-row class="align-items-center">
          <b-col md="6">
            <iframe class="big" :src="'https://www.youtube.com/embed/' + dataCourse.link_embed_youtube.slice(-11)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
          </b-col>
          <b-col md="6">
            <h3 class="section-title white">{{ dataCourse.title }}</h3>
            <p class="section-subtitle white">{{ dataCourse.type }}</p>
          </b-col>
        </b-row>
      </b-container>
    </div>

    <div class="belajar-online white-wrap">
      <b-container>
        <b-row class="align-items-center">
          <b-col md="6">
            <h3 class="section-title">{{ dataTeaching.title }}</h3>
            <p class="section-subtitle">{{ dataTeaching.type }}</p>
          </b-col>
          <b-col md="6">
            <iframe class="big" :src="'https://www.youtube.com/embed/' + dataTeaching.link_embed_youtube.slice(-11)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
          </b-col>
        </b-row>
      </b-container>
    </div>

  </div>
</template>

<script>
import _ from "lodash";

export default {
  head() {
    return {
      title: 'CME | Yayasan Kardiovaskular Indonesia',
      meta: [
        { hid: 'title', name: 'title', content: 'CME | Yayasan Kardiovaskular Indonesia' },
        { hid: 'og:title', name: 'og:title', content: 'CME | Yayasan Kardiovaskular Indonesia' },
        { hid: 'keywords', name: 'keywords', content: 'Yayasan, Universitas Indonesia, Kardiologi, Indonesia, Yayasan Kardiologi Indonesia' },
        { hid: 'description', name: 'description', content: 'Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI.' },
        { hid: 'og:description', name: 'og:description', content: 'Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI.' },
      ]
    }
  },
  async asyncData({ app, route }) {
    let getBanner = await app.$axios.$get(`/banner`)
    let filteredBanner = _.filter(getBanner.data, ['page_name', 'CME'])
    let tempBanner = null
    if(filteredBanner.length > 0){
      tempBanner = filteredBanner[0]
    } else {
      tempBanner = []
    }
    let getCME = await app.$axios.$get(`/cme`)
    let tempWebinar = _.filter(getCME.data, ['type', 'Webinar'])
    let tempCourse = _.filter(getCME.data, ['type', 'Live course']).slice(0, 1)
    let tempTeaching = _.filter(getCME.data, ['type', 'Live teaching']).slice(0, 1)

    return { 
      dataBanner: tempBanner,
      dataWebinar: tempWebinar,
      dataCourse: tempCourse[0],
      dataTeaching: tempTeaching[0],
    }
  },
  data(){
    return{
      dataBanner: [],
    }
  }
}
</script>