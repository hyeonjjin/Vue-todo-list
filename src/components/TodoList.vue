<template>
  <section>
    <transition-group name="list" tag="ul">
      <li v-for="(todoItem, index) in propsdata" :key="todoItem" class="shadow">
        <div v-show="!editing || ind != index">
          <i class="checkBtn fas fa-check" aria-hidden="true"></i>
            {{ todoItem }}
          <span class="removeBtn" type="button" @click="removeTodo(todoItem, index)">
            <i class="far fa-trash-alt" aria-hidden="true"></i>
          </span>
          <span class="editBtn" type="button" @click="editTodo(todoItem, index)">
            <i class="far fa-edit" aria-hidden="true"></i>
          </span>
        </div>
        <div v-show="editing && ind == index">
          <label>item: </label>
          <input type="text" v-model="todo" >
          <span class="saveBtn" type="button" @click="hideForm(todoItem, index)">
            <i class="far fa-save" aria-hidden="true"></i>
          </span>
        </div>
      </li>
    </transition-group>
  </section>
</template>

<script>
export default {
  data() {
    return {
      todo: "",
      editing: false,
      ind: -1
    }
  },
  props: ['propsdata'],
  methods: {
    removeTodo(todoItem, index) {
      this.$emit('removeTodo', todoItem, index);
    },
    showForm() {
      this.editing = true;
    },
    hideForm(todoItem, index) {
      this.editing = false;
      this.$emit('editTodo', this.todo, index);
    },
    editTodo(todoItem, index) {
      this.showForm();
      this.ind = index;
      this.todo = todoItem;
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
    display: block;
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
  .removeBtn, .editBtn, .saveBtn {
    float: right;
    margin-left: 5px;
    color: #de4343;
  }
  .list-enter-active, .list-leave-active {
    transition: all 1s;
  }
  .list-enter, .list-leave-to {
    opacity: 0;
    transform: translateY(30px);
  }
</style>
