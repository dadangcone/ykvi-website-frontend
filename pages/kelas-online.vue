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
                <h3>Kelas Online</h3>
                <p>Ruang Kardiovaskular Indonesia adalah tempat belajar ilmu dan keterampilan kardiovaskular online pertama di Indonesia. Anda dapat mengakses materi dimanapun Anda berada tanpa dibatasi oleh ruang dan waktu. </p>
              </div>
            </div>
          </b-col>
          <b-col md="6">
            <div v-if="dataBanner" class="image" :style="{ backgroundImage: `url('${dataBanner.url_banner_image}')`}"></div>
            <div v-else class="image"></div>
          </b-col>
        </b-row>
        <b-link to="" class="scroll" v-scroll-to="'.nav-page'"><img src="/chevron-down.png" alt=""></b-link>
      </div> -->
    </b-container>

    <!-- <div class="nav-page">
      <b-container>
        <b-row>
          <b-col>
            <b-link to="" v-scroll-to="'.ruang'">
              Tentang Kelas Online
            </b-link>
            <b-link to="" v-scroll-to="'.faq'">
              FAQ
            </b-link>
          </b-col>
        </b-row>
      </b-container>
    </div> -->

    <div class="gray-container">
      <b-container>
        <b-row>
          <b-col md="12">
            <div class="rounded-wrap">
              <b-row>
                <b-col md="12">
                  <b-breadcrumb :items="items"></b-breadcrumb>
                  <div class="ruang">
                    <h3 class="section-title">
                      {{ dataElearning.title }}
                    </h3>
                    <p class="section-subtitle">
                      {{ dataElearning.description }}
                    </p>
                    <b-link
                      :href="dataElearning.link_url_redirect"
                      target="_blank"
                      class="link-ruang"
                    >
                      Kunjungi Ruang Kardiovaskular Indonesia
                    </b-link>
                  </div>

                  <div class="faq">
                    <h3 class="section-title">FAQ</h3>
                    <div class="accordion faq" role="tablist">
                      <b-card
                        no-body
                        class="mb-1"
                        v-for="item in dataFAQ"
                        :key="item.id"
                      >
                        <b-card-header role="tab">
                          <b-button block v-b-toggle="'accordion-' + item.id"
                            >{{ item.question }}
                            <img src="/plus.png" alt="" class="plus float-right"
                          /></b-button>
                        </b-card-header>
                        <b-collapse
                          :id="'accordion-' + item.id"
                          accordion="faq-accordion"
                          role="tabpanel"
                        >
                          <b-card-body>
                            <b-card-text>{{ item.answer }}</b-card-text>
                          </b-card-body>
                        </b-collapse>
                      </b-card>
                    </div>
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
      title: "Kelas Online | Yayasan Kardiovaskular Indonesia",
      meta: [
        {
          hid: "title",
          name: "title",
          content: "Kelas Online | Yayasan Kardiovaskular Indonesia"
        },
        {
          hid: "og:title",
          name: "og:title",
          content: "Kelas Online | Yayasan Kardiovaskular Indonesia"
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
    let filteredBanner = _.filter(getBanner.data, ["page_name", "E-Learning"]);
    let tempBanner = null;
    if (filteredBanner.length > 0) {
      tempBanner = filteredBanner[0];
    } else {
      tempBanner = [];
    }

    let getFAQ = await app.$axios.$get(`/e-learning/faq`);
    let getElearning = await app.$axios.$get(`/e-learning`);

    return {
      dataBanner: tempBanner,
      dataFAQ: getFAQ.data,
      dataElearning: getElearning.data
    };
  },
  data() {
    return {
      items: [
        {
          text: "Beranda",
          href: "/"
        },
        {
          text: "Kelas Online",
          active: true
        }
      ]
    };
  }
};
</script>
