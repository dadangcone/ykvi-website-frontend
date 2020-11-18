<template>
  <div>
    <b-container fluid class="px-0">
      <div class="hero inner">
        <b-row class="no-gutters">
          <b-col md="6">
            <div class="red-sect blue">
              <div class="wrap">
                <h3>Tentang Kami</h3>
                <p>Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI. Saat ini YKVI diketuai oleh Dr. dr. Ismoyo Sunu, SpJP(K)</p>
              </div>
            </div>
          </b-col>
          <b-col md="6">
            <div class="image" style="background-image: url('/kelas-hero.png')"></div>
          </b-col>
        </b-row>
        <b-link to="" class="scroll" v-scroll-to="'.nav-page'"><img src="/chevron-down.png" alt=""></b-link>
      </div>
    </b-container>

    <div class="nav-page d-none">
      <b-container>
        <b-row>
          <b-col>
            <b-link to="" v-scroll-to="'.sejarah'">
              Sejarah
            </b-link>
            <b-link to="" v-scroll-to="'.struktur-organisasi'">
              Struktur Organisasi
            </b-link>
          </b-col>
        </b-row>
      </b-container>
    </div>

    <div class="sejarah gray-wrap">
      <b-container>
        <b-row>
          <b-col md="8" offset-md="2">
            <h3 class="section-title text-center mb-5">{{ dataAbout.title }}</h3>
            <img :src="dataAbout.url_about_us_image" alt="" class="img-about">
            <vue-markdown>{{ dataAbout.description }}</vue-markdown>
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
      title: 'Tentang Kami | Yayasan Kardiovaskular Indonesia',
      meta: [
        { hid: 'title', name: 'title', content: 'Tentang Kami | Yayasan Kardiovaskular Indonesia' },
        { hid: 'og:title', name: 'og:title', content: 'Tentang Kami | Yayasan Kardiovaskular Indonesia' },
        { hid: 'keywords', name: 'keywords', content: 'Yayasan, Universitas Indonesia, Kardiologi, Indonesia, Yayasan Kardiologi Indonesia' },
        { hid: 'description', name: 'description', content: 'Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI.' },
        { hid: 'og:description', name: 'og:description', content: 'Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI.' },
      ]
    }
  },
  async asyncData({ app, route }) {
    let getBanner = await app.$axios.$get(`/banner`)
    let filteredBanner = _.filter(getBanner.data, ['page_name', 'CME'])
    let getAbout = await app.$axios.$get('/about-us')

    return { 
      dataBanner: filteredBanner[0],
      dataAbout: getAbout.data
    }
  },
  data(){
    return{

    }
  }
}
</script>