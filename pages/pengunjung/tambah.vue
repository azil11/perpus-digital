<template>
  <div class="content">
    <div class="container-fluid ">
      <header>
        <div class="row">
          <div class="col-lg-4">
            <img src="@/assets/img/LOGO-SMK4.png" alt="" class="float-end" style="width: 100px;">
          </div>
          <div class="col-lg-8 ">
            <h1>Perpustakaan Digital</h1>
            <address>
              SMKN 4 Tasikmalaya<br>
              Jl.Depok, Sukamenak, Purbaratu
            </address>
          </div>
        </div>
      </header>
      <form @submit.prevent="KirimData">
        <div class="row justify-content-center">
          <div class="col-lg-10">
            <div class="mb-3">
              <input v-model="form.nama" type="text" placeholder="NAMA..."
                class="form-control formcontrol-lg rounded-5 border-dark">
            </div>
            <div class="mb-3">
              <select v-model="form.keanggotaan" @change="resetKelas" class="form-control from-control-lg rounded-5 border-dark">
                <option value="">KEANGGOTAAN...</option>
                <option v-for="(member, i) in members" :key="i" :value="member.id">{{ member.Nama }}</option>
              </select>
            </div>
            <div class="mb-4">
              <div class="row">
                <div class="col-md-4">
                  <select v-model="form.tingkat"
                    class="form-control from-control-lg from-select rounded-5 mb-2 border-dark">
                    <option value="">TINGKAT</option>
                    <option value="X">X</option>
                    <option value="XI">XI</option>
                    <option value="XII">XII</option>
                  </select>
                </div>
                <div class="col-md-4">
                  <select v-model="form.jurusan"
                    class="form-control from-control-lg from-select rounded-5 mb-2 border-dark">
                    <option value="">JURUSAN</option>
                    <option value="PPLG">PPLG</option>
                    <option value="TBSM">TBSM</option>
                    <option value="TOI">TOI</option>
                    <option value="TKJT">TKJT</option>
                    <option value="DKV">DKV</option>
                  </select>
                </div>
                <div class="col-md-4">
                  <select v-model="form.kelas"
                    class="form-control from-control-lg from-select rounded-5 mb-2 border-dark">
                    <option value="">KELAS</option>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                  </select>
                </div>
              </div>
            </div>
            <div class="mb-3">
              <select v-model="form.keperluan" class="form-control form-control-lg from-select rounded-5 border-dark">
                <option value="">KEPERLUAN...</option>
                <option v-for="(item, i) in objectives" :key="i" :value="item.id">{{ item.nama }}</option>
              </select>
            </div>
          </div>
        </div>
        <div class="text-center border-dark">
          <button class="btn btn-primary mt-3 border-dark">
            <nuxt-link to="/buku" class="text-decoration-none">
          </nuxt-link>
            Confirm</button>
      </div>


      </form>
          <div class="btn btn-dark rounded-5">
            <nuxt-link to="/" class="text-decoration-none">
            back to Home
          </nuxt-link>
          </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const members = ref([])
const objectives = ref([])


const form = ref({
  nama: "",
  keanggotaan: "",
  tingkat: "",
  jurusan: "",
  kelas: "",
  keperluan: "",
})

const KirimData = async () => {
  const { error } = await supabase.from('Pengunjung').insert([form.value])
  if (error) throw error
  else navigateTo('/Pengunjung')
}


const getKeanggotaan = async () => {
  const { data, error } = await supabase.from('Keanggotaan').select('*')
  if (data) members.value = data
}


const getKeperluan = async () => {
  const { data, error } = await supabase.from('Keperluan').select('*')
  if (data) objectives.value = data
}
const resetKelas = e => {
  if(e.target.value === '2' || '3' || '4'){
  form.value.tingkat = ''
  form.value.jurusan = ''
  form.value.kelas = ''
  }
}

onMounted(() => {
  getKeanggotaan()
  getKeperluan()
});
</script>


<style scoped>
.card{
  width: 10rem;
  height: 6rem;
  background-color: rgb(0, 0, 0);
  padding: 9  px;
  color: rgb(255, 255, 255);
}

.content{
  background-color: rgb(34, 255, 0);
}
</style>