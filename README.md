# v-easytable


API   http://doc.huangsw.com/vue-easytable/app.html#/intro

## [vuex](https://vuex.vuejs.org/zh/guide/mutations.html)  使用单一状态树
* ### State
` mapState`辅助函数
```
//在单独构建的版本中辅助函数为 Vuex.mapState
import { mapState } from 'vuex'

export default {
  // ...
  computed: mapState({
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
```
当映射的计算属性的名称与state的子节点名称相同时，也可以给mapState传一个字符串数组

```
computed: mapState([
  // 映射 this.count 为 store.state.count
  'count'
])
```
* ### Getter
Vuex 允许在 store 中定义“getter”（可以认为是 store 的计算属性）。就像计算属性一样，getter 的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算。

Getters接受state作为其第一个参数

```
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
```
Getters也可以接受其他getter作为第二参数

```
getters:{
 //....
 doneTodosCount:(state,getters)=>{
    return getters.doneTodos.length
 }
}
```
#### 通过方法访问
```
getters: {
  // ...
  getTodoById: (state) => (id) => {
    return state.todos.find(todo => todo.id === id)
  }
}
store.getters.getTodoById(2) // -> { id: 2, text: '...', done: false }
```

#### 辅助函数
mapGetters辅助函数仅仅是将store中的getters映射到局部计算属性
```
import { mapGetters } from 'vuex'

export default {
  // ...
  computed: {
  // 使用对象展开运算符将 getter 混入 computed 对象中
    ...mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
  }
}
```
* ### Mutation 
更改Vuex的store中的状态的唯一方法是提交mutation。Vuex中的mutation非常类似于事件：每个mutation都有一个字符串的`事件类型（type）`和一个`回调函数（handler）`。






