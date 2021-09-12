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
            @click.prevent="boardTitleEdit"
            :disabled="disabledBoardSaveButton"
            :class="[disabledBoardSaveButton ? 'button_disabled' : '']">
              Сохранить
              </button>
            <button 
            class='button button_cancel'
            @click.prevent="boardForm=false">
              Отмена
              </button>
                </form>
          <button 
          class='button button_delete button_delete-board'
          @click.prevent="boardDelete">Удалить доску</button>
              <tasks-list 
              :tasksListData="boardItemData.tasks"/>
                <button class='button button_add'
                 @click="taskForm=true" 
                 v-show="!taskForm">
                  Добавить задачу
                  </button>
                <form class='change-form'
                v-show="taskForm">
                <label class='change-label'>
                <div class='change-input-error'></div>
                <input class='change-input' 
                placeholder='Введите название задачи'
                v-model="taskTitle">
                </label>
                <label class='change-label'>
                <div class='change-textarea-error'></div>
                <textarea 
                cols='10' 
                rows='10' 
                class='change-textarea' 
                placeholder='Введите описание задачи'
                v-model="taskText">
                </textarea>
                </label>
                <button class='button button_save'
                 @click.prevent="taskAdd"
                 :disabled="disabledTaskSaveButton"
                 :class="[disabledTaskSaveButton ? 'button_disabled' : '']">
                  Сохранить
                  </button>
                    <button class='button button_cancel'
                    @click.prevent="taskForm=false">
                      Отмена
                    </button>
                </form>
                </li>
</template>

<script>
import tasksList from './tasks-list.vue'

export default {
  name: 'board-item',
   components: { 
    tasksList 
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
    },
    //  tasksListData: {
    //   type: Array,
    //   default() {
    //     return []
    //   }
    // }
  },
  data() {
    return {
    boardForm: false,
    boardTitle: this.boardItemData.title,
    taskForm: false,
    taskTitle: '',
    taskText: '',
    }
  },
  methods: {
    boardTitleEdit() {
      console.log(this.boardItemData.id);
      this.boardItemData.title = this.boardTitle;
      // this.$emit('boardTitleEdit', this.boardItemData.id, this.boardTitle);
      this.boardForm=false;
    },
    boardDelete() {
      this.$emit('boardDelete', this.boardItemData.id);
    },
    taskAdd() {
      const newTask = {};
      // newTask.id = new Date().format('m-d-Y h:i:s');
      // newTask.id = new Date();
      // newTask.id = dateFormat(new Date(), 'm-d-Y h:i:s');
      newTask.id = (new Date()).toString();
      console.log(typeof(newTask.id));
      newTask.title = this.taskTitle;
      newTask.text = this.taskText;
      // this.boardsListData.push(newBoard);
      this.taskTitle = '';
      this.taskText = '';
      // console.log(this.boardsListData)
      this.taskForm=false;
      this.boardItemData.tasks.push(newTask);
      // this.$emit('taskAdd', newTask, this.boardItemData.id);
    }
  },
  computed: {
    disabledBoardSaveButton() {
      if (this.boardTitle.trim().length > 0) {
        return false
      } 
      else {
        return true
      }
    },
    disabledTaskSaveButton() {
       if (this.taskTitle.trim().length > 0 && this.taskText.trim().length > 0) {
        return false
      } 
      else {
        return true
      }
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
.change-board-input {
    margin-bottom: 10px;
}
.button_edit-board,
.button_delete-board {
    margin-bottom: 10px;
}
.button_delete,
.button_cancel {
    border-color: lightcoral !important;
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
    background-color: lightgray;
}
.board-title {
    margin-bottom: 10px;
}
.button_disabled {
  background-color: rgb(211, 211, 211, .4);
}
</style>
