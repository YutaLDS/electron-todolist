<template>
  <el-main>
    <el-input v-model.trim="todo" placeholder="ToDoÇì¸óÕ">
      <el-button slot="append" @click="addTodo()">Add</el-button>
    </el-input>

    <el-table :data="todoList" :show-header="false" stripe>
      <el-table-column prop="todo" width="auto"></el-table-column>
      <el-table-column align="center" width="100px">
        <template slot-scope="record">
          <el-button type="warning" size="mini" @click="deleteTodo(record.$index)">Done</el-button>
        </template>
      </el-table-column>
    </el-table>
  </el-main>
</template>

<script>
  export default {
    data () {
      return {
        todoList: getLocalStorage(),
        todo: ''
      }
    },
    methods: {
      // Addâüâ∫éûí«â¡
      addTodo () {
        var todoObj = {}
        todoObj.todo = this.todo

        var todoList = getLocalStorage()
        var index = todoList.length
        todoObj.id = index

        todoList.push(todoObj)
        setLocalStorage(todoList)

        this.todoList = getLocalStorage()
        this.todo = ''
      },
      // Doneâüâ∫éûçÌèú
      deleteTodo (index) {
        deleteLocalStorage(index)
        this.todoList = getLocalStorage()
      }
    }
  }

// LocalStorageÇ©ÇÁéÊìæ
var getLocalStorage = function () {
    var todoList = []
    if (localStorage.getItem('todoList') != null) {
      todoList = localStorage.getItem('todoList')
      todoList = JSON.parse(todoList)
    }
    return todoList
}

// LocalStorageÇ÷ï€ë∂
var setLocalStorage = function (todoList) {
    var jsonData = JSON.stringify(todoList)
    localStorage.setItem('todoList', jsonData)
}

// LocalStorageÇ©ÇÁçÌèú
var deleteLocalStorage = function (index) {
    var todoList = getLocalStorage()
    todoList.splice(index, 1)
    setLocalStorage(todoList)
}
</script>

<style scoped>
  main.el-main {
    width: 310px;
    margin: 0px auto;
  }
  #allClear {
    margin: 5px 0 0 0;
    float:right;
  }
</style>