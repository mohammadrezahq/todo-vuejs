<template>
  <BackButton url="/" title="Back To Home" />
  <Enter>
    <div class="my-4">
      <h1 class="text-center text-3xl font-medium select-none">Schedule</h1>
    </div>
    <div class="bg-gray-100 m-auto flex flex-col items-center p-4">
      <input
        class="block w-96 p-2 m-2 rounded-lg outline-none"
        type="text"
        v-model="title"
        placeholder="title"
      />
      <input
        class="block w-96 p-2 m-2 rounded-lg outline-none"
        type="date"
        v-model="date"
      />
      <textarea
        class="block p-2 m-2 w-96 rounded-lg outline-none"
        rows="10"
        placeholder="Description"
        v-model="description"
      ></textarea>
      <button
        class="px-4 py-2 w-32 bg-white rounded-lg hover:bg-gray-200 transition"
        @click="submit()"
      >
        Submit
      </button>
    </div>
  </Enter>
</template>
<script>
import BackButton from "@/components/BackButton.vue";
import Enter from "@/components/Enter.vue";

export default {
  name: "DoSchedule",
  components: {
    BackButton,
    Enter,
  },
  data() {
    return {
      title: "",
      date: "",
      description: "",
    };
  },
  methods: {
    submit() {
      var todos = localStorage.getItem("todos");

      var id;
      var length;
      var list = [];

      if (todos == null || todos == "[]") {
        id = 0;
        length = 0;
      } else {
        list = JSON.parse(todos);
        length = list.length;
        id = list[list.length - 1].id + 1;
      }

      let todo = {
        id: id,
        title: this.title,
        date: this.date,
        description: this.description,
      };

      list[length] = todo;

      localStorage.setItem("todos", JSON.stringify(list));
      this.$router.push("/");
    },
  },
  created() {
    let today = new Date();
    var month = today.toLocaleDateString("en-US", { month: "2-digit" });
    var day = today.toLocaleDateString("en-US", { day: "2-digit" });
    var year = today.toLocaleDateString("en-US", { year: "numeric" });

    let tommorow = year + "-" + month + "-" + day;
    this.date = tommorow;
  },
};
</script>