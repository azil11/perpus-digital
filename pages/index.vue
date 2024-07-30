<template>
  <Header>
    <div class="row p-3 d-flex justify-content-center align-items-center navbar">
      <div class="col-lg-2">
        <img src="@/assets/img/LOGO-SMK4.png" style="width: 100px;" alt="logo SMKN 4">
      </div>
      <div class="col-lg-7 text-center">
        <h1>Perpustakaan Digital</h1>
        <address>
          SMK NEGERI 4 Tasikmalaya
          Jl.Depok, Kel.Sukamenak, Kec.Purbaratu
        </address>
      </div>
      <div class="col-lg-2">
        <img src="@/assets/img/LOGO-SMK4.png" style="width: 100px;" alt="logo SMKN 4">
      </div>
    </div>
  </Header>
  <div class="main">
    <nuxt-link to="pengunjung/tambah" class="text-decoration-none">
      <div class="card bg-pengunjung rounded-5">
        <div class="card-body text-center">
          <h2>Isi Kunjungan</h2>
          <h3>Klik</h3>
        </div>
      </div>
    </nuxt-link>
  </div>
</template>

<script setup>

</script>

<style scoped>
.navbar{
  background-color: #57aeff;
}
.card{
  width: 20rem;
  height: 8rem;
  background-color: #00000079;
  padding: 8  px;
  color: rgb(255, 255, 255)
}

/* .card.bg-penunjung{
    background-image: url('../assets/img/bg-home-kunjungan.jpeg');
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
}
.card .bg-buku{
    background-image: url('~/assets/img/bg-home-cari-buku.jpg') no-repeat center center;
    background-size: cover;
} */
.main {
  width: 100%;
  min-height: 80vh;
  background-image: url("~/assets/img/bg-home.png");
  background-size: cover;
  padding: 15% 5%;
}
</style>
