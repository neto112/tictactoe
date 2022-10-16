<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <button class="square" @click="setValue">
      {{ value }}
    </button>
  </div>
</template>

<script>

export default {
  props: ['value'],
  methods: {
    setValue() {
      this.$emit('click');
    }
  }
};
</script>

