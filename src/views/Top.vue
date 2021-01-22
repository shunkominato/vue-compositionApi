<template>
  <div class="home">
    <h1>アンケートフォーム</h1>
    <div class="questionary__form">
      <TextInput
        placeholder='名前'
        :value="state.name"
        type='text'
        className="questionary__input"
        :maxlength="10"
        @onChange="onChangeForm($event,'name')"
      />

      <TextInput
        placeholder='年齢'
        :value="state.age"
        type='number'
        className="questionary__input"
        :maxlength="2"
        @onChange="onChangeForm($event,'age')"
       />

      <TextInput
        placeholder='メールアドレス'
        :value="state.email"
        type='email'
        className="questionary__input"
        :maxlength="2"
        @onChange="onChangeForm($event,'email')"
      />

      <RadioButton
        labelClassName="questionary-label"
        radioClassName="questionary-radio"
        radioName="gender"
        :options="genderOptions"
        @onChange="onChangeForm($event,'gender')"
      />

      <TextAreaInput
        row=5
        col=30
        placeholder="要望"
        :value="state.demand"
        className="questionary__textarea"
        @onChange="onChangeForm($event,'demand')"
      />

      <FormButton
        btnLabel="送信"
        className='questionary-button'
        @click="sendForm()"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue';
import TextInput from '../components/Uikit/TextInput.vue';
import TextAreaInput from '../components/Uikit/TextAreaInput.vue';
import RadioButton from '../components/Uikit/RadioButton.vue';
import FormButton from '../components/Uikit/FormButton.vue';

interface State {
  name: string;
  age: string;
  email: string;
  gender: string;
  demand: string;
}

interface ErrorState {
  name: string;
  age: string;
  email: string;
  gender: string;
  demand: string;
}

interface Options {
  labal: string;
  value: string;
}

export default defineComponent({
  name: 'Top',
  components: {
    TextInput,
    RadioButton,
    FormButton,
    TextAreaInput,
  },
  setup() {
    const genderOptions = [
      { label: '男', value: '1' },
      { label: '女', value: '2' },
    ];
    console.log('top');
    const state = reactive<State>({
      name: '',
      age: '1',
      email: '',
      gender: '1',
      demand: '',
    });

    const errorState = reactive<ErrorState>({
      name: '',
      age: '',
      email: '',
      gender: '',
      demand: '',
    });

    const onChangeForm = (value: string, type: string) => {
      console.log('onchange');
      console.log(value);
      console.log(type);
      switch (type) {
        case 'name': {
          state.name = value;
          break;
        }
        case 'age': {
          state.age = value;
          break;
        }
        case 'email': {
          state.email = value;
          break;
        }
        case 'gender': {
          state.gender = value;
          break;
        }
        case 'demand': {
          state.demand = value;
          break;
        }
        default: {
          console.log('err');
          break;
        }
      }
    };

    const getError = (formValue: State, errorMessage: ErrorState) => {
      console.log(formValue, errorMessage);

      const {
        name, age, email, gender, demand,
      } = formValue;

      name ? 
    };

    const sendForm = () => {
      getError(state, errorState);
    };

    return {
      state,
      onChangeForm,
      genderOptions,
      sendForm,
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
}
</style>
