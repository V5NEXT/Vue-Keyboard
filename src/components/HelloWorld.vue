<template>
  <div :class="keyboardClass"></div>
</template>

<script>
import Keyboard from "simple-keyboard";
import "simple-keyboard/build/css/index.css";
import SimpleKeyboardLayouts from "simple-keyboard-layouts";
// import SimpleKeyboardLayouts from "../lib/components/Layouts";
// import layout from "simple-keyboard-layouts/build/layouts/german";

export default {
  name: "SimpleKeyboard",
  props: {
    keyboardClass: {
      default: "simple-keyboard-layouts",
      type: String,
    },
    input: {
      type: String,
    },
  },
  data: () => ({
    keyboard: null,
  }),
  mounted() {
    this.keyboard = new Keyboard(this.keyboardClass, {
      onChange: this.onChange,
      onKeyPress: this.onKeyPress,
    });
  },
  methods: {
    onChange(input) {
      this.$emit("onChange", input);
    },
    onKeyPress(button) {
      this.$emit("onKeyPress", button);

      /**
       * If you want to handle the shift and caps lock buttons
       */
      if (button === "{shift}" || button === "{lock}") this.handleLanguages();
    },
    handleShift() {
      let currentLayout = this.keyboard.options.layoutName;
      let shiftToggle = currentLayout === "default" ? "shift" : "default";

      this.keyboard.setOptions({
        layoutName: shiftToggle,
      });
    },
    handleLanguages() {
      let languageToggle =
        this.keyboard.options.layoutName === "english" ? "german" : "english";
      let SimpleKeyboardLayouts = new SimpleKeyboardLayouts();
      const layout = this.SimpleKeyboardLayouts().get(languageToggle);
      this.keyboard.setOptions({ layout });
    },
  },
  watch: {
    input(input) {
      this.keyboard.setInput(input);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
