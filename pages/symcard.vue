<template>
  <div>
    <b-container fluid class="px-0">
      <div class="hero inner">
        <b-row class="no-gutters">
          <b-col md="6">
            <div class="red-sect blue">
              <div class="wrap">
                <h3>Symcard</h3>
                <p>Coming Soon</p>
              </div>
            </div>
          </b-col>
          <b-col md="6">
            <div class="image" style="background-image: url('/kelas-hero.png')"></div>
          </b-col>
        </b-row>
        <b-link to="" class="scroll" v-scroll-to="'.symcard'"><img src="/chevron-down.png" alt=""></b-link>
      </div>
    </b-container>

    <div class="symcard gray-wrap">
      <b-container>
        <b-row>
          <b-col md="8" offset-md="2" class="text-center">
            <h3 class="section-title text-center">Symcard</h3>
            <p class="section-subtitle text-center">{{ dataSymcard.title }}</p>
            <b-link :href="dataSymcard.description" target="_blank" class="link-symcard text-center">{{ dataSymcard.description }}</b-link>
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
      title: 'Symcard | Yayasan Kardiovaskular Indonesia',
      meta: [
        { hid: 'title', name: 'title', content: 'Symcard | Yayasan Kardiovaskular Indonesia' },
        { hid: 'og:title', name: 'og:title', content: 'Symcard | Yayasan Kardiovaskular Indonesia' },
        { hid: 'keywords', name: 'keywords', content: 'Yayasan, Universitas Indonesia, Kardiologi, Indonesia, Yayasan Kardiologi Indonesia' },
        { hid: 'description', name: 'description', content: 'Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI.' },
        { hid: 'og:description', name: 'og:description', content: 'Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI.' },
      ]
    }
  },
  async asyncData({ app, route }) {
    let getBanner = await app.$axios.$get(`/banner`)
    let filteredBanner = _.filter(getBanner.data, ['page_name', 'CME'])
    let getSymcard = await app.$axios.$get(`/sym-card`)

    return { 
      dataBanner: filteredBanner[0],
      dataSymcard: getSymcard.data
    }
  },
  data(){
    return{

    }
  }
}
</script>