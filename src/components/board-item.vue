<template>
   <li class='board'>
      <h2 class='title board-title'
      v-show="!boardForm">
      {{boardItemData.title}}
      </h2>
        <button 
        @click="boardForm=true" 
        v-show="!boardForm" 
        class='button button_edit button_edit-board'>
        Редактировать доску
        </button>
          <form v-show="boardForm" class='change-form'>
            <label class='change-label'>
              <div class='change-input-error'></div>
              <input class='change-input change-board-input' 
              placeholder='Введите название доски'
              v-model="boardTitle">
            </label>
            <button 
            class='button button_save'
            @click.prevent="boardTitleEdit">
              Сохранить
              </button>
            <button 
            class='button button_cancel'
            @click.prevent="boardForm=false">
              Отмена
              </button>
                </form>
          <button class='button button_delete button_delete-board'>Удалить доску</button>
              <!-- <tasks-list /> -->
                <button class='button button_add'>
                  Добавить задачу
                  </button>
                <form class='change-form'>
                <label class='change-label'>
                <div class='change-input-error'></div>
                <input class='change-input' 
                placeholder='Введите название задачи'>
                </label>
                <label class='change-label'>
                <div class='change-textarea-error'></div>
                <textarea 
                cols='10' 
                rows='10' 
                class='change-textarea' 
                placeholder='Введите описание задачи'>
                </textarea>
                </label>
                <button class='button button_save'>
                  Сохранить
                  </button>
                    <button class='button button_cancel'>
                      Отмена
                    </button>
                </form>
                </li>
</template>

<script>
// import tasksList from './tasks-list.vue'

export default {
  name: 'board-item',
   components: { 
    // tasksList 
    },
  props: {
    // boardsListData: {
    //   type: Array,
    //   default() {
    //     return []
    //   }
    // },
    boardItemData: {
      type: Object,
      default() {
        return {}
      }
    }
  },
  data() {
    return {
    boardForm: false,
    boardTitle: this.boardItemData.title
    }
  },
  methods: {
    boardTitleEdit() {
      console.log(this.boardItemData.id)
      this.$emit('boardTitleEdit', this.boardItemData.id);
    }
  }
}
</script>

<style>
.board {
    display: flex;
    flex-direction: column;
    width: 300px;
    min-height: 400px;
    padding: 20px 10px;
    margin: 10px;
    border-radius: 12px;
    border: 1px solid lightgray;
}
.change-label {
    position: relative;
    margin-bottom: 5px;
}
.change-input-error,
.change-textarea-error {
    height: 20px;
    font-size: 12px;
    color: lightcoral;
    margin-left: 10px;
}
.change-input-error_main {
    margin-left: 20px;
}
.change-input,
.change-textarea {
  width: 100%;
  font-family: inherit;
  color: #333333;
  padding: 5px 10px;
  border-radius: 50px;
  border: 2px solid lightgray;
  background-color: white;
  
}
.change-input_main {
  width: 80%;
  font-size: 20px;
  padding: 8px 20px;
  border-radius: 0;
  border-color: lightcoral;
}
.change-board-input {
    margin-bottom: 10px;
}
.button_edit-board,
.button_delete-board {
    margin-bottom: 10px;
}
.button_delete,
.button_cancel {
    border-color: lightcoral;
    background-color: transparent;
}
.button_add {
    padding: 10px 20px;
    margin-top: 10px;
    background-color: lightpink;
}
.button_edit,
.button_save {
    margin-right: 5px;
}
.board-title {
    margin-bottom: 10px;
}
</style>
