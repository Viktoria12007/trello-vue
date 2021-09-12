<template>
<li class='task'>
  <h3 class='task-title'>{{taskItemData.title}}</h3>
  <p class='task-text'>{{taskItemData.text}}</p>
  <button class='button button_edit'>Редактировать</button>
  <form class='change-form'>
  <label class='change-label'>
    <div class='change-input-error'></div>
    <input class='change-input' placeholder='Введите название задачи'>
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
    <button class='button button_delete'>
      Удалить
    </button>
</li>
</template>

<script>
export default {
  name: 'task-item',
  props: {
    taskItemData: {
      type: Object,
      default() {
        return {}
      }
    }
  }
}
</script>

<style>
.task {
    width: 100%;
    padding: 10px;
    margin: 5px 0;
    border-radius: 6px;
    border: 2px solid lightpink;
    cursor: grab;
    background-color: #fcfcf9;
}
.task-title {
    margin-bottom: 5px;
}
.task-text {
    margin-bottom: 5px;
}
.change-textarea {
  border-radius: 25px;  
  resize: none;
  margin-bottom: 10px;
}
</style>
