<template>
  <div class="home">
    <h1>アンケートフォーム</h1>
    <div class="questionary__form">
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
  email: string;
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

    const state = reactive<State>({
      name: '',
      age: '1',
      email: '',
      gender: '1',
      demand: '',
    });

    const errorState = reactive<ErrorState>({
      name: '',
      email: '',
      demand: '',
    });

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

    // const extractErrorMessage = (obj: any): void => {
    //   console.log('ext');

    //   obj.map((o: any) => o.key === );
    // };

    const setErrorMessages = (errorMessages: ErrorState): void => {
      errorState.name = errorMessages.name;
      errorState.email = errorMessages.email;
      errorState.demand = errorMessages.demand;
    };

    const getError = (formValue: State, errorMessages: ErrorState): ErrorState => {
      const {
        name, age, email, gender, demand,
      } = formValue;

      let {
        name: nameError, email: emailError, demand: demandError,
      } = errorMessages;

      nameError = !name ? '必須項目です' : '';
      emailError = !email || !email.match(/^[A-Za-z0-9]{1}[A-Za-z0-9_.-]*@{1}[A-Za-z0-9_.-]{1,}\.[A-Za-z0-9]{1,}$/) ? '形式が違います' : '';
      demandError = !demand ? '必須項目です' : '';

      return { name: nameError, email: emailError, demand: demandError };
    };

    const sendForm = (): void => {
      const errorMessages = getError(state, errorState);
      setErrorMessages(errorMessages);
    };

    return {
      state,
      errorState,
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
