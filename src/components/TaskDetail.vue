<template>
    <div class="background" @click.self="close()">
        <div class="detailContainer">
            <div class="General">
                <h2>{{chosenTask.title}}</h2>
                <div class="smallSpan">
                <span :class="{
                'text-high': chosenTask.importance === 'High',
                'text-normal': chosenTask.importance === 'Normal',
                'text-low': chosenTask.importance === 'Low',
              }">{{chosenTask.importance}}</span>
                <span class="span2">{{chosenTask.deadline}}</span>
                </div>
            </div>
            <div class="detail">
                <span>
                    {{chosenTask.description}}
                </span>
            </div>
            <div class="buttons">
                <button class="closeBtn" @click="close()">CLOSE</button>
                <button class="deleteBtn" @click="deleteFunc()" >DELETE</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TaskDetail',
    props:['chosenTask'],
    methods: {
        close(){
            this.$emit('closeDetail');
        },
        deleteFunc(){
            this.$emit('deleteDetail',this.chosenTask);
        }
    }
}
</script>

<style>
.background{
    background-color: rgba(0, 0, 0, 0.7);
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
}
.detailContainer{
    background-color: white;
    width: 50%;
    height: 50%;
    border-radius: 10px;
    margin: 0 auto;
}
.General h2{
    margin-top: 100px;
    display: block;
    position: relative;
    top: 20px;
    font-size: 32px;
    letter-spacing: 1px;
}
.smallSpan{
    width: 70%;
    margin: 0 auto;
    margin-top: 40px;
    display: inline-flex;
    justify-content: space-between;
    font-size: 20px;
}
.detail{
    text-align: justify;
    width: 80%;
    margin: 0 auto;
    margin-top: 35px;
    font-size: 18px;
    line-height: 25px;
    height: 250px;
    letter-spacing: 1px;
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
.buttons{
    display: inline-flex;
    width: 70%;
    justify-content: space-between;
    margin-top: 25px;
}
.closeBtn{
    background-color: #455A64;
    border: 2px solid #455A64;
    border-radius: 5px;
    padding: 10px 12px;
    color: white;
    font-weight: 600;
    letter-spacing: 1px;
    cursor: pointer;
    transition: 500ms;
}
.closeBtn:hover{
    background-color: white;
    color: #455A64;
}
.deleteBtn{
    background-color: #D32F2F;
    border: 2px solid #D32F2F;
    border-radius: 5px;
    padding: 10px 12px;
    color: white;
    font-weight: 600;
    letter-spacing: 1px;
    cursor: pointer;
    transition: 500ms;
}
.deleteBtn:hover{
    color: #D32F2F;
    background: white;
}
</style>