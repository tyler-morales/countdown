<template>
  <div class="dropDownContainer">
    <div class="selection" :class="{ opened: opened }" @click="toggle">
      <span class="selectionText">
        {{ selected.label }}
        <span class="downArrow"></span>
      </span>
    </div>
    <transition name="slide">
      <div class="options" v-if="opened">
        <span
          v-for="(option, index) in choices"
          :key="index"
          @click="makeSelection(option), emitSort(option.name)"
        >
          {{ option.label }}
        </span>
      </div>
    </transition>
  </div>
</template>

<script>
import EventBus from '@/components/EventBus'

export default {
  props: {
    choices: Array,
    menuLabel: String
  },
  data: function() {
    return {
      selected: this.choices[0],
      opened: false,
      sortResult: ''
    }
  },
  methods: {
    toggle: function() {
      this.opened = !this.opened
    },
    makeSelection: function(selected) {
      this.selected = selected
      this.opened = false
    },
    emitSort(option) {
      this.sortResult = option
      EventBus.$emit('sort-catagories', this.sortResult)
    }
  }
}
</script>

<style lang="scss" scoped>
/* Component Wrapper */
.dropDownContainer {
  display: inline-flex;
  flex-direction: column;
  position: relative;

  @include breakpoint(sm) {
    width: 100%;
  }
}

/*  Box with current selection e.g. <select/>  */
.dropDownContainer .selection {
  position: relative;
  color: #fff;
  border-radius: 20px;
  cursor: pointer;
  padding: 10px 30px;
  background-color: var(--color-primary);

  transition: all 0.2s;

  &:hover {
    transform: translateY(-3px);
    box-shadow: var(--shadow-base);
  }
}

.selection span.selectionText {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  font-family: var(--header-text);
  border-radius: 20px;
  font-size: 24px;
  transition: all 0.2s;
}

/* DownArrow in selection */
.selection span.downArrow {
  display: block;
  position: relative;
  width: 0;
  height: 0;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: 5px solid white;
  margin-left: 20px;
  transition: all 0.1s linear;
}

/* Down arrow when opened */
.selection.opened span.downArrow {
  transform: rotate(180deg);
}
/* List of options */
.dropDownContainer .options {
  display: inline-block;
  position: absolute;
  width: 100%;
  top: 54px;
  background-color: #ffffff;
  box-shadow: var(--shadow-base);
  border-radius: 20px;
  padding: 8px;
}
/* Individual Option */
.dropDownContainer .options span {
  display: block;
  position: relative;
  cursor: pointer;
  padding: 8px 10px;
  margin: 5px;
  border-radius: 10px;
}

/* Individual Option Hover */
.dropDownContainer .options span:hover {
  background-color: var(--color-primary-light);
}
/* Enter and leave animations can use different */
/* durations and timing functions.              */
.slide-enter-active,
.slide-leave-active {
  transition: all 0.2s;
}
.slide-enter, .slide-leave-to
/* .slide-leave-active below version 2.1.8 */ {
  transform: translateY(10px);
  opacity: 0;
}
</style>
