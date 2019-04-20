<template>
        <div class="card col-3">
          <div class="card-header">
              <h2>{{data.name}}</h2>
          </div>
          <div class="card-body">         
         <isi v-for="(item) in data.data" :key="item.id" :item="item" :name="data.name"></isi>
          </div>
        </div>
</template>

 
<script>
import isi from '@/components/isi.vue'
export default {
  name: 'kanbancard',
  components: {
    isi
  },
  data: function () {
    return {}
  },
  props: ['data'],
  created () {
    this.cardTitle = this.title
  }
}
</script>

<style scoped>
</style>
