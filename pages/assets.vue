<template>
  <div>
    <NavBar/>
    <AssetEditModal :asset="selectedAsset"/>
    <AssetDeleteModal :asset="selectedAsset" @onDeleted="getAll" />
    <div class="container mt-5">
      <div>
        <AssetEntryModal class="float-right mt-2" @onAdded="getAll"/>
        <h1 class="text-warning">Assets</h1>
      </div>
      <table class="table table-striped table-dark">
        <thead class="bg-warning text-dark">
          <th>Name</th>
          <th>Description</th>
          <th>Location</th>
          <th>Value</th>
          <th>Status</th>
          <th>&nbsp;</th>
          <th>&nbsp;</th>
        </thead>
        <tbody>
          <tr v-for="asset in assets" :key="asset.id">
            <td>{{asset.name}}</td>
            <td>{{asset.description}}</td>
            <td>{{asset.location}}</td>
            <td>{{asset.value}}</td>
            <td>{{asset.status}}</td>
            <td>
              <b-button @click="onEdit(asset)" variant="info" size="sm">Edit</b-button>
            </td>
            <td>
              <b-button @click="onDelete(asset)" variant="danger" size="sm">Delete</b-button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>

export default {
  data(){
    return {
      assets: [],
      selectedAsset: {}
    }
  },
  methods: {
    async getAll(){
      await this.$axios.get('/api/assets')
      .then((res)=>{
        if(res.status==200){
          this.assets = res.data
        }
      })
    },
    onEdit(selectedAsset){
      this.selectedAsset = selectedAsset
      this.$bvModal.show('assetEditModal')
    },
    onDelete(selectedAsset){
      this.selectedAsset = selectedAsset
      this.$bvModal.show('assetDeleteModal')
    }
  },
  created(){
    this.getAll()  
  }
}
</script>

<style>
body{
  background-color: #212121;
}
</style>