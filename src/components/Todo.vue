<template>
  <transition name="slide-fade">
    <div class="bg-white rounded-lg p-2 my-2" v-if="show">
      <p class="text-lg font-medium">
        {{ title }} -
        <span class="text-sm font-light text-gray-500"> {{ date }} </span>
      </p>
      <p class="my-2">
        {{ description }}
      </p>
      <button
        @click="done()"
        class="
          bg-red-400
          rounded-lg
          text-white
          hover:bg-red-600
          p-2
          my-2
          transition
        "
      >
        I was tired
      </button>
      <button
        @click="done()"
        class="
          bg-gray-200
          rounded-lg
          text-gray-400
          hover:bg-gray-300 hover:text-gray-500
          p-2
          m-2
          transition
        "
      >
        Done
      </button>
    </div>
  </transition>
</template>
<script>
export default {
  props: ["id", "title", "date", "description"],
  data() {
    return {
      show: false,
    };
  },
  methods: {
    done() {
      let todos = JSON.parse(localStorage.getItem("todos"));
      for (var i = 0; i < todos.length; i++) {
        if (this.id === todos[i].id) {
          todos.splice(i, 1);
        }
      }
      localStorage.setItem("todos", JSON.stringify(todos));
      this.show = false;
    },
  },
  mounted() {
    this.show = true;
  },
};
</script>
<style lang="scss" scoped>
.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
</style>