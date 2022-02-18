<template>
  <BackButton url="/ScheduleTable" title="Back To The Table" />
  <Enter>
    <div class="p-5 flex flex-col bg-gray-100">
      <Todo
        :id="todo.id"
        :title="todo.title"
        :date="todo.date"
        :description="todo.description"
      />
    </div>
  </Enter>
</template>
<script>
import BackButton from "@/components/BackButton.vue";
import Todo from "@/components/Todo.vue";
import Enter from "@/components/Enter.vue";

export default {
  components: {
    BackButton,
    Enter,
    Todo,
  },
  data() {
    return {
      todo: {},
    };
  },
  created() {
    let todo = JSON.parse(localStorage.getItem("todos"))[
      this.$route.params.index
    ];
    this.todo = todo;
  },
};
</script>