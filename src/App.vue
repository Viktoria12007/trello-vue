<template>
  <div id="app">
    <h1 className='title title_main'>Ваши доски</h1>
     <form class='change-form change-form_main'>
            <label class='change-label'>
                <div class='change-input-error change-input-error_main'>
                </div>
            <input 
            class='change-input change-board-input change-input_main' 
            placeholder='Введите название доски'
            type='text'
            v-model="boardTitle">
            </label>
             <button 
             class='button button_main'
             @click.prevent="addBoard"
             :disabled="disabledMainButton"
             :class="[disabledMainButton ? 'button_main_disabled' : '']"
             >
               Добавить доску
               </button>
        </form>
    <boards-list 
    :boardsListData="boardsListData"
    @boardDelete="boardDelete"
    />
  </div>
</template>

<script>
import boardsList from './components/boards-list.vue'

export default {
  name: 'App',
  components: {
    boardsList
  },
  props: {
    
  },
  data() {
      return {
        boardTitle: '',
        boardsListData: [{id: 1, title: "ifjos", tasks: []}, 
        {id: 2, title: "oioio", tasks: [{title: 'eff', text: 'wdwd'}, {title: 'iok', text: 'sfg'}]}, 
        {id: 3, title: "dsfsa", tasks: [{title: 'xzc', text: 'rete'}]}]
        // boardsListData: []
   }
  },
  methods: {
    addBoard() {
      const newBoard = {};
      newBoard.id = (new Date()).toString();
      console.log(newBoard.id);
      newBoard.title = this.boardTitle;
      newBoard.tasks = [];
      this.boardsListData.push(newBoard);
      this.boardTitle = '';
      console.log(this.boardsListData)
    },
    // boardTitleEdit(currentId, currentTitle) {
    //   this.boardsListData[currentId].title = currentTitle
    //   console.log(this.boardsListData[currentId].title)
    //   console.log(currentTitle)
    // }
    boardDelete(currentId) {
      const currentIndex = this.boardsListData.findIndex((item) => {
        item.id === currentId
      })
      console.log(currentIndex);
      this.boardsListData.splice(currentIndex, 1);
      console.log(this.boardsListData);
    },
    // taskAdd(newTask, currentId) {
    //    const currentIndex = this.boardsListData.findIndex((item) => {
    //     item.id === currentId
    //   })
    //   this.boardsListData[currentIndex].tasks.push(newTask);
    // }
  },
  computed: {
    disabledMainButton() {
      if (this.boardTitle.trim().length > 0) {
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 16px;
  text-align: center;
  color: #2c3e50;
  max-width: 1920px;
  padding: 10px;
  margin: 0 auto;
}
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
.title {
   text-align: center;
}
.title_main {
    margin-bottom: 10px;
}
.button {
    font-family: inherit;
    font-weight: 700;
    line-height: 20px;
    font-size: 16px;
    text-align: center;
    color: #333333;
    padding: 5px 10px;
    border: 1px solid transparent;
    border-radius: 50px;
    cursor: pointer;
  }
.button_main {
   padding: 13.5px 30px 10.5px 30px;
   border-radius: 0;
   background-color: lightcoral;
}
.button_main_disabled {
  background-color: rgb(240, 128, 128, .4);
}
.change-form {
    width: 100%;
    flex-direction: column;
    margin-bottom: 10px;
}
.change-form_main {
    display: block;
    align-items: center;
    margin-bottom: 20px;
}
.change-input_main {
  width: 80%;
  font-size: 20px;
  padding: 8px 20px;
  border-radius: 0;
  border-color: lightcoral;
}
</style>
