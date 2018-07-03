<template>
  <el-main>
    <el-input v-model.trim="todo" placeholder="ToDoを入力">
      <el-button slot="append" @click="addTodo">Add</el-button>
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
      // Add押下時
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
      // Done押下時
      deleteTodo (index) {
        deleteLocalStorage(index)
        this.todoList = getLocalStorage()
      }
    }
  }

  // LocalStorage取得
  var getLocalStorage = function () {
    var todoList = []
    if (localStorage.getItem('todoList') != null) {
      todoList = localStorage.getItem('todoList')
      todoList = JSON.parse(todoList)
    }
    return todoList
  }

  // LocalStorage保存
  var setLocalStorage = function (todoList) {
    var jsonData = JSON.stringify(todoList)
    localStorage.setItem('todoList', jsonData)
  }

  // LocalStorage削除
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
</style>