<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <div class="board-row" v-for="(row, index) in board" :key="index">
      <Square
        v-for="square in row"
        :key="square"
        :value="squares[square]"
        @click="handleClick(square)"
      />
    </div>
  </div>
</template>

<script>
import Square from "./Square.vue";

export default {
  components: {
    Square,
  },
  props: ["squares"],
  data() {
    return {
      board: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
      ],
    };
  },
  methods: {
    handleClick(i) {
      this.$emit("click", i);
    },
  },
};
</script>

