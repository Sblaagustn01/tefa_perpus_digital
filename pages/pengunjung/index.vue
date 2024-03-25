<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
        <div class="my-3">
          <input type="search" class="form-control form-control-lg rounded-5" placeholder="Filter...">
        </div>
        <div class="my-3 text-muted">menampilkan 1 dari 1</div>
        <table class="table">
          <thead>
            <tr>
              <td>#</td>
              <td>NAMA</td>
              <td>KEANGGOTAAN</td>
              <td>WAKTU</td>
              <td>KEPERLUAN</td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitors,i) in visitors" :key="i">
              <td>{{ i+i }}.</td>
              <td>{{ visitors.nama }}.</td>
              <td>{{ visitors.keanggotaan.nama }}.</td>
              <td>{{ visitors.tanggal }}.</td>
              <td>{{ visitors.keperluan.nama }}.</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <NuxtLink to="/pengunjung/tambah">
      <button type="submit" class="btn btn-primary rounded-5 px-5">Kembali</button>
    </NuxtLink>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const visitors = ref ([])
const getPengunjung = async () => {
  const { data, error } = await supabase.from('pengunjung').select('*, keanggotaan(*), keperluan(*)')
  if(data) visitors.value = data
}

onMounted(() => {
  getPengunjung()
})
</script>

<style scoped>
.btn{
  background-color: black;
}
.form-control{
  background-color: black;
}
</style>