<template>
  <div>
    <b-container fluid class="px-0">
      <b-row class="no-gutters">
        <b-col md="12">
          <div class="wrap-carousel">
            <VueSlickCarousel class="carousel-hero" v-bind="settings">
              <div
                class="item"
                v-for="item in dataBanner"
                :key="item.id"
                :style="{ backgroundImage: `url('${item.url_banner_image}')` }"
              ></div>
            </VueSlickCarousel>
            <div class="text-hero">
              <div class="wrap">
                <h2>Yayasan Kardiovaskular Indonesia</h2>
                <h6>
                  Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah
                  organisasi nonpemerintah yang dibentuk oleh Departemen
                  Kardiologi dan Kedokteran Vaskular FKUI. Saat ini YKVI
                  diketuai oleh Dr. dr. Ismoyo Sunu, SpJP(K)
                </h6>
              </div>
            </div>
          </div>
        </b-col>
      </b-row>

      <!-- <div class="hero">
        <b-row class="no-gutters">
          <b-col md="6">
            <div class="red-sect">
              <div class="wrap">
                <h3>Yayasan Kardiovaskular Indonesia</h3>
                <p>
                  Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah
                  organisasi nonpemerintah yang dibentuk oleh Departemen
                  Kardiologi dan Kedokteran Vaskular FKUI. Saat ini YKVI
                  diketuai oleh Dr. dr. Ismoyo Sunu, SpJP(K)
                </p>
                <b-link class="btn btn-primary" to="/tentang-kami"
                  >Selengkapnya <img src="/arrow-right.png" alt=""
                /></b-link>
              </div>
            </div>
          </b-col>
          <b-col md="6">
            <div
              v-if="dataBanner"
              class="image"
              :style="{
                backgroundImage: `url('${dataBanner.url_banner_image}')`
              }"
            ></div>
            <div v-else class="image"></div>
          </b-col>
        </b-row>
        <b-link to="" class="scroll" v-scroll-to="'.daftar'"
          ><img src="/chevron-down.png" alt=""
        /></b-link>
      </div> -->
    </b-container>

    <div class="daftar">
      <b-container fluid>
        <b-row class="align-items-center">
          <b-col lg="8">
            <h5>Bersama belajar online</h5>
            <h2>Daftar segera di Ruang Kardiovaskular Indonesia</h2>
            <p>
              Ruang Kardiovaskular Indonesia adalah tempat belajar ilmu dan
              keterampilan kardiovaskular online pertama di Indonesia. Anda
              dapat mengakses materi dimanapun Anda berada tanpa dibatasi oleh
              ruang dan waktu.
            </p>
          </b-col>
          <b-col lg="4">
            <div class="webinar-small" v-if="dataWebinar">
              <h6>{{ dataWebinar.type }}</h6>
              <h3>{{ dataWebinar.title }}</h3>
              <b-link
                :href="
                  'https://www.youtube.com/embed/' +
                    dataWebinar.link_embed_youtube.slice(-11)
                "
              >
                <img src="/youtube.png" alt="" />
                play on youtube
              </b-link>
            </div>
          </b-col>
        </b-row>
      </b-container>
    </div>

    <div class="kelas">
      <b-container fluid>
        <div class="kelas-head">
          <b-row>
            <b-col md="6">
              <h3>E-Learning CME</h3>
            </b-col>
            <b-col md="6">
              <b-link to="/cme">
                Lihat Lainnya
                <img src="/arrow-right-blue.png" alt="" />
              </b-link>
            </b-col>
          </b-row>
        </div>
        <b-row v-if="dataCME">
          <b-col lg="3" md="6" v-for="kelas in dataCME" :key="kelas.id">
            <div class="kelas-item">
              <iframe
                class="small"
                :src="
                  'https://www.youtube.com/embed/' +
                    kelas.link_embed_youtube.slice(-11)
                "
                frameborder="0"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen
              ></iframe>
              <h4>{{ kelas.title }}</h4>
              <h6>{{ kelas.type }}</h6>
            </div>
          </b-col>
        </b-row>
      </b-container>
    </div>

    <!-- <div class="webinar">
      <b-container>
        <b-row class="align-items-center">
          <b-col md="6">
            <iframe
              class="big"
              :src="
                'https://www.youtube.com/embed/' +
                  dataWebinar.link_embed_youtube.slice(-11)
              "
              frameborder="0"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen
            ></iframe>
          </b-col>
          <b-col md="6">
            <h6>{{ dataWebinar.type }}</h6>
            <h3>{{ dataWebinar.title }}</h3>
          </b-col>
        </b-row>
      </b-container>
    </div> -->
  </div>
</template>

<script>
import _ from "lodash";

export default {
  head() {
    return {
      title: "Home Page | Yayasan Kardiovaskular Indonesia",
      meta: [
        {
          hid: "title",
          name: "title",
          content: "Home Page | Yayasan Kardiovaskular Indonesia"
        },
        {
          hid: "og:title",
          name: "og:title",
          content: "Home Page | Yayasan Kardiovaskular Indonesia"
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
    console.log(getBanner);
    // let filteredBanner = _.filter(getBanner.data, ["page_name", "Home"]);
    let filteredBanner = getBanner.data;
    let tempBanner = null;
    if (filteredBanner.length > 0) {
      tempBanner = filteredBanner;
    } else {
      tempBanner = [];
    }
    let getCME = await app.$axios.$get(`/cme`);
    let tempCME = _.filter(getCME.data, ["is_home", 1]).slice(0, 4);
    let tempWebinar = _.filter(getCME.data, ["type", "Webinar"]).slice(0, 1);

    return {
      dataBanner: tempBanner,
      dataCME: tempCME,
      dataWebinar: tempWebinar[0]
    };
  },
  data() {
    return {
      settings: {
        dots: true,
        arrows: true,
        slidesToShow: 1,
        slidesToScroll: 1
      },
      kelas: [
        {
          id: 1,
          img: "/kelas.png",
          judul: "Kelas cara menggunakan stetoskop",
          mentor: "John Doe"
        },
        {
          id: 2,
          img: "/kelas2.png",
          judul: "Kelas cara bagaimana menjaga kondisi hati saat pandemi",
          mentor: "John Doe"
        },
        {
          id: 3,
          img: "/kelas3.png",
          judul: "Kelas berbagai macam alat alat kedokteran",
          mentor: "John Doe"
        },
        {
          id: 4,
          img: "/kelas4.png",
          judul: "Kelas berbagai profesi spesialis dalam kedokteran",
          mentor: "John Doe"
        }
      ]
    };
  }
};
</script>
