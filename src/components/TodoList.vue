<template>
  <div>
      <ul>
        <li v-for="(item, idx) in todoItem" :key="item.item" class="shadow">
          <i class="fa-check-square checkBtn" :class="{'far': !item.completed, 'fas': item.completed}" @click="toggleComplete(item)"></i>
          <span :class="{textCompleted: item.completed}">{{ item.item }}</span>
          <span class="removeBtn" @click="removeTodo(item, idx)">
            <i class="fas fa-trash"></i>
          </span>
        </li>
      </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoItem: []
    }
  },
  methods: {
    removeTodo(item, itemIdx) {
      localStorage.removeItem(item);
      this.todoItem.splice(itemIdx,1);
    },
    toggleComplete(item) {
      item.completed = !item.completed;
      localStorage.removeItem(item.item);
      localStorage.setItem(item.item, JSON.stringify(item));
    }
  },
  created() {
    if(localStorage.length > 0) {
      for(var i = 0; i<localStorage.length; i++) {
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
          this.todoItem.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
          // this.todoItem.push(localStorage.key(i));
        }
      }
    }
  }
}
</script>

<style scoped>
  ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
  }

  li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
  }

  .checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
  }

  .checkBtnCompleted {
    color: #b3adad;
  }

  .textCompleted {
    text-decoration: line-through;
    color: #b3adad;
  }

  .removeBtn {
    margin-left: auto;
    color: #de4343;
  }
</style>