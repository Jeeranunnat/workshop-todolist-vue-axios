<template>
    <div class="TodoList" v-for="(task, id) in tasks" :key="id" :class="task.complete ? 'task-true' : 'task-false'">
        <div class="list-left">
            <input type="checkbox" @click="$emit('onToggle', task.id)" />
            <p>{{ task.name }}</p>
        </div>
        <div class="list-right">
            <button class="bt-close" @click="$emit('onRemove', task.id)"> X </button>
        </div>
    </div>
</template>
    
<script>
export default {
    name: "TodoList",
    props: ['tasks'],
    emits: ['onRemove', 'onToggle']
}
</script>

<style scoped>
.TodoList {
    background-color: lightgray;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 20px;
    padding: 10px;
    transition: all 0.2s ease;
    border-radius: 5px;
}

.TodoList:hover {
    font-weight: bold;
}

.list-left {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.list-left p {
    padding-left: 10px;
}

.bt-close {
    color: white;
    background-color: rgba(255, 0, 0, 0.891);
    border: none;
    padding: 8px 22px 8px 22px;
    border-radius: 5px;
    transition: all 0.2s ease;
}

.bt-close:hover {
    background-color: white;
    color: red;
    border: 2px solid red;
    font-weight: bold;
}

.task-true {
    text-decoration: line-through;
}

.task-false {
    text-decoration: none;
}
</style>