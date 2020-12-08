<template>
  <div>
    <b-container fluid class="px-0">
      <div class="hero inner">
        <b-row class="no-gutters">
          <b-col md="6">
            <div class="red-sect blue">
              <div class="wrap">
                <h3>Produk {{ dataProduct.name }}</h3>
                <!-- <p>Coming Soon</p> -->
              </div>
            </div>
          </b-col>
          <b-col md="6">
            <div v-if="dataBanner" class="image" :style="{ backgroundImage: `url('${dataBanner.url_banner_image}')`}"></div>
            <div v-else class="image"></div>
          </b-col>
        </b-row>
        <b-link to="" class="scroll" v-scroll-to="'.produk'"><img src="/chevron-down.png" alt=""></b-link>
      </div>
    </b-container>

    <div class="produk white-wrap">
      <b-container>
        <b-row>
          <b-col md="8" offset-md="2">
            <b-carousel
              v-model="slide"
              :interval="4000"
              controls
              indicators
              background="#ababab"
              @sliding-start="onSlideStart"
              @sliding-end="onSlideEnd"
              class="mb-4"
            >
              <!-- Slides with image only -->
              <b-carousel-slide v-for="item in dataProduct.product_details" :key="item.id" :img-src="item.url_product_image"></b-carousel-slide>

            </b-carousel>

            <p class="text-center">{{ dataProduct.description }}</p>
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
      title: 'Produk | Yayasan Kardiovaskular Indonesia',
      meta: [
        { hid: 'title', name: 'title', content: 'Produk | Yayasan Kardiovaskular Indonesia' },
        { hid: 'og:title', name: 'og:title', content: 'Produk | Yayasan Kardiovaskular Indonesia' },
        { hid: 'keywords', name: 'keywords', content: 'Yayasan, Universitas Indonesia, Kardiologi, Indonesia, Yayasan Kardiologi Indonesia' },
        { hid: 'description', name: 'description', content: 'Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI.' },
        { hid: 'og:description', name: 'og:description', content: 'Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI.' },
      ]
    }
  },
  async asyncData({ app, route }) {
    let getBanner = await app.$axios.$get(`/banner`)
    let filteredBanner = _.filter(getBanner.data, ['page_name', 'Product'])
    let tempBanner = null
    if(filteredBanner.length > 0){
      tempBanner = filteredBanner[0]
    } else {
      tempBanner = []
    }
    let getProduct = await app.$axios.$get(`/product/` + route.params.slug)

    return { 
      dataBanner: tempBanner,
      dataProduct: getProduct.data,
    }
  },
  data(){
    return{
      dataBanner: [],
      slide: 0,
    }
  },
  methods: {
    onSlideStart(slide) {
      this.sliding = true
    },
    onSlideEnd(slide) {
      this.sliding = false
    }
  }
}
</script>