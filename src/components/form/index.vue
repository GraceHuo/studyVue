<template>
  <div>
    <KForm :model="userInfo" :rules="rules" ref="loginForm">
      <KFormItem label="User Name" prop="username">
        <KInput
          v-model="userInfo.username"
          placeholder="Please enter a username"
        ></KInput>
      </KFormItem>
      <KFormItem label="Password" prop="password">
        <KInput type="password" v-model="userInfo.password"></KInput>
      </KFormItem>
      <KFormItem>
        <button @click="login">Login</button>
      </KFormItem>
    </KForm>
    {{ userInfo.username }}
  </div>
</template>

<script>
import KInput from "@/components/form/KInput.vue";
import KFormItem from "@/components/form/KFormItem.vue";
import KForm from "@/components/form/KForm.vue";
import Notice from "@/components/Notice.vue";
export default {
  data() {
    return {
      userInfo: {
        usename: "",
        password: ""
      },
      rules: {
        username: [{ required: true, message: "Please enter username" }],
        password: [{ required: true, message: "Please enter password" }]
      }
    };
  },
  components: {
    KInput,
    KFormItem,
    KForm
  },
  methods: {
    login() {
      this.$refs["loginForm"].validate(valid => {
        const notice = this.$create(Notice, {
          title: "Alert",
          message: valid ? "Success" : "Fail"
        });
        notice.show();
      });
    }
  }
};
</script>

<style scoped></style>
