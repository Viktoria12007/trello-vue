<template>
  <ul class='boards'>
    <p v-if="!boardsListData.length">У вас пока нет созданных досок!</p>
    <board-item 
    v-for="item in boardsListData"
    :key="item.id"
    :boardItemData="item"
    @boardDelete="boardDelete"
    v-else  
    />
    
  </ul>
</template>

<script>
import boardItem from './board-item.vue'

export default {
  name: 'boards-list',
  components: {
    boardItem
  },
  props: {
    boardsListData: {
      type: Array,
      default() {
      return []
    }
  },
  // item: {
  //   type: Object,
  //   default() {
  //     return {}
  //   }
  // }
},
// data () {
//   return {
//     item: {}
//   }
// }
methods: {
  // boardTitleEdit(currentId, currentTitle) {
  //   this.$emit('boardTitleEdit', currentId, currentTitle)
    // this.boardsListData[currentId].title = currentTitle
    // console.log(this.boardsListData[currentId].title)
  // }
  boardDelete(currentId) {
     this.$emit('boardDelete', currentId)
  },
  // taskAdd(newTask, currentId) {
  //    this.$emit('taskAdd', newTask, currentId)
  // }
}
}
</script>

<style>
.boards {
    display: flex;
    flex-wrap: wrap;
    align-items: flex-start;
    justify-content: center;
}
</style>
