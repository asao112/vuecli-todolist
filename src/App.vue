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
      <table>
        <thead>
          <tr>
            <th>ID コメント</th>
            <th class="state">状態</th>
          </tr>
        </thead>
        <tbody>
          <tr class="taskList" v-for="(list, key) in lists" :key="list.status">
            <td>{{key}} {{ list.task }}</td>
            <td>
              <button class="statusTask" @click="changeStatus(key)">{{list.status}}</button>
              <button class="deleteTask" @click="deleteList(key)">削除</button> 
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div>
      <h2>新規タスクの追加</h2>
      <input type="text" v-model="newTask">
      <input type="submit" value="追加" @click="addList">
    </div>
  </div>
</template>
<script>
export default {
  data: () => ({
    lists:[],
    newTask:''
  }),
  methods:{
    // Todoの追加
    addList:function(e){
      e.preventDefault();
      if (this.newTask.match(/\S/g)) 
        this.lists.push({
          task: this.newTask,
          status:"作業中",
      });
    },
    //削除機能
    deleteList:function(key){
      this.lists.splice(key, 1)
    },
    //状態の変更
    changeStatus:function(key) {
      if (this.lists[key].status === "作業中"){
        this.lists[key].status = "完了";
      }else if(this.lists[key].status === "完了") {
        this.lists[key].status = "作業中";
      }
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
.statusTask{
  position:fixed;
  left:100px;
}
th.state{
  position:fixed;
  left: 135px;
}
</style>