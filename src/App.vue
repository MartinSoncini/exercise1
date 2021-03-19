<template>
  <div id="app">
    <at-header></at-header>
    <at-task-handler></at-task-handler>
    <at-footer></at-footer>
  </div>
</template>

<script>
import AtHeader from "./components/AtHeader";
import AtFooter from "./components/AtFooter";
import AtTaskHandler from "./components/AtTaskHandler";
export default {
  name: "App",
  components: {
    AtFooter,
    AtHeader,
    AtTaskHandler
  }
};
</script>
