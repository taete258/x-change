<template>
  <div>
    <h1>app</h1>
    <span>Count1 : {{ count1 }}</span>
    <br />
    <span>Count2 : {{ count2 }}</span>
    <br />

    <button @click="onInCrease">Add 1 to Count 1</button>
    <button @click="onInCrease2">Add 1 to Count 2</button>

    <hr />
    <span>Account : {{ state.account }}</span
    ><br />
    <button @click="onClearAccount">Clear</button>
    <hr />

    <LoginForm :title="state.account" @submitLogin="onHandleSubmit" />
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, ref, onMounted } from "vue";
import LoginForm from "./components/LoginForm.vue";
import { AccountType } from "./type/accountType.type";

const defaultAccount = { username: "", password: "" };
export default defineComponent({
  components: {
    LoginForm,
  },
  setup() {
    let count1 = 1;
    const count2 = ref<number>(2);
    const state = reactive({
      account: { username: "taete258", password: "123456" },
    });

    onMounted(() => {
      setInterval(onInCrease2, 1000);
    });

    const onInCrease = () => {
      count1 += 1;
    };
    const onInCrease2 = () => {
      count2.value += 1;
    };
    const onClearAccount = () => {
      state.account = defaultAccount;
    };

    const onHandleSubmit = (acc: AccountType) => {
      alert(JSON.stringify(acc));
    };
    return {
      count1,
      count2,
      state,
      onInCrease,
      onInCrease2,
      onClearAccount,
      onHandleSubmit,
    };
  },
});
</script>
