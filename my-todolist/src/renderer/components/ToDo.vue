<template>
  <el-main>
    <!-- タスク入力 -->
    <el-input v-model="todo" placeholder="ToDoを入力" clearable>
      <el-button slot="append" size="mini" @click="addTodo">Add</el-button>
    </el-input>
    <!-- タスク一覧 -->
    <el-table :data="todoList" :show-header="false" stripe height="270px" overflow-y="scroll">
      <el-table-column prop="todo" width="auto"></el-table-column>
      <el-table-column align="center" width="100px">
        <template slot-scope="record">
          <el-button size="mini" type="warning" @click="deleteTodo(record.$index)">Done</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-button id="allClear" size="mini" type="danger" @click="deleteAllTodo(record)">All Clear</el-button>
  </el-main>
</template>

<script>
  export default {
    data () {
      return {
        todoList: [],
        todo: ''
      }
    },
    methods: {
      // タスク追加
      addTodo () {
        this.todoList.push({todo: this.todo})
        this.todo = ''
      },
      // レコード削除
      deleteTodo (index) {
        this.todoList.splice(index, 1)
      },
      // 全削除
      deleteAllTodo (record) {
        this.todoList.splice(record)
      }
    }
  }
</script>

<style scoped>
  main.el-main {
    width: 350px;
    margin: 0px auto;
  }
  #allClear {
    margin: 5px 0 0 0;
    float:right;
  }
</style>