<template>
  <div>
    <b-container fluid class="px-0">
      <div class="hero inner">
        <b-row class="no-gutters">
          <b-col md="6">
            <div class="red-sect blue">
              <div class="wrap">
                <h3>Kontak</h3>
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

    <div class="kontak white-wrap">
      <b-container>
        <b-row>
          <b-col md="6">
            <h3 class="section-title">Kontak Kami</h3>
            <p class="section-subtitle">Coming Soon</p>

            <div class="info-ykvi">
              <h6>Sekretariat YKVI</h6>
              <p>
                Jl. Letjen S. Parman Kav 87, Slipi, Jakarta Barat, 11420<br/>
                P | 021-568 4085 Ext. 1427<br/>
                E | sekretariat@ykvi.or.id
              </p>
              <b-link class="socmed" href="" target="_blank"><i class="fab fa-facebook-square"></i></b-link>
              <b-link class="socmed" href="" target="_blank"><i class="fab fa-twitter-square"></i></b-link>
              <b-link class="socmed" href="" target="_blank"><i class="fab fa-instagram"></i></b-link>
              <b-link class="socmed" href="https://www.youtube.com/channel/UCekqBXYi2bhILgDQIakMYEw" target="_blank"><i class="fab fa-youtube"></i></b-link>
            </div>
          </b-col>
          <b-col md="6">
            <ValidationObserver v-slot="{ handleSubmit }" ref="observer">
              <form @submit.prevent="handleSubmit(submitKontak)">
                <b-row>
                  <b-col md="6">
                    <ValidationProvider name="Nama" rules="required" v-slot="{ errors }" class="form-wrap">
                      <label for="">Nama</label>
                      <b-form-input v-model="kontak.nama" :class="[{'is-invalid': errors[0] }, errors[0] ? 'mb-1' : 'mb-3' ]"></b-form-input>
                      <span class="validator text-danger">{{ errors[0] }}</span>
                    </ValidationProvider>
                  </b-col>
                  <b-col md="6">
                    <ValidationProvider name="Email" rules="required|email" v-slot="{ errors }" class="form-wrap">
                      <label for="">Email</label>
                      <b-form-input v-model="kontak.email" type="email" :class="[{'is-invalid': errors[0] }, errors[0] ? 'mb-1' : 'mb-3' ]"></b-form-input>
                      <span class="validator text-danger">{{ errors[0] }}</span>
                    </ValidationProvider>
                  </b-col>
                  <b-col md="6">
                    <ValidationProvider name="Nomor Telepon" rules="required" v-slot="{ errors }" class="form-wrap">
                      <label for="">Nomor Telepon</label>
                      <b-form-input v-model="kontak.phone" :class="[{'is-invalid': errors[0] }, errors[0] ? 'mb-1' : 'mb-3' ]"></b-form-input>
                      <span class="validator text-danger">{{ errors[0] }}</span>
                    </ValidationProvider>
                  </b-col>
                  <b-col md="6">
                    <ValidationProvider name="Judul" rules="required" v-slot="{ errors }" class="form-wrap">
                      <label for="">Judul</label>
                      <b-form-input v-model="kontak.judul" :class="[{'is-invalid': errors[0] }, errors[0] ? 'mb-1' : 'mb-3' ]"></b-form-input>
                      <span class="validator text-danger">{{ errors[0] }}</span>
                    </ValidationProvider>
                  </b-col>
                  <b-col md="12">
                    <ValidationProvider name="Pesan" rules="required" v-slot="{ errors }" class="form-wrap">
                      <label for="">Pesan</label>
                      <b-form-textarea v-model="kontak.pesan" :class="[{'is-invalid': errors[0] }, errors[0] ? 'mb-1' : 'mb-3' ]"></b-form-textarea>
                      <span class="validator text-danger">{{ errors[0] }}</span>
                    </ValidationProvider>
                  </b-col>
                </b-row>
                <div class="button-wrap">
                  <button id="submitKontak" type="submit" class="btn btn-primary mt-3" :disabled="loading">Kirim Pesan</button>
                  <div class="load" v-if="loading">
                    <b-spinner variant="primary" label="Spinning" class="mt-2"></b-spinner>
                  </div>
                </div>
              </form>
            </ValidationObserver>
          </b-col>
        </b-row>
      </b-container>
    </div>

    <GmapMap
      :center="{lat:-6.363259, lng:106.833672}"
      :zoom="15"
      map-type-id="terrain"
      class="map"
      :options="{
        zoomControl: true,
        mapTypeControl: false,
        scaleControl: true,
        streetViewControl: false,
        rotateControl: false,
        fullscreenControl: false,
        disableDefaultUi: false
      }"
    >
      <GmapMarker
        :position="{lat:-6.363259, lng:106.833672}"
        icon="/marker.png"
      />
    </GmapMap>

  </div>
</template>

<script>
import _ from "lodash";

export default {
  head() {
    return {
      title: 'Kontak | Yayasan Kardiovaskular Indonesia',
      meta: [
        { hid: 'title', name: 'title', content: 'Kontak | Yayasan Kardiovaskular Indonesia' },
        { hid: 'og:title', name: 'og:title', content: 'Kontak | Yayasan Kardiovaskular Indonesia' },
        { hid: 'keywords', name: 'keywords', content: 'Yayasan, Universitas Indonesia, Kardiologi, Indonesia, Yayasan Kardiologi Indonesia' },
        { hid: 'description', name: 'description', content: 'Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI.' },
        { hid: 'og:description', name: 'og:description', content: 'Yayasan Kardiovaskular Indonesia (YKVI) adalah sebuah organisasi nonpemerintah yang dibentuk oleh Departemen Kardiologi dan Kedokteran Vaskular FKUI.' },
      ]
    }
  },
  async asyncData({ app, route }) {
    let getBanner = await app.$axios.$get(`/banner`)
    let filteredBanner = _.filter(getBanner.data, ['page_name', 'Contact Us'])
    let tempBanner = null
    if(filteredBanner.length > 0){
      tempBanner = filteredBanner[0]
    } else {
      tempBanner = []
    }

    return { 
      dataBanner: tempBanner,
    }
  },
  data(){
    return{
      loading: false,
      kontak: {
        nama: '',
        email: '',
        phone: '',
        judul: '',
        pesan: '',
      }
    }
  },
	methods: {
    async submitKontak(){
      this.loading = true
      this.reset = false
      try{
        let formKontak = new FormData()
        formKontak.append('name', this.kontak.nama)
        formKontak.append('email', this.kontak.email)
        formKontak.append('phone_number', this.kontak.phone)
        formKontak.append('subject', this.kontak.judul)
        formKontak.append('message', this.kontak.pesan)

        await this.$axios.$post(`/contact-us/store`, formKontak)
        this.$toast.success('Terimakasih telah menghubungi kami!').goAway(3000);

        // reset form
        this.kontak.nama = ''
        this.kontak.email = ''
        this.kontak.phone = ''
        this.kontak.judul = ''
        this.kontak.pesan = ''
        this.$nextTick(() => this.$refs.observer.reset());
      } catch(error){
        this.$toast.error(error).goAway(3000);
      }
      this.loading = false
    },
  }
}
</script>