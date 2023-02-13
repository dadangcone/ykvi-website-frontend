<template>
  <header>
    <b-navbar type="dark" toggleable="md">
      <b-navbar-brand to="/"><img src="/logo.png" alt=""/></b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="mr-auto">
          <!-- <b-nav-item to="/">Home</b-nav-item> -->
          <b-nav-item href="http://elearn.ykvi.or.id/" target="_blank">Ruang Kardiovaskular</b-nav-item>
          <b-nav-item to="/cme">Webinar</b-nav-item>
          <b-nav-item to="/produk">Produk</b-nav-item>
          <b-nav-item to="https://www.pld-ui.com/symcard">Symcard</b-nav-item>
          <b-nav-item href="https://wecoc.id/" target="_blank">WECOC</b-nav-item>
          <b-nav-item to="/tentang-kami">Tentang Kami</b-nav-item>
          <b-nav-item to="/Kontak">Kontak</b-nav-item>
        </b-navbar-nav>
        <b-navbar-nav class="right-nav d-none" right>
          <b-nav-item to="">Masuk</b-nav-item>
          <b-nav-item to="">Daftar</b-nav-item>
          <b-nav-item to="">
            <img src="/search.png" alt="" class="search" />
          </b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </header>
</template>
