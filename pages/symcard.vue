<template>
  <div>
    <b-container fluid class="px-0">
      <div
        class="hero-inner-new"
        :style="{
          backgroundImage: `url('${
            dataBanner ? dataBanner.url_banner_image : null
          }')`
        }"
      ></div>
      <!-- <div class="hero inner">
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
            <div v-if="dataBanner" class="image" :style="{ backgroundImage: `url('${dataBanner.url_banner_image}')`}"></div>
            <div v-else class="image"></div>
          </b-col>
        </b-row>
        <b-link to="" class="scroll" v-scroll-to="'.symcard'"><img src="/chevron-down.png" alt=""></b-link>
      </div> -->
    </b-container>

    <div class="gray-container">
      <b-container>
        <b-row>
          <b-col md="12">
            <div class="rounded-wrap">
              <b-row>
                <b-col md="12">
                  <b-breadcrumb :items="items"></b-breadcrumb>
                  <div class="symcard">
                    <b-row>
                      <b-col md="12" class="text-center">
                        <h3 class="section-title text-center">Symcard</h3>
                        <p class="section-subtitle text-center">
                          {{ dataSymcard.title }}
                        </p>
                        <img
                          v-if="dataSymcard.url_sym_card_image"
                          :src="dataSymcard.url_sym_card_image"
                          alt=""
                          class="img-fluid mb-4"
                        />
                        <vue-markdown>{{
                          dataSymcard.description
                        }}</vue-markdown>
                        <b-link
                          v-if="dataSymcard.link_embed_youtube"
                          :to="dataSymcard.link_embed_youtube"
                          class="link-symcard-embed"
                          >Klik disini untuk melihat video youtube
                          symcard</b-link
                        >
                      </b-col>
                    </b-row>
                  </div>
                </b-col>
              </b-row>
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
      title: "Symcard | Yayasan Kardiovaskular Indonesia",
      meta: [
        {
          hid: "title",
          name: "title",
          content: "Symcard | Yayasan Kardiovaskular Indonesia"
        },
        {
          hid: "og:title",
          name: "og:title",
          content: "Symcard | Yayasan Kardiovaskular Indonesia"
        },
        {
          hid: "keywords",
          name: "keywords",
          content:
            "Yayasan, Universitas Indonesia, Kardiologi, Indonesia, Yayasan Kardiologi Indonesia"
        },
        {
          hid: "description",
          name: "description",
          content:
            "Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI."
        },
        {
          hid: "og:description",
          name: "og:description",
          content:
            "Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI."
        }
      ]
    };
  },
  async asyncData({ app, route }) {
    let getBanner = await app.$axios.$get(`/banner`);
    let filteredBanner = _.filter(getBanner.data, ["page_name", "SymCard"]);
    let tempBanner = null;
    if (filteredBanner.length > 0) {
      tempBanner = filteredBanner[0];
    } else {
      tempBanner = [];
    }
    let getSymcard = await app.$axios.$get(`/sym-card`);

    return {
      dataBanner: tempBanner,
      dataSymcard: getSymcard.data
    };
  },
  data() {
    return {};
  }
};
</script>
