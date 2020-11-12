<template>
  <div>
    <b-container fluid class="px-0">
      <div class="hero">
        <b-row class="no-gutters">
          <b-col md="6">
            <div class="red-sect">
              <div class="wrap">
                <h3>Yayasan Kardiovaskular Indonesia</h3>
                <p>Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI. Saat ini YKVI diketuai oleh Dr. dr. Ismoyo Sunu, SpJP(K)</p>
                <b-link class="btn btn-primary" to="">Selengkapnya <img src="/arrow-right.png" alt=""></b-link>
              </div>
            </div>
          </b-col>
          <b-col md="6">
            <div class="image" style="background-image: url('/hero.png')"></div>
          </b-col>
        </b-row>
        <b-link to="" class="scroll" v-scroll-to="'.daftar'"><img src="/chevron-down.png" alt=""></b-link>
      </div>
    </b-container>

    <div class="daftar">
      <b-container>
        <b-row class="align-items-center">
          <b-col md="6">
            <h5>Bersama belajar online</h5>
            <h2>Daftar segera di Ruang Kardiovaskular Indonesia</h2>
          </b-col>
          <b-col md="6">
            <p>Ruang Kardiovaskular Indonesia adalah tempat belajar ilmu dan keterampilan kardiovaskular online pertama di Indonesia. Anda dapat mengakses materi dimanapun Anda berada tanpa dibatasi oleh ruang dan waktu. </p>
          </b-col>
        </b-row>
      </b-container>
    </div>

    <div class="kelas">
      <b-container>
        <div class="kelas-head">
          <b-row>
            <b-col md="6">
              <h6>E-Learning</h6>
              <h3>Kelas Populer</h3>
            </b-col>
            <b-col md="6">
              <b-link to="">
                Lihat Lainnya
                <img src="/arrow-right-blue.png" alt="">
              </b-link>
            </b-col>
          </b-row>
        </div>
        <b-row>
          <b-col lg="3" md="6" v-for="kelas in kelas" :key="kelas.id">
            <b-link to="" class="kelas-item">
              <div class="image" :style="{ backgroundImage: 'url(' + kelas.img + ')' }"></div>
              <h4>{{ kelas.judul }}</h4>
              <h6>{{ kelas.mentor }}</h6>
            </b-link>
          </b-col>
        </b-row>
      </b-container>
    </div>

    <div class="webinar">
      <b-container>
        <b-row class="align-items-center">
          <b-col md="6">
            <vue-plyr>
              <div class="blue-button" data-plyr-provider="youtube" data-plyr-embed-id="xkEmO3I9RkM"></div>
            </vue-plyr>
          </b-col>
          <b-col md="6">
            <h6>Webinar</h6>
            <h3>Saksikan webinar dari para ahli setiap minggunya</h3>
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
      title: 'Home Page | Yayasan Kardiovaskular Indonesia',
      meta: [
        { hid: 'title', name: 'title', content: 'Home Page | Yayasan Kardiovaskular Indonesia' },
        { hid: 'og:title', name: 'og:title', content: 'Home Page | Yayasan Kardiovaskular Indonesia' },
        { hid: 'keywords', name: 'keywords', content: 'Yayasan, Universitas Indonesia, Kardiologi, Indonesia, Yayasan Kardiologi Indonesia' },
        { hid: 'description', name: 'description', content: 'Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI.' },
        { hid: 'og:description', name: 'og:description', content: 'Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI.' },
      ]
    }
  },
  data(){
    return{
      kelas: [
        {
          id: 1,
          img: '/kelas.png',
          judul: 'Kelas cara menggunakan stetoskop',
          mentor: 'John Doe'
        },
        {
          id: 2,
          img: '/kelas2.png',
          judul: 'Kelas cara bagaimana menjaga kondisi hati saat pandemi',
          mentor: 'John Doe'
        },
        {
          id: 3,
          img: '/kelas3.png',
          judul: 'Kelas berbagai macam alat alat kedokteran',
          mentor: 'John Doe'
        },
        {
          id: 4,
          img: '/kelas4.png',
          judul: 'Kelas berbagai profesi spesialis dalam kedokteran',
          mentor: 'John Doe'
        },
      ]   

    }
  }
}
</script>