<template>
        <div class="card col-3">
          <div :class="data.name">
              <h3 class="text-light p-4">{{data.name}}</h3>
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
.BackLog{
  background-color: #0097e6;

}
.ToDo{
  background-color: #8c7ae6;

}
.OnGoing{
  background-color:#e1b12c;

}
.Finished{
  background-color:#44bd32;

}
</style>
