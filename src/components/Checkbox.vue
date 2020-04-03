<template>
  <label htmlFor="name.toLowerCase()" class="container">
    <input
      v-model="state"
      tabIndex="-1"
      type="checkbox"
      id="name.toLowerCase()"
      name="name.toLowerCase()"
      @click="handleClick"
      @keydown="handleSpace"
      :disabled="!isEnabled"
    />
    <span
      @keydown="handleSpace"
      :tabIndex="isEnabled ? '1' : '-1'"
      :class="['tabShadow', state ? 'tabMarked' : 'tabUnmarked']"
    >
    </span>
    <span
      tabIndex="-1"
      class="checkmark"
      :class="[isEnabled ? 'checkmarkEnabled' : 'checkmarkDisabled']"
    >
    </span>
    <transition name="wave">
      <span
        v-if="state"
        tabIndex="-1"
        :class="['shadowArea', 'shadowAreaMarked']"
      >
      </span>
    </transition>
    <transition name="wave-gray">
      <span
        v-if="!state"
        tabIndex="-1"
        :class="['shadowArea', 'shadowAreaUnmarked']"
      >
      </span>
    </transition>
    {{ name }}
  </label>
</template>

<script>
export default {
  name: "Checkbox",
  props: {
    name: String,
    isChecked: Boolean,
    isEnabled: Boolean,
    callback: Function
  },
  data() {
    return {
      state: this.isChecked
    };
  },
  methods: {
    handleClick() {
      this.callback();
    },
    handleSpace(event) {
      console.log("event", event);
      if (this.isEnabled && event.keyCode === 32) {
        // 32 - space
        this.state = !this.state;
        this.callback();
      }
    }
  }
};
</script>

<style scoped>
.container {
  display: block;
  margin: 30px 0 12px 10px;
  position: relative;
  padding-left: 35px;
  cursor: pointer;
  width: fit-content;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0px;
  left: 1px;
  height: 18px;
  width: 18px;
  background-color: inherit;
  border-radius: 4px;
  border: solid;
  z-index: 1;
}

.checkmarkDisabled {
  border-color: #9e9e9e;
}
.checkmarkEnabled {
  border-color: #666666;
}

/* When the checkbox is checked, add a blue or gray */
.container input:checked ~ .checkmarkEnabled {
  background-color: #246bf6;
  border-color: #246bf6;
}

input:checked ~ .checkmarkDisabled {
  background-color: #9e9e9e;
}

/* Create a shadow area around checkbox */
.shadowArea {
  position: absolute;
  top: -11px;
  left: -10px;
  opacity: 0.1;
  height: 45px;
  width: 45px;
  border-radius: 50%;
  z-index: 0;
}

.tabShadow {
  position: absolute;
  top: -11px;
  left: -10px;
  height: 45px;
  width: 45px;
  border-radius: 50%;
  z-index: -1;
}

/* Switch area color */
.shadowAreaMarked {
  background-color: #b1d1dd;
}
.shadowAreaUnmarked {
  background-color: #c1b8b8;
}

/* On mouse-over, show area*/
.container input ~ .shadowArea:hover {
  opacity: 0.3;
}

.checkmark:hover ~ .shadowArea {
  opacity: 0.3;
}

/* On focus, show area */
.container input ~ .tabMarked:focus {
  background-color: #b1d1dd;
  opacity: 0.6;
  /* outline: none; */
}

.container input ~ .tabUnmarked:focus {
  background-color: #c1b8b8;
  opacity: 0.6;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 5px;
  top: 0px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}

/* Styles for animation */
.wave-enter-active {
  animation: bounce-in 0.3s;
  animation-timing-function: ease-in-out;
}
.eave-enter-to {
  display: none;
}

.wave-leave-active {
  display: none;
}

.wave-gray-enter-active {
  animation: bounce-in 0.3s;
  animation-timing-function: ease-in-out;
}

@keyframes bounce-in {
  from {
    transform: scale(0.1);
    opacity: 1;
  }
  to {
    transform: scale(1);
    opacity: 0.2;
  }
}
</style>
