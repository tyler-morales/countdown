<template>
  <div class="dropDownContainer">
    <div class="selection" :class="{ opened: opened }" @click="toggle">
      <span class="selectionText">
        {{ selected.label }}
        <span class="downArrow"></span>
      </span>
    </div>
    <transition name="grow">
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
}
/*  Box with current selection e.g. <select/>  */
.dropDownContainer .selection {
  display: inline-block;
  position: relative;
  height: 32px;
  padding-left: 10px;
  padding-right: 10px;
  background-color: #e3e3e3; /* Light Grey */
  border: none;
  border-radius: 5px 5px 0px 0px;
  border-bottom: 1px solid #5f6161;
  cursor: pointer;
}
/* Active style when list is open */
.dropDownContainer .selection.opened {
  border-bottom: 2px solid #4a9fff; /*  Sky Blue  */
}
.selection span.selectionText {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  height: 100%;
}

/* DownArrow in selection */
.selection span.downArrow {
  display: block;
  position: relative;
  width: 0;
  height: 0;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: 5px solid #5f6161;
  margin-left: 20px;
  transition: all 0.1s linear;
}

/* Down arrow when opened */
.selection.opened span.downArrow {
  border-top: 5px solid #4a9fff; /*  Sky Blue  */
  transform: rotate(180deg);
  /*   bottom: 3px; */
}
/* List of options */
.dropDownContainer .options {
  display: inline-block;
  position: absolute;
  width: 100%;
  top: 34px;
  background-color: #ffffff;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.3);
  border-radius: 0 0 5px 5px;
  padding-top: 8px;
  padding-bottom: 8px;
}
/* Individual Option */
.dropDownContainer .options span {
  display: block;
  position: relative;
  cursor: pointer;
  padding: 7px;
}

/* Individual Option Hover */
.dropDownContainer .options span:hover {
  background-color: #e3e3e3;
}
/* Transition animation when options open/close */
.grow-enter,
.grow-leave-to {
  transform: scaleY(0);
  transform-origin: top;
  /*   opacity: 0; */
}
.grow-enter-active,
.grow-leave-active {
  transition: transform 0.4s;
  transform-origin: top;
  /*   transition: opacity .3s; */
}
</style>
