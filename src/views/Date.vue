<template>
  <BackButton url="/ScheduleTable" title="Back To The Table" />
  <Enter>
    <div class="date">
      <div class="my-4">
        <h1 class="text-center text-3xl font-medium select-none">
          Things To do
        </h1>
        <p class="text-center select-none">{{ $route.params.date }}</p>
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
        <p v-if="todos.length == 0">Add something for this day</p>
      </div>
      <div class="flex justify-center">
        <router-link
          class="bg-gray-200 text-gray-500 py-2 px-4 m-2 rounded-lg"
          to="/DoSchedule"
          >Schedule</router-link
        >
      </div>
    </div>
  </Enter>
</template>

<script>
import BackButton from "@/components/BackButton.vue";
import Todo from "@/components/Todo.vue";
import Enter from "@/components/Enter.vue";

export default {
  name: "Home",
  components: {
    BackButton,
    Enter,
    Todo,
  },
  date() {
    return {
      todos: [],
    };
  },
  created() {
    let todos = JSON.parse(localStorage.getItem("todos"));

    if (todos) {
      let theDay = this.$route.params.date;
      todos = Object.values(todos).filter(function (todo) {
        if (todo.date == theDay) {
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
