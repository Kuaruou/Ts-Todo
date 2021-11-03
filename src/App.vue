<template>
  <div class="container mx-auto mt-4">
    <h1 class="text-3xl text-center p-2 font-bold">
      Vue 3 Todo App with TS and Vuex 4
    </h1>

    <div v-if="loading">
      <h3 class="text-center mt-4">
        Loading...
      </h3>
    </div>
    <div v-else>
      <p class="text-center mt-2">
        {{ completedCount }} of {{ totalCount }} completed.
      </p>
      <NewItem />
      <TodoList />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, computed, onMounted } from 'vue';
import TodoList from './components/TodoList.vue'
import NewItem from './components/NewItem.vue'
import { useStore } from './store'
import { ActionTypes } from './store/actions'

export default defineComponent({
  components: { TodoList, NewItem },
  setup() {
    const store = useStore()
    
    const loading = computed(() => store.state.loading)
    onMounted(() => store.dispatch(ActionTypes.GetTodoItems))

    const completedCount = computed(() => store.getters.completedCount)
    const totalCount = computed(() => store.getters.totalCount)

    return { loading, completedCount,  totalCount }
  }
})
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

  .text-center {
    text-align: center;
  }

  .flex-grow {
    flex-grow: 1;
  }

  .flex-shrink-0 {
    flex-shrink: 0;
  }
  
</style>
