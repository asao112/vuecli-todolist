<template>
  <div id="app">
    <h1 class="title">ToDoリスト</h1>
    <div>
      <input type="radio" id="all" value="all" checked @change="all" v-model="radio">
      <label for="all">すべて</label>
      <input type="radio" id="wark" value="work" @change="work" v-model="radio">
      <label for="work">作業中</label>
      <input type="radio" id="done" value="done" @change="done" v-model="radio">
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
          <tr class="taskList" v-for="(list, key) in viewTodos" :key="key">
            <td>{{list.id}} {{ list.task }}</td>
            <td>
              <button class="statusTask" @click="changeStatus(list.id)">{{list.status}}</button>
              <button class="deleteTask" @click="deleteList(list.id)">削除</button> 
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
    newTask:'',
    displayState:''
  }),
  computed:{
    viewTodos(){
      return this.displayState
      ? this.lists.filter((i) => i.status === this.displayState)
      : this.lists
    }
  },
  methods:{
    // Todoの追加
    addList:function(e){
      e.preventDefault();
      if (this.newTask.match(/\S/g)) 
        this.lists.push({
          id: this.lists.length,
          task: this.newTask,
          status:"作業中",
      });
      this.newTask=''
    },
    //削除機能
    deleteList:function(id){
      if(id > -1)
      this.lists.splice(id, 1);
      this.lists.forEach((list, key) => {
        list.id = key
      })
    },
    //状態の変更
    changeStatus:function(id){
      const list = this.lists[id]
      if (list.status === "作業中"){
        list.status = "完了";
      }else if(list.status === "完了") {
        list.status = "作業中";
      }
    },
    all(){
      this.displayState = ''
    },
    done(){
      this.displayState = '完了'
    },
    work(){
      this.displayState = '作業中'
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
  margin: -0.8em;
}
.statusTask{
  position:fixed;
  left:100px;
  margin: -0.8em;
}
th.state{
  position:fixed;
  left: 135px;
}
</style>