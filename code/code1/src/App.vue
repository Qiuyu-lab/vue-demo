<template>
  <div>
  <h1>APP 根组件 </h1>

  <hr  />
  
  <!-- 使用todo-inputs组件 -->
  <!-- 监听TodoInput的自定义事件 -->
  <todo-input @add="onAddNewTask"></todo-input>

  <!-- 使用todo-list组件 -->
  <todo-list :list="tasklist" class="mt-2"></todo-list>

  <!-- 使用todo-button组件 -->
  <todo-button :active="activeBtnIndex"></todo-button>
  </div>
</template>

<script>
// 导入TodoList组件
import TodoList from './components/todo-list/TodoList.vue'
// 导入TodoInput组件
import TodoInput from './components/todo-input/TodoInput.vue'
// 导入TodoButtont组件
import TodoButton from './components/todo-button/TodoButton.vue'

export default {
  name: 'MyApp',

// 注册私有组件
  components: {
    TodoList,
    TodoInput,
    TodoButton,
  },

  data() {
    return {
      // 任务列表的数据
      todolist: [
        { id: 1, task: '周一早晨9点开会', done: false },
        { id: 2, task: '周一晚上7点聚餐', done: false },
        { id: 3, task: '准备周三上午的演讲稿', done: true },
      ],

      //下一个可用的ID值
      nextId: 4,

      //激活按钮的索引
      activeBtnIndex: 0
    }
  },

  methods: {
    //TodoIput组件add事件的处理函数
    onAddNewTask( taskname) {
      //1.向任务列表中新增任务信息
      this.todolist.push({
        id: this.nextId,
        task: taskname,
        done: false,
      })

      //2.让nextId自增+1
      this.nextId++
    },
  },

  computed: {
    //根据激活按钮的索引值，动态计算要展示的列表数据
    tasklist() {
      //对“源数据”进行switch..case的匹配，并返回“计算之后的结果”
      switch(this.activeBtnIndex){
        case 0: //全部
          return this.todolist
        case 1: //已完成
          return this.todolist.filter(x => x.done)
        case 2: //未完成
          return this.todolist.filter(x => !x.done)
      }
    },
  },

}
</script>

<style lang="less" scoped> </style>
