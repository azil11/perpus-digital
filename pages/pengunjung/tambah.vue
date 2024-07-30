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
              <select v-model="form.keanggotaan" class="form-control from-control-lg rounded-5 border-dark">
                <option value="">KEANGGOTAAN...</option>
                <option v-for="(member, i) in members" :key="i" :value="member.id">{{ member.nama }}</option>
              </select>
            </div>
            <div  v-if="form.keanggotaan == 1" class="mb-4">
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
          <button class="btn btn-primary mt-3 border-dark">Kirim</button>
        </div>

      </form>
      <div class="card bg-pengunjung rounded-5">
        <div class="card-body text-center">
          <nuxt-link to="/" class="text-decoration-none">
            <h3>Back To Home</h3>
          </nuxt-link>
          </div>
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
  const { error } = await supabase.from('pengunjung').insert([form.value])
  if (error) throw error
  else navigateTo('/pengunjung')
}


const getKeanggotaan = async () => {
  const { data, error } = await supabase.from('keanggotaan').select('*')
  if (data) members.value = data
}


const getKeperluan = async () => {
  const { data, error } = await supabase.from('keperluan').select('*')
  if (data) objectives.value = data
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
  background-color: blanchedalmond;
  padding: 9  px;
  color: blue;
}

.content{
  background-color: cadetblue;
}
</style>