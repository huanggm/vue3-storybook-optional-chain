<template>
  <button type="button" :class="classes" @click="onClick" :style="style">{{ label }} - {{test?.name}}</button>
</template>

<script lang="ts">
import './button.css';
import { reactive, computed } from 'vue';

interface Test {
  name?: string;
}

export default {
  name: 'my-button',

  props: {
    label: {
      type: String,
      required: true,
    },
    primary: {
      type: Boolean,
      default: false,
    },
    size: {
      type: String,
      validator: function (value: any) {
        return ['small', 'medium', 'large'].indexOf(value) !== -1;
      },
    },
    backgroundColor: {
      type: String,
    },
  },

  emits: ['click'],

  setup(props: any, { emit }: any) {
    props = reactive(props);

    const test: Test = {
        name: 'hello'
    }

    return {
      test,
      classes: computed(() => ({
        'storybook-button': true,
        'storybook-button--primary': props.primary,
        'storybook-button--secondary': !props.primary,
        [`storybook-button--${props.size || 'medium'}`]: true,
      })),
      style: computed(() => ({
        backgroundColor: props.backgroundColor,
      })),
      onClick() {
        emit('click');
      }
    }
  },
};
</script>
