<template>
  <v-avatar size="23px" :class="statusClass">
    <font-awesome-icon :class="statusIconClass" :icon="statusIcon" size="lg"/>
  </v-avatar>
</template>

<script>
export default {
  data: () => ({}),

  props: ["status"],

  computed: {
    statusClass: function() {
      var status = this.status;
      if (status === "Initializing") {
        return ["green", "darken-2"];
      } else if (status === "InitializationError") {
        return ["red", "darken-3"];
      } else if (status === "Starting") {
        return ["green", "darken-2"];
      } else if (status === "Started") {
        return ["green", "darken-2"];
      } else if (status === "StartedWithErrors") {
        return ["red", "darken-3"];
      } else if (status === "Stopping") {
        return ["grey", "darken-3"];
      } else if (status === "Stopped") {
        return ["grey", "darken-3"];
      } else if (status === "StoppedWithErrors") {
        return ["red", "darken-3"];
      } else if (status === "Terminating") {
        return ["grey", "darken-3"];
      } else if (status === "Terminated") {
        return ["grey", "darken-3"];
      } else if (status === "LifecycleError") {
        return ["red", "darken-3"];
      } else {
        return ["grey", "darken-3"];
      }
    },
    statusIcon: function() {
      var status = this.status;
      if (status === "Initializing") {
        return "cog";
      } else if (status === "InitializationError") {
        return "exclamation-circle";
      } else if (status === "Starting") {
        return "cog";
      } else if (status === "Started") {
        return "cog";
      } else if (status === "StartedWithErrors") {
        return "exclamation-circle";
      } else if (status === "Stopping") {
        return "cog";
      } else if (status === "Stopped") {
        return "stop";
      } else if (status === "StoppedWithErrors") {
        return "fa-exclamation-circle";
      } else if (status === "Terminating") {
        return "times";
      } else if (status === "Terminated") {
        return "times";
      } else if (status === "LifecycleError") {
        return "bolt";
      } else {
        return "question";
      }
    },
    statusIconClass: function() {
      var status = this.status;
      if (status === "Initializing") {
        return ["fa-spin", "green--text"];
      } else if (status === "InitializationError") {
        return ["red--text", "text--lighten-4"];
      } else if (status === "Starting") {
        return ["fa-spin", "green--text"];
      } else if (status === "Started") {
        return ["green--text", "text--lighten-3"];
      } else if (status === "StartedWithErrors") {
        return ["yellow--text", "text--lighten-1"];
      } else if (status === "Stopping") {
        return ["grey--text", "text--lighten-4"];
      } else if (status === "Stopped") {
        return ["grey--text", "text--lighten-4"];
      } else if (status === "StoppedWithErrors") {
        return ["red--text", "text--lighten-4"];
      } else if (status === "Terminating") {
        return ["grey--text", "text--lighten-4"];
      } else if (status === "Terminated") {
        return ["grey--text", "text--lighten-4"];
      } else if (status === "LifecycleError") {
        return ["red--text", "text--lighten-4"];
      } else {
        return ["grey--text", "text--lighten-4"];
      }
    }
  }
};
</script>

<style scoped>
</style>
