<template>
  <div class="container-fluid ">

    <div class="row d-flex justify-center">
      <div class="col-lg-5 text-center p-3">
        <h2>PERPUS DIGITAL</h2>
        SMKN 4 Kota Tasikmalaya
        Jl.Depok,Sukamenak,Purbaratu
        <address>
        </address>
      </div>
      <div class="col-lg-2">
        <img src="@/assets/img/LOGO-SMK4.png" style="width: 100px;" alt="logo SMKN 4">
      </div>
      <div class="col-lg-5">
        <h2 class="row text-center my-3 ms-4">RIWAYAT KUNJUNGAN</h2>
      </div>
    </div>

    <div class="row my-3 d-flex justify-content-center">
      <nuxt-link to="/buku" class="row justify-content-center mt-18 ">
        <button type="button" class=" btn btn-primary rounded-4 form-control-lg rounded-5 border-dark col-3">🔍PENCARIAN
          BUKU</button>
      </nuxt-link>
      <input v-model="keyword" class="fani col-6 form-control form-control-lg rounded-5 border-dark  mt-2 "
        placeholder="🔍 Search Riwayat Kunjungan..." style="width: 30rem;" @input="getPengunjung" />
      <h4>Jumlah Pengunjung {{ visitors.length }}</h4>

    </div>
    <div class="table-responsive">
      <table class="table">
        <thead>
          <tr>
            <td>No</td>
            <td>Nama</td>
            <td>Kenggotaan</td>
            <td>Waktu</td>
            <td>Keperluan</td>
            <td>Kelas</td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(visitor, i) in visitors" :key="i">
            <td>{{ i + 1 }}.</td>
            <td>{{ visitor.nama }}</td>
            <td>{{ visitor.keanggotaan.nama }}</td>
            <td>{{ visitor.tanggal }}, {{ visitor.jam.split(".")[0] }}</td>
            <td>{{ visitor.keperluan.nama }}</td>
            <td>{{ visitor.tingkat }}-{{ visitor.jurusan }}-{{ visitor.kelas }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <nuxt-link to="/pengunjung/tambah">
      <button type="button" class="btn btn-primary btn-lg mt-4">BACK</button>
    </nuxt-link>
  </div>
</template>


<script setup>

const supabase = useSupabaseClient()
const keyword = ref('')
const visitors = ref([])

const getPengunjung = async () => {
  const { data, error } = await supabase.from('Pengunjung').select(`*, Keanggotaan(*), Keperluan(*)`)
    .ilike('nama', `%${keyword.value}%`)
    .order('id', { ascending: false })
  if (data) visitors.value = data
}

onMounted(() => {
  getPengunjung()
})
</script>


<style scoped>
address {
  padding-top: 10px;
}



.container-fluid {
  background-color: rgb(255, 0, 0);


}
</style>

