<template>
    <label>
      <textarea
        :rows="rows"
        :cols="cols"
        :placeholder="placeholder"
        :value="value"
        :class="className"
        :maxlength="maxlength"
        @change="onChange"
      />
    </label>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    row: {
      type: String,
    },
    col: {
      type: String,
    },
    placeholder: {
      type: String,
    },
    value: {
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
    console.log('asd');
    console.log(props);
    console.log(context);
    const onChange = (e: any) => {
      context.emit('onChange', e.target.value);
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

.questionary__textarea {
  width: 70%;
  margin: auto;
}
</style>
