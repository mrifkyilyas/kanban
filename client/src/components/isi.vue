<template>

<div class="card text-white mb-3" :style="template">
  <div class="card-header"><h4>{{item.title}}</h4></div>
  <div class="card-body">
    <p class="card-text">{{item.descrip}}</p>
    <div class="d-flex flex-column align-self-end">
      <div>
       <button class="btn" :style="designOne"  @click="actionOne">{{buttonOne}}</button>
    </div>
    <div>
      <button class="btn" :style="designTwo" @click="actionTwo" v-if="buttonTwo">{{buttonTwo}}</button>
    </div>
     <div>
      <button class="btn btn-danger"  @click="removeItem">delete</button>
    </div>
    </div>
    
  </div>
</div>
</template>

<script>
import database from '@/api/config.js'

export default {
  name: 'isi',
  data: function () {
    return {
      buttonOne: '',
      buttonTwo: '',
      designOne:'',
      template:''
    }
  },
  props: ['item', 'name'],
  methods: {
    actionOne () {
      database.ref(`/${this.item.id}`).remove()
      database.ref('/').push({
        title: this.item.title,
        status: this.buttonOne,
        descrip: this.item.descrip
      })
    },
    actionTwo () {
      database.ref(`/${this.item.id}`).remove()
      database.ref('/').push({
        title: this.item.title,
        status: this.buttonTwo,
        descrip: this.item.descrip
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
      this.designOne = `background:#8c7ae6; color:white;`
      this.template = `max-width: 18rem;background:#0097e6; `

    } else if (this.name === 'ToDo') {
      this.buttonOne = 'BackLog'
      this.buttonTwo = 'OnGoing'
      this.designOne = `background:#0097e6; color:white;`
      this.designTwo =`background:#e1b12c; color:white;`
       this.template = `max-width: 18rem; background:#8c7ae6; `
      
    } else if (this.name === 'OnGoing') {
      this.buttonTwo = 'Finished'
      this.buttonOne = 'ToDo'
      this.designTwo =`background:#44bd32; color:white;`
      this.designOne = `background:#8c7ae6; color:white;`
       this.template = `max-width: 18rem; background:#e1b12c; `
    } else if (this.name === 'Finished') {
      this.buttonOne = 'OnGoing'
      this.designOne = `background:#e1b12c; color:white;`
       this.template = `max-width: 18rem; background:#44bd32; `
      this.buttonTwo = null
    }
  }
}
</script>

<style scoped>

.BackLog{
  background-color: #00b894;

}
.ToDo{
  background-color: #00cec9;

}
.OnGoing{
  background-color: #0984e3;


}
.Finished{
  background-color: #6c5ce7;


}
.delete{
  background-color: #c23616;


}
  
</style>
