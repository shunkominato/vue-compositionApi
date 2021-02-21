<template>
  <div class="home">
    <h1>アンケートフォーム</h1>
    <div class="questionary__form">
      <p>{{ errorState.name }}</p>
      <div v-if='errorState.name'>
        <label>{{ errorState.name }}</label>
      </div>
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

      <div v-if='errorState.email'>
        <label>{{ errorState.email }}</label>
      </div>
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

      <div v-if='errorState.demand'>
        <label>{{ errorState.demand }}</label>
      </div>
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
        @click="send(state.email)"
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
type FormStateType = 'name' | 'age' | 'email' | 'gender' | 'demand';
type FormState = {
  [key in FormStateType]?: string;
};

// interface ErrorState {
//   name: string;
//   email: string;
//   demand: string;
// }
type ErrorType = 'name' | 'email' | 'demand';
type ErrorState = {
  [key in ErrorType]?: string;
};

interface Options {
  labal: string;
  value: string;
}

function useValidate() {
  const errorState = reactive<ErrorState>({
    name: '',
    email: '',
    demand: '',
  });
  function validate(type: ErrorType, value: string) {
    const m: string = (() => {
      console.log(type);
      console.log(value);
      switch (type) {
        case 'name':
          return !value ? '必須項目です' : '';
        case 'email':
          return !value ? '必須項目です' : '';
        case 'demand':
          return !value ? '必須項目です' : '';
        default:
          // ((a: never) => { throw new Error(a); })(type);
          return '';
      }
    })();
    errorState[type] = m;
  }

  function getMessage(type: ErrorType) {
    return errorState[type] || '';
  }

  return { validate, getMessage, errorState };
}

function useInputForm(state: State) {
  // const state = reactive<FormState>({});
  const onChangeForm = (value: string, type: string) => {
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

  return { onChangeForm, state };
}

function useSendForm(state: State) {
  const send = () => {
    console.log(state);
    const { validate, getMessage } = useValidate();
    validate('name', state.name);
    const aa = getMessage('name');
    console.log(aa);
  };

  return { send };
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
    const state = reactive<State>({
      name: '',
      age: '1',
      email: '',
      gender: '1',
      demand: '',
    });
    const { onChangeForm } = useInputForm(state);
    const { send } = useSendForm(state);
    const { validate, getMessage, errorState } = useValidate();
    const genderOptions = [
      { label: '男', value: '1' },
      { label: '女', value: '2' },
    ];

    // const errorState = reactive<ErrorState>({
    //   name: '',
    //   email: '',
    //   demand: '',
    // });

    // const extractErrorMessage = (obj: any): void => {
    //   console.log('ext');

    //   obj.map((o: any) => o.key === );
    // };

    // const setErrorMessages = (errorMessages: ErrorState): void => {
    //   errorState.name = errorMessages.name;
    //   errorState.email = errorMessages.email;
    //   errorState.demand = errorMessages.demand;
    // };

    return {
      state,
      // errorState,
      onChangeForm,
      genderOptions,
      // sendForm,
      validate,
      getMessage,
      errorState,
      send,
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
