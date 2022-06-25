<template>
  <div>
    <div>Login form</div>

    <form>
      <label for="username">Username:</label>
      <input
        type="text"
        name="username"
        id="username"
        v-model="formStates.account.username"
      /><br />

      <label for="password">Password:</label>
      <input
        type="text"
        name="password"
        id="password"
        v-model="formStates.account.password"
      /><br />

      <br />
      <button type="button" @click="onSubmit">Submit</button>
      <button
        type="button"
        @click="onClear"
        v-if="formStates.account.username && formStates.account.password"
      >
        Clear
      </button>
    </form>
  </div>
</template>
<script lang="ts">
import { AccountType } from "../type/accountType.type";
import { defineComponent, reactive, onMounted } from "vue";

interface LoginState {
  account: AccountType;
}
export default defineComponent({
  props: ["title"],
  emits: ["submitLogin"],
  setup(props, { emit }) {
    const formStates = reactive<LoginState>({
      account: {
        username: props.title.username,
        password: props.title.password,
      },
    });

    onMounted(() => {
      console.log(props.title);
    });

    const onSubmit = () => {
      emit("submitLogin", formStates.account);
    };
    const onClear = () => {
      formStates.account = { username: "", password: "" };
    };
    return {
      formStates,
      onSubmit,
      onClear,
    };
  },
});
</script>
