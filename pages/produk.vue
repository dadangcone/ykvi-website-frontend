<template>
  <div>
    <b-container fluid class="px-0">
      <div class="hero inner">
        <b-row class="no-gutters">
          <b-col md="6">
            <div class="red-sect blue">
              <div class="wrap">
                <h3>Produk</h3>
                <p>Coming Soon</p>
              </div>
            </div>
          </b-col>
          <b-col md="6">
            <div class="image" style="background-image: url('/produk-hero.png')"></div>
          </b-col>
        </b-row>
        <b-link to="" class="scroll" v-scroll-to="'.produk'"><img src="/chevron-down.png" alt=""></b-link>
      </div>
    </b-container>

    <div class="produk white-wrap">
      <b-container>
        <b-row>
          <b-col md="12">
            <h3 class="section-title">Produk Populer</h3>
          </b-col>
          <b-col sm="6" md="3" lg="2" v-for="item in dataProduct" :key="item.id">
            <div class="item-product">
              <div class="image">
                <img :src="item.product_details[0].url_product_image" alt="">
              </div>
              <h6>{{ item.name }}</h6>
              <p class="desc">{{ item.description }}</p>
            </div>
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
    let filteredBanner = _.filter(getBanner.data, ['page_name', 'CME'])
    let getProduct = await app.$axios.$get(`/product`)

    return { 
      dataBanner: filteredBanner[0],
      dataProduct: getProduct.data,
    }
  },
  data(){
    return{
      dataBanner: [],
    }
  }
}
</script>