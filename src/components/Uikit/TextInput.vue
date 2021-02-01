<template>
    <label>
      <input
        :placeholder="placeholder"
        :value="value"
        :type="type"
        :class="className"
        :maxlength="maxlength"
        @change="onChange"/>
    </label>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    placeholder: {
      type: String,
    },
    value: {
      type: String,
    },
    type: {
      type: String,
    },
    className: {
      type: String,
    },
    maxlength: {
      type: Number,
    },
  },

  setup(props, context) {
    const onChange = (e: Event) => {
      if (e.target instanceof HTMLInputElement) {
        console.log(e.target.value);
        context.emit('onChange', e.target.value);
      }
    };

    return {
      onChange,
    };
  },
});
</script>

<style scoped lang="scss">
.questionary__form{
    width: 400px;
    margin: auto;
}

.questionary__input{
  width: 70%;
  padding: 8px;
  border-radius: 4px;
  margin: 16px;
}
</style>
