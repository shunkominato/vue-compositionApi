<template>
  <div :class="divClassName">
    <template v-for="(option, index) in options" :key="index" >
      <label :class="labelClassName">
        <input
          v-model="state.selectedItem"
          type="radio"
          :class="radioClassName"
          :name="radioName"
          :value="option.value"
          :disabled="disabled"
          @change="onChange($event)"
        />
        <span :class="radioTextClassName">
          {{ option.label }}
        </span>
      </label>
    </template>
  </div>
</template>

<script lang='ts'>
import { computed, defineComponent, reactive } from 'vue';

interface State {
  selectedItem: string;
}

export default defineComponent({
  props: {
    labelClassName: {
      type: String,
    },
    value: {
      type: String,
    },
    radioClassName: {
      type: String,
    },
    radioName: {
      type: String,
    },
    options: {
      type: [],
    },
    disabled: {
      type: Boolean,
    },
  },
  setup(props, context) {
    console.log('radio');
    console.log(props);
    const state = reactive<State>({
      selectedItem: '',
    });

    const onChange = (e: any, a: string) => {
      context.emit('onChange', e.target.value);
    };

    return {
      state,
      onChange,
    };
    // selectedItem:computed({
    //   get: () => props.value,
    //   set: (value: string) => context.emit('onChange', value)
    // })
  },
});
</script>
