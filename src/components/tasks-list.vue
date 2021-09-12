<template>
  <ul class="tasks">
     <!-- <p v-if="!boardItemData.tasks.length">У вас пока нет созданных задач!</p> -->
    <task-item 
    v-for="item in tasksListData"
    :key="item.id"
    :taskItemData="item"
    />
  </ul>
</template>

<script>
import taskItem from './task-item.vue'

export default {
  components: { 
    taskItem 
    },
  name: 'tasks-list',
  props: {
    tasksListData: {
      type: Array,
      default() {
        return []
      }
    },
    // taskItemData: {
    //   type: Object,
    //   default() {
    //     return {}
    //   }
    // }
  },
  data() {
    return {
      
    }
  }
}
</script>

<style>
.tasks {
  display: flex;
  flex-direction: column;
}
</style>
