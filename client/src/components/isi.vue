<template>

<div class="card text-white bg-primary mb-3" style="max-width: 18rem;">
  <div class="card-header">{{item.title}}</div>
  <div class="card-body">
    <p class="card-text">{{item.descrip}}</p>
    <div>
      <button class="btn btn-danger"  @click="removeItem">delete</button>
    </div>
    <div>
       <button class="btn btn-success"  @click="actionOne">{{buttonOne}}</button>
    </div>
    <div>
      <button class="btn btn-info" @click="actionTwo" v-if="buttonTwo">{{buttonTwo}}</button>
    </div>
  </div>
</div>
</template>

<script>
import database from '@/api/config.js'

export default {
  name: 'content',
  data: function () {
    return {
      buttonOne: '',
      buttonTwo: ''
    }
  },
  props: ['item', 'name'],
  methods: {
    actionOne () {
      database.ref(`/${this.item.id}`).remove()
      database.ref('/').push({
        title: this.item.title,
        status: this.buttonOne
      })
    },
    actionTwo () {
      database.ref(`/${this.item.id}`).remove()
      database.ref('/').push({
        title: this.item.title,
        status: this.buttonTwo
      })
    },
    removeItem () {
      database.ref(`/${this.item.id}`).remove()
    }
  },
  created () {
    if (this.name === 'BackLog') {
      this.buttonOne = 'ToDo'
      this.buttonTwo = null
    } else if (this.name === 'ToDo') {
      this.buttonOne = 'BackLog'
      this.buttonTwo = 'OnGoing'
    } else if (this.name === 'OnGoing') {
      this.buttonOne = 'Finished'
      this.buttonTwo = 'ToDo'
    } else if (this.name === 'Finished') {
      this.buttonOne = 'OnGoing'
      this.buttonTwo = null
    }
  }
}
</script>

<style scoped>
.card-header {
  color: #dadadada;
  height: 34px;
};
  
</style>
