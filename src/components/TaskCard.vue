<template>
    <div class="card" :class="priority">
        <h4>{{title}}</h4>
        <span>{{description}}</span>
        <hr>
        <div class="buttonContainer">
            <button @click="completeTask"  class="check"> Concluir </button> 
            <button @click="deleteTask" class="delete"> X </button> 
        </div>
        
    </div>
</template>

<script>
export default {
    name: "TaskCard",
    props: ["title", "description", "priority", "id"],
    methods:{
        deleteTask(){
            this.$emit('delete')
        }, 
        completeTask(){
            this.$emit('complete')
        }
    }
}
</script>

<style scoped>

.card {
    background-color: #142530; 
    color: #e6e9ec; 
    padding: 25px 40px; 
    border-radius: 4px;
    box-shadow: 2px 2px 15px rgba(0, 0, 0, 0.301);
    margin-top: 3rem;
    width: 20rem;
    height: auto;
    min-height: 13rem;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    
}

hr{
    margin-top: 2rem;
}
h3{
    margin-bottom: 10px;
}

.high{
    border-left: solid 9px tomato;
}

.medium{
    border-left: solid 9px orange;
}

.low{
    border-left: solid 9px greenyellow;
}
.buttonContainer{
    display: flex;
    justify-content: space-between;
    gap: 4px;
}

button{
    border-radius: 3px;
    border: none; 
    margin-top: 10px;
    height: 40px;
    cursor: pointer;
    transition: .2s;
    color: white; 
}

button:hover{
    filter: brightness(0.8)
}

.delete{
    background-color: rgb(253, 50, 36);
    width: 25%;
}

.check{
    background-color: rgb(39, 97, 31);
    width: 75%;
}

</style>