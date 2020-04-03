<template>
  <div id="app" class="container">
    <h1>Checkboxes</h1>
    <Checkbox
      class="target"
      name="Target"
      :isChecked="targetState"
      :isEnabled="targetEnabled"
      :callback="targetCheckboxEvent"
    />
    <Checkbox
      name="Enable target"
      :isChecked="targetEnabled"
      :isEnabled="true"
      :callback="changeEnable"
    />
    <h2>Checked</h2>
    <Checkbox name="Enabled Checked" :isChecked="true" :isEnabled="true" />
    <Checkbox name="Disabled Checked" :isChecked="true" :isEnabled="false" />
    <h2>Unchecked</h2>
    <Checkbox name="Enabled Unchecked" :isChecked="false" :isEnabled="true" />
    <Checkbox name="Disabled Unchecked" :isChecked="false" :isEnabled="false" />
  </div>
</template>

<script>
import Checkbox from "./components/Checkbox";

export default {
  name: "App",
  components: {
    Checkbox
  },
  methods: {
    changeEnable() {
      this.targetEnabled = !this.targetEnabled;
    },
    targetCheckboxEvent() {
      console.log("Target checkox event callback example");
    }
  },
  data() {
    return {
      targetState: false,
      targetEnabled: true
    };
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
