<template>
  <header>
    <b-navbar type="dark" toggleable="md">
      <b-navbar-brand to="/"><img src="/logo.png" alt=""></b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item to="/kelas-online">Kelas Online</b-nav-item>
          <b-nav-item to="/cme">CME</b-nav-item>
          <b-nav-item to="/produk">Produk</b-nav-item>
          <b-nav-item to="/symcard">Symcard</b-nav-item>
          <b-nav-item to="/tentang-kami">Tentang Kami</b-nav-item>
          <b-nav-item to="/Kontak">Kontak</b-nav-item>
          <a to="" class="btn btn-outline-primary">Masuk</a>
          <a to="" class="btn btn-primary">Daftar</a>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </header>
</template>
