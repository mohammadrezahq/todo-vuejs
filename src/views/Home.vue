<template>
  <Enter>
    <div class="home">
      <div class="my-4">
        <h1 class="text-center text-3xl font-medium select-none">
          Things To do
        </h1>
        <p class="text-center select-none">What I should to do today</p>
      </div>
      <div class="p-5 flex flex-col bg-gray-100">
        <Todo
          v-for="(todo, i) in todos"
          :id="todo.id"
          :key="i"
          :title="todo.title"
          :date="todo.date"
          :description="todo.description"
        />
        <p v-if="todos.length == 0">Add something for today</p>
      </div>
      <Buttons />
    </div>
  </Enter>
</template>

<script>
import Todo from "@/components/Todo.vue";
import Enter from "@/components/Enter.vue";
import Buttons from "@/components/Home/Buttons.vue";

export default {
  name: "Home",
  components: {
    Enter,
    Todo,
    Buttons,
  },
  date() {
    return {
      todos: [],
    };
  },
  created() {
    let todos = JSON.parse(localStorage.getItem("todos"));

    if (todos) {
      let today = new Date();
      var month = today.toLocaleDateString("en-US", { month: "2-digit" });
      var day = today.toLocaleDateString("en-US", { day: "2-digit" });
      var year = today.toLocaleDateString("en-US", { year: "numeric" });

      today = year + "-" + month + "-" + day;

      todos = Object.values(todos).filter(function (todo) {
        if (todo.date == today) {
          return todo;
        }
      });
    } else {
      todos = [];
    }

    this.todos = todos;
  },
};
</script>
