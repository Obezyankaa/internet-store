<script setup>
defineProps({
  data: {
    message: 'Ведите задачу !',
    tipes: 'button',
    disState: true,
    taskList: [
      'Развернуть окружение в Codepen',
      'Пройти курс по Vue',
      'Сделать интернет-магазин на Vue',
    ],
    taskListDone: [
      'дз скиллбоксу скинул',
      'показания счетчика передал',
    ]
  }
})
</script>

<template>
<h1>Список задач</h1>
<div>Осталось сделать задач: <span class="counter">3</span></div>
<div class="list">

  <div class="item" v-for="taskBlock in taskList">
    <input type="checkbox">
    {{ taskBlock }}
  </div>
  <div class="item done" v-for="taskDoneBlock in taskListDone">
    <input type="checkbox">
    {{ taskDoneBlock }}
  </div>
  <div class="form">
    <input v-bind:placeholder=message>
    <button v-bind:type=tipes v-bind:disabled=disState>Добавить</button>
  </div>
</div>
</template>

