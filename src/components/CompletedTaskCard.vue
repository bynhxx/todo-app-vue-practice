<template>
    <div class="cardCompleted">
        <h4>{{title}}</h4>
    </div>
</template>

<script>
export default {
props: ['title', 'description']
}
</script>

<style scoped>

.cardCompleted{
    background-color: #c6cace;
    padding: 20px 30px;
    border-radius: 3px;
    color: rgb(36, 39, 51);
    margin-top: 20px;
    
}

</style>