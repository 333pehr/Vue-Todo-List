<template>
<div class="errorBox" v-if="titleErr">
  <span>Title must be filled</span>
</div>
<h1 class="header">Todo List</h1>
<div class="inputContainer">
  <div class="title">
    <span>Title</span>
    <input type="text" placeholder="e.g. Math Homework" v-model="Title" required>
  </div>
  <br>
  <div class="row">
  <div class="importance">
      <span>Importance</span>
      <select v-model="Importance">
        <option value="High">High</option>
        <option value="Normal">Normal</option>
        <option value="Low">Low</option>
      </select>
    </div>
    <div class="deadLine">
      <span>Deadline</span>
      <input type="date" v-model="Deadline" required>
    </div>
  </div>
  <br>
  <br>
  <div class="description">
    <span>Description</span>
    <textarea cols="30" rows="10" style="resize:none" v-model="Description"></textarea>
  </div>
  <button class="addButton" @click="pushTask()"> ADD </button>
</div>
<div class="table">
  <table>
    <tr class="tableHeader">
      <th>Task Title</th>
      <th>Deadline</th>
      <th>Importance</th>
      <th>Details</th>
    </tr>
    <tr v-for="Task in Tasks" :key="Task">
      <th>{{Task.title}}</th>
      <th>{{Task.deadline}}</th>
      <th :class="{
                'text-high': Task.importance === 'High',
                'text-normal': Task.importance === 'Normal',
                'text-low': Task.importance === 'Low',
              }">{{Task.importance}}</th>
      <th>
       <button class="detailsBut" @click="showkey(Task)">Details</button>
      </th>
    </tr>
  </table>
</div>
  <TaskDetail :chosenTask="chosenTask" 
    v-if="showDetail" @closeDetail="closeMore()"
    @deleteDetail="deletefunc(chosenTask)"/>

<div class="programmer">
  <a href="https://github.com/333pehr" target="_blank">GitHub</a>
  <span>
    Sepehr Latifi Azad
  </span>
  <a href="https://www.linkedin.com/in/sepehrlatifiazad" target="_blank">LinkedIn</a>
</div>
</template>

<script>
import TaskDetail from './components/TaskDetail.vue';
export default {
  name: 'App',
  components:{
    TaskDetail
},
  data(){
    return{
      Title: '',
      Description: '',
      Importance: '',
      Deadline: '',
      Tasks:[],
      titleErr: false,
      chosenTask: null,
      showDetail: false,
    }
  },
  methods:{
    pushTask(){
      if(this.Title !== ''){
        this.Tasks.push({
          title: this.Title,
          description: this.Description,
          importance: this.Importance,
          deadline: this.Deadline,
        })
        this.titleErr= false;
      }
      else{
        this.titleErr= true;
      }
    },
    showkey(key){
      this.chosenTask = key;
      this.showDetail = true;
    },
    closeMore(){
      this.showDetail = false;
    },
    deletefunc(chosenTask){
      console.log(chosenTask);
      this.Tasks = this.Tasks.filter((item) => {
          return chosenTask !== item
        });
      this.showDetail = false;
      }
    }
  }
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Times New Roman', Times, serif;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align: center;
}
.errorBox{
  background-color: rgba(210, 4, 45, 0.4);
  width: 50%;
  height: 50px;
  margin: 0 auto;
  margin-top: 15px;
  border: 2px solid red;
  border-radius: 5px;
}
.errorBox span{
  color: red;
  font-size: 17px;
  margin: 0 auto;
  margin-top: 15px;
  display: block;
  letter-spacing: 1px;
}
.header{
  margin-top: 50px;
  color: white;
  font-weight: 700;
  letter-spacing: 2px;
}
.inputContainer{
  color: white;
  border: 3px solid white;
  width: 70%;
  padding: 10px;
  background-color: rgba(0, 0, 0, 0.3);
  border-radius: 15px;
  margin: 0 auto;
  margin-top: 50px;
  height: 405px;
}
.title{
  width: 70%;
  margin: 0 auto;
  margin-top: 15px;
}
.title span{
  letter-spacing: 0.9px;
  text-align: left;
  display: flex;
  margin-bottom: 5px;
}
.title input{
  width: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  border: 1px solid white;
  border-radius: 5px;
  color: white;
  padding: 10px 0px 10px 15px;
  font-size: 15px;
  letter-spacing: 0.9px;
  margin: 0 auto;
  display: flex;
}
.description{
  width: 70%;
  margin: 0 auto;
}
.description span{
  letter-spacing: 0.9px;
  text-align: left;
  display: flex;
  margin-bottom: 5px;
}
.description textarea{
  height: 100px;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  color: white;
  border: 1px solid white;
  border-radius: 5px;
  font-size: 15px;
}
.row{
  width: 70%;
  margin: 0 auto;
  display: inline-flex;
  justify-content:space-between;
}
.importance{
  width: 45%;
}
.importance span{
  letter-spacing: 0.9px;
  text-align: left;
  display: flex;
  margin-bottom: 5px;
}
.importance select{
  background-color: rgba(0, 0, 0, 0.4);
  color: white;
  border: 1px solid white;
  border-radius: 5px;
  padding: 10px;
  font-size: 15px;
  width: 100%;
  text-align: center;
}
.deadLine{
  width: 45%;
}
.deadLine input{
  padding: 10px;
  background-color: rgba(0, 0, 0, 0.4);
  color: white;
  border: 1px solid white;
  border-radius: 5px;
  width: 100%;
}
.deadLine span{
  letter-spacing: 0.9px;
  text-align: left;
  display: flex;
  margin-bottom: 5px;
}
.addButton{
  margin-top: 30px;
  width: 15%;
  height: 35px;
  background-color: rgba(0, 0, 0, 0.4);
  color: white;
  border: 1px white solid;
  border-radius: 5px;
  transition: 500ms;
  letter-spacing: 1px;
}
.addButton:hover{
  background-color: white;
  color: black;
}
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
  color: white;
}
td, th {
  border: 2px solid #ffffff;
  text-align: center;
  padding: 8px;
}
tr:nth-child(even) {
  background-color: rgba(0, 0, 0, 0.6);
}
.table{
  width: 90%;
  margin: 0 auto;
  margin-top: 50px;
  margin-bottom: 50px;
}
.tableHeader{
  color: #BDBDBD;
  letter-spacing: .9px;
  font-size: 16px;
}
.detailsBut{
  background-color: #FBC02D;
  border: 1px solid #FBC02D;
  border-radius: 5px;
  color: black;
  height: 25px;
  width: 70px;
  transition: 500ms;
  cursor: pointer;
}
.detailsBut:hover{
  color: #FBC02D;
  background-color: black;
}
.text-high{
  color:red; 
}
.text-normal{
  color: #FBC02D;
}
.text-low{
  color: green;
}
.programmer{
  width: 100%;
  background-color: rgba(0, 0, 0, 0.6);
  display: inline-flexbox;
  position: fixed;
  bottom: 0px;
  text-align: center;
  height: 40px;
  padding-top: 10px;
  margin: 0 auto;
}
.programmer span{
  color: #ffffff;
  margin: 0 25px;
  font-size: 20px;
}
.programmer a{
  color: #BDBDBD;
}
</style>
