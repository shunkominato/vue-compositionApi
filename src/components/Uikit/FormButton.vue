<template>
  <button :class="className" data-testid="test-btn" @click="$emit('click')">{{ btnLabel }}</button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    btnLabel: {
      type: String,
    },
    className: {
      type: String,
    },
  },
});
</script>

<style scoped lang="scss">
.questionary-button {
  width: 60px;
  height: 30px;
  padding: 8px;
  border-radius: 8px;
}
</style>
