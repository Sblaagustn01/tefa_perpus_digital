<template>
  <div>
    <h1 class="text-start my-4">{{ buku.judul }}</h1>
    <div class="row">
      <div class="col-md-3">
        <div class="card"> 
          <div class="card-body">
    <span v-if="buku.cover"><img :src="buku.cover" :alt="buku.judul"></span>
    <span v-else><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3f/Placeholder_view_vector.svg/681px-Placeholder_view_vector.svg.png" :alt="buku.judul"></span>
  </div>
  <div class="col-md-6">
    <ul class="list-group list-group-flush">
      <li class="list-group-item">penulis : {{ buku.penulis }}</li>
      <li class="list-group-item">tahun_terbit : {{ buku.tahun_terbit }}</li>
      <li class="list-group-item">penerbit : {{ buku.penerbit }}</li>
      <li class="list-group-item">rak : {{ buku.rak }}</li>
      <li class="list-group-item">deskripsi : {{ buku.deskripsi }}</li>
    </ul>
  </div>
        </div>
      </div>
    </div>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const route = useRoute()
const buku = ref([])

const getBukuById = async () => {
  const { data, error } = await supabase.from('buku').select(`*, kategori(*)`)
  .eq('id', route.params.id)
  if(data) buku.value = data[0]
}

onMounted(() => {
  getBukuById()
})
</script>
