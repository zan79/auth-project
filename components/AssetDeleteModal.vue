<template>
   <div>    
    <b-modal id="assetDeleteModal" title="Delete Asset" ok-title="Delete Asset" @ok="onDelete"
    ok-variant="danger" cancel-variant="secondary"
    header-bg-variant="dark"  header-text-variant="warning" header-border-variant="dark" header-close-variant="light"
    body-bg-variant="dark"    body-text-variant="light"
    footer-bg-variant="dark"  footer-border-variant="dark"
    >
      Do you really want to delete this asset? <br>
      {{asset.name}} - {{asset.description}}
    </b-modal>  
  </div>
</template>

<script>
export default {
  props: {
    asset: {}
  },
  methods: {
    async onDelete(){
      this.$axios.delete('api/assets/' + this.asset.id)
      .then((res)=>{
        if(res.status==202){
          alert("Asset Succesfully Deleted")
          this.$emit('onDeleted')
        }
      })
    }
  }
}
</script>

<style>

</style>
