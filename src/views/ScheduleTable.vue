<template>
  <BackButton url="/" title="Back To Home" />
  <Enter>
    <FullCalendar :options="calendarOptions" />
  </Enter>
</template>
<script>
import BackButton from '@/components/BackButton.vue';
import "@fullcalendar/core/vdom";
import FullCalendar from "@fullcalendar/vue3";
import dayGridPlugin from "@fullcalendar/daygrid";
import interactionPlugin from "@fullcalendar/interaction";
import tippy, { animateFill } from "tippy.js";
import "tippy.js/dist/tippy.css";
import "tippy.js/themes/material.css";
import "tippy.js/dist/backdrop.css";
import "tippy.js/animations/shift-away.css";
import Enter from '@/components/Enter.vue';

let th;

export default {
  components: {
    BackButton,
    FullCalendar,
    Enter
  },
  data() {
    return {
      calendarOptions: {
        plugins: [dayGridPlugin, interactionPlugin],
        initialView: "dayGridMonth",
        dateClick: this.handleDateClick,
        eventBackgroundColor: "#eee",
        eventBorderColor: "#eee",
        eventTextColor: "#aaa",
        eventDidMount: function (info) {
          tippy(info.el, {
            content: info.event.extendedProps.description,
            animateFill: true,
            plugins: [animateFill],
            theme: "material",
          });
        },
        eventClick: function (info) {
          th.$router.push(info.event.extendedProps.route);
        },
      },
    };
  },
  methods: {
    handleDateClick: function (arg) {
      this.$router.push("/Date/" + arg.dateStr);
    },
  },
  created() {
    th = this;
    let todos = JSON.parse(localStorage.getItem("todos"));
    if (todos !== "" && todos !== null) {
      for (var i = 0; i < todos.length; i++) {
        todos[i].route = "/Todo/" + i;
      }
      this.calendarOptions["events"] = todos;
    }

  },
};
</script>
<style>
* {
  font-family: "Quicksand";
}
.fc-daygrid-day.fc-day-today {
  background-color: #f9f9f9 !important;
  font-weight: 800;
}
.fc-daygrid-event {
  padding: 5px;
  cursor: pointer;
}
.fc-toolbar.fc-header-toolbar {
  margin: 1.5em;
}
</style>