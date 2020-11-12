<template>
  <div>
    <b-container fluid class="px-0">
      <div class="hero inner">
        <b-row class="no-gutters">
          <b-col md="6">
            <div class="red-sect blue">
              <div class="wrap">
                <h3>{{ dataBanner.page_name }}</h3>
                <p>Coming Soon</p>
              </div>
            </div>
          </b-col>
          <b-col md="6">
            <div class="image" style="background-image: url('/cme-hero.png')"></div>
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
              Kursus Live
            </b-link>
            <b-link to="" v-scroll-to="'.belajar-online'">
              Belajar Online
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
          <b-col md="4" v-for="item in dataCME" :key="item.id">
            <div class="item-webinar">
              <vue-plyr>
                <div class="blue-button small" data-plyr-provider="youtube" :data-plyr-embed-id="item.link_embed_youtube.slice(-11)"></div>
              </vue-plyr>
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
            <vue-plyr>
              <div class="blue-button" data-plyr-provider="youtube" data-plyr-embed-id="xkEmO3I9RkM"></div>
            </vue-plyr>
          </b-col>
          <b-col md="6">
            <h3 class="section-title white">Kursus Live</h3>
            <p class="section-subtitle white">Coming Soon</p>
          </b-col>
        </b-row>
      </b-container>
    </div>

    <div class="belajar-online white-wrap">
      <b-container>
        <b-row class="align-items-center">
          <b-col md="6">
            <h3 class="section-title">Pembelajaran live</h3>
            <p class="section-subtitle">Coming Soon</p>
          </b-col>
          <b-col md="6">
            <vue-plyr>
              <div class="blue-button" data-plyr-provider="youtube" data-plyr-embed-id="xkEmO3I9RkM"></div>
            </vue-plyr>
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
    let getCME = await app.$axios.$get(`/cme`)

    return { 
      dataBanner: filteredBanner[0],
      dataCME: getCME.data,
    }
  },
  data(){
    return{
      dataBanner: [],
    }
  }
}
</script>