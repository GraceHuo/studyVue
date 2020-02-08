<template>
  <div>
    <!-- lable -->
    <label v-if="label">{{ label }}</label>
    <slot></slot>
    <!-- validation -->
    <p v-if="error">{{ error }}</p>
  </div>
</template>

<script>
import Schema from "async-validator";

export default {
  inject: ["form"],
  data() {
    return {
      error: ""
    };
  },
  props: {
    label: {
      type: String,
      default: ""
    },
    prop: {
      type: String
    }
  },
  mounted() {
    this.$on("validate", () => {
      this.validate();
    });
  },
  methods: {
    validate() {
      const rules = this.form.rules[this.prop];
      const value = this.form.model[this.prop];
      //校验描述对象
      const desc = {
        [this.prop]: rules
      };
      //创建Schema实例
      const schema = new Schema(desc);
      return schema.validate(
        {
          [this.prop]: value
        },
        errors => {
          if (errors) {
            this.error = errors[0].message;
          } else {
            this.error = "";
          }
        }
      );
    }
  }
};
</script>

<style scoped></style>
