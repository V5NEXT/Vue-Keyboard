<template>
  <div id="app">
    <select @change="onChangeMethod($event)">
      <option value="german">German</option>
      <option value="english">English</option>
      <option value="french">French</option>
      <option value="spanish">Spanish</option>
    </select>
    <input
      :value="input"
      class="input"
      @input="onInputChange"
      placeholder="Tap on the virtual keyboard to start"
    />
    <SimpleKeyboard
      @onChange="onChange"
      @onKeyPress="onKeyPress"
      :input="input"
    />
  </div>
</template>

<script>
import SimpleKeyboard from "./components/HelloWorld.vue";
import "./App.css";

export default {
  name: "App",
  components: {
    SimpleKeyboard,
  },
  data: () => ({
    input: "",
  }),
  methods: {
    onChange(input) {
      this.input = input;
    },
    onKeyPress(button) {
      console.log("button", button);
    },
    onInputChange(input) {
      this.input = input.target.value;
    },
    onChangeMethod(event) {
      console.log("Selected Language", event);
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
