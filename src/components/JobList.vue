<template>
  <div class="job-list">
    <ul>
      <p>Ordered by {{order}}</p>
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
          <p>{{ job.salary }} rupees</p>
        </div>
        <div class="desciption">lor</div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
// import Vue from 'vue'
import { computed, defineComponent, PropType } from 'vue'
import Job from '../types/Job'
import OrderTerm from '../types/OrderTerm'

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>
    }
  },
  setup (props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1
      })
    })

    return { orderedJobs }
  }
})
</script>

<style scoped>
  .job-list {
    max-width: 960px;
    margin: 40px auto;
  }

  .job-list ul {
    padding: 0;
  }

  .job-list li {
    list-style-type: none;
    background-color: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }
</style>