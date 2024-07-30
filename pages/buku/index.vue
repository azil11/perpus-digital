<template>
  <Header>
    <div class="row p-3 d-flex  navbar">
      <div class="col-lg-2 ps-5">
        <img src="@/assets/img/LOGO-SMK4.png" style="width: 100px;" alt="logo SMKN 4">
      </div>
      <div class="col-lg-4 header ">
        <h2>Perpus Digital</h2>
        <address>
          SMKN 4 Tasikmalaya
          Jl.Depok,Sukamenak,
          Purbaratu
        </address>
        
          <button type="button" class="btn btn-primary btn-sm rounded-5 " data-bs-toggle="modal" data-bs-target="#confirmBack">BACK TO HOME</button>
        <!-- Modal -->
        <div class="modal fade" id="confirmBack" tabindex="-1" aria-labelledby="confirmBackLabel" aria-hidden="true">
          <div class="modal-dialog">
            <div class="modal-content">
              <div class="modal-header">
                <h1 class="modal-title fs-5" id="confirmBackLabel">Kembali Ke Halaman Utama</h1>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
              </div>
              <div class="modal-body">
                Apakah Anda Ingin Kembali Ke Halaman Utama?..
              </div>
              <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">TIDAK</button>
                <button type="button" class="btn btn-primary" data-bs-dismiss="modal" @click="navigateTo('/')">YA</button>
              </div>
            </div>
          </div>
        </div>

      </div>
      <div class="col-lg-2">
        <nuxt-link to="/pengunjung/" class="row float-center me-7">
          <button type="button" class="btn btn-primary btn-sm rounded-5">Kembali<P>Melihat Riwayat kunjungan</P></button>
        </nuxt-link>
      </div>
    </div>
  </Header>
  <div class="container-fluid">
    <div class="row">
      <div class="row d-flex justify-content-center">
        <div class="col-lg-4">
            <h2 class="text-center text-white my-4">BUKU</h2>
            <div class="my-3">
              <input v-model="keyword" type="Search" class="form form-control rounded-5 text-white" @input="getBooks"
                placeholder="🔍 Mau baca apa hari ini? . . . . .">
            </div>
        </div>
        <div class="row">
          <div class="col-lg-2 " v-for="(buku, i) in books " :key="i">
            <div class="card mb-3 mt-4">
              <div class="card-body">
                <nuxt-link :to="`/buku/${buku.id}`">
                  <img :src="buku.cover" class="cover" :alt="buku.judul" />
                </nuxt-link>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script setup>

const supabase = useSupabaseClient()


const books = ref([])
const keyword = ref('')

const getBooks = async () => {
  const { data, error } = await supabase.from('buku').select(`*, kategori(*)`)
    .ilike('judul', `%${keyword.value}%`)
  if (data) books.value = data
}

onMounted(() => {
  getBooks()
})
</script>



<style scoped>
.card-body {
  width: 100%;
  height: 400px;
  padding: 0%;
}

.navbar {
  background-color: #DED2D2;
}

.cover {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 0 30;
}

.container-fluid {
  background-image: url("assets/img/ado.avif");
}

.btn {
  font-size: 17px;
}

.header {
  text-align: center;
}

.form {
  background-color: #0d6efd;
}

::placeholder {
  color: white;
}
</style>