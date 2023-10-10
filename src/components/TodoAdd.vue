<template>
    <div class="todolist">
        <div class="input">
            <input type="text" placeholder="Enter message" v-model="newTask.name">
        </div>
        <button class="bt-submit" @click="createTask">SUBMIT</button>

    </div>
</template>
    
<script>
import * as uuid from "uuid"

export default {
    name: "TodoAdd",
    data() {
        return {
            newTask: {
                id: 0,
                name: "",
                complete: false,
            }
        }
    },
    methods: {
        createTask() {
            if (this.newTask.name != "") {
                const newID = uuid.v4
                this.newTask.id = newID()
                const item = { ...this.newTask }
                this.$emit('onSubmit', item)
                this.newTask.name = ""
            }
            else alert('กรุณากรอกข้อมูล')
        }
    }
}
</script>

<style scoped>
.todolist {
    display: flex;
    justify-content: space-between;
    margin: 10px 0 10px 0;
}

.todolist .input {
    width: 90%;
    border-bottom: 2px solid darkgray;
}

.todolist .input input {
    width: 100%;
    border: none;
}

.bt-submit {
    color: white;
    background-color: rgba(6, 163, 45, 0.891);
    border: none;
    padding: 8px 22px 8px 22px;
    border-radius: 5px;
    transition: all 0.2s ease;
}

.bt-submit:hover {
    background-color: white;
    color: rgb(21, 122, 50);
    border: 2px solid rgb(34, 163, 41);
    font-weight: bold;
}
</style>