<template>
  <div class="container-fluid">
    <div class="row my-5 d-flex justify-content-evenly">
      <div class="col-lg-6 box">
        <nuxt-link to="/pengunjung/tambah">
          <div class="card bg-pengunjung rounded-5">
            <div class="card-body">
              <h2>Pengunjung</h2>
            </div>
          </div>
        </nuxt-link>
      </div>

      <div class="col-lg-6 box">
        <nuxt-link to="/buku">
          <div class="card bg-buku rounded-5 ">
            <div class="card-body">
              <h2>Buku</h2>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>
    <div class="statistik">
      <h1>STATISTIK</h1>
    </div>

    <div class="container-fluid">
      <div class="row my-5 d-flex justify-content-evenly ">
        <div class="col-lg-6 box">
        <NuxtLink to="/pengunjung">
          <div class="card rounded-5">
            <div class="card-body">
              <h2><span class="no">{{ jml_pengunjung }}</span> pengunjung</h2>
              </div>
            </div>
          </NuxtLink>
        </div>
        <div class="col-lg-6 box">
          <div class="card c2 rounded-5">
            <div class="card-body">
              <h2><span class="no">{{ jml_buku }}</span> Buku</h2>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="container-fluid">
      <div class="row my-5">
        <div class="col-lg-12">
          <Statistik />
        </div>
      </div>
    </div>
</template>
<script setup>
const supabase = useSupabaseClient()
const jml_pengunjung = ref(0)
const jml_buku = ref(0)

async function getjml_pengunjung() {
  const{ error , data, count } = await supabase
  .from("pengunjung")
  .select('*', { count: 'exact' })
  if (count) jml_pengunjung.value = count
  
}
async function getjml_buku() {
  const{ error , data, count } = await supabase
  .from("buku")
  .select('*', { count: 'exact' })
  if (count) jml_buku.value = count
  
}


onMounted(() => {
  getjml_pengunjung()
  getjml_buku()
})
</script>
<style scoped>
h2{
  color: white;
}
.card {
  height: 250px;
  box-shadow: 1px 1px 10px #424242;
  background-color: gray;
}
.card.bg-pengunjung {
  background-image: url('../assets/pengunjung.jpeg');
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}
.card.bg-buku {
  background: url('../assets/buku.jpg') no-repeat center center;
  background-size: cover;
}
.c2{
  background-color: rgb(154, 187, 154);
}
.statistik {
  color: grey;
  margin-left: 50px;
}
.box{
  width: 45%;
}
.box a{
  text-decoration: none;
}
</style>
