<template>
  <div id="app">
    <h1 class="title">ToDoリスト</h1>
    <div>
      <input type="radio" id="all" value="all" v-model="radioTask">
      <label for="all">すべて</label>
      <input type="radio" id="wark" value="work" v-model="radioTask">
      <label for="work">作業中</label>
      <input type="radio" id="done" value="done" v-model="radioTask">
      <label for="done">完了</label>
    </div>
    <div>
      <thead>
        <tr>
          <th>ID コメント</th>
          <th class="state">状態</th>
        </tr>
      </thead>
      <ul class="taskList" v-for="(list, key) in lists" :key="key">
        {{key}}  {{ list.task }}
        <button class="stateTask">作業中</button>  
        <button class="deleteTask">削除</button> 
      </ul>
    </div>
    <div>
      <h2>新規タスクの追加</h2>
      <input type="text" v-model="task">
      <input type="submit" value="追加" @click="addList">
    </div>
  </div>
</template>
<script>
export default {
  data: () => ({
    lists: [],
  }),
  methods: {
    // Todoの追加
    addList: function(){
      this.lists.push({task: this.task})
      this.task = ''
    }
  }
};
</script>
<style>
ul{
  list-style:none;
  padding-left: 0;
}
.taskList{
  letter-spacing:0.2em;  
}
.deleteTask{
  position:fixed;
  left:160px;
}
.stateTask{
  position:fixed;
  left:100px;
}
th.state{
  position:fixed;
  left: 135px;
}
</style>