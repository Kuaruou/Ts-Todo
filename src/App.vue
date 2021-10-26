<template>
  <div class="app">
    <!-- <p>{{ name }} - {{ age }}</p> -->
    <!-- <button @click="changeName('zelda')">change name</button>
    <button @click="changeAge('24')">change age</button> -->

    <!-- <p>{{ name }} - {{ age }}</p> -->
    <header>
      <div class="order">
        <button @click="handleClick('title')">order by title</button>
        <button @click="handleClick('salary')">order by salary</button>
        <button @click="handleClick('location')">order by location</button>
      </div>
    </header>
    <JobList :jobs="jobs" :order="order" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, reactive, toRefs } from 'vue';
import JobList from './components/JobList.vue'
import Job from './types/Job'
import OrderTerm from './types/OrderTerm'


export default defineComponent({
  name: 'App',
  components: {
    JobList
  },
  setup() {
    // const state = reactive({
    //   name: 'Link',
    //   age: 25 as string | number
    // })

    // state.name = 999
    // state.age = '55'

    // return { ...toRefs(state)}

    // const name = ref('link')
    // const age = ref<number | string>(25)

    // return {name, age}

    const jobs = ref<Job[]>([
      { title: 'farm worker', location: 'lon ranch', salary: 25000, id: '1'},
      { title: 'quarryman', location: 'death mountain', salary: 30000, id: '2'},
      { title: 'lawyer', location: 'wall street', salary: 40000, id: '3'},
      { title: 'fisherman', location: 'jon harbor', salary: 40000, id: '4'},
      { title: 'prison guard', location: 'harrison prison', salary: 45000, id: '5'}
    ])
    const order = ref<OrderTerm>('title')

    const handleClick = (term: OrderTerm) => {
      order.value = term
    }

    return { jobs, handleClick, order }
  },
  // data() {
  //   return {
  //     name: 'henry',
  //     age: 25 as number | string
  //   }
  // },
  methods: {
    // changeName(name: string) {
    //   this.name = name
    //   return name
    // },

    // changeAge(age: string | number) {
    //   this.age = age
    //   return age
    // }
  }
});
</script>

<style>
  header {
    text-align: center;
  }

  header .order {
    margin-top: 20px;
  }

  button {
    margin: 0 10px;
    color: #587480;
    border: 3px solid #587480;
    background-color: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  } 
</style>
