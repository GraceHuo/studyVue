<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "KForm",
  componentName: "KForm",
  provide() {
    return {
      form: this
    };
  },
  props: {
    model: {
      type: Object,
      required: true
    },
    rules: {
      type: Object
    }
  },
  created() {
    this.fields = [];
    this.$on("kkb.form.addField", item => {
      this.fields.push(item);
    });
    // todo: remove
  },
  methods: {
    validate(cb) {
      // 获取所有孩子，KFormItem [resultPromise]
      const tasks = this.fields.map(item => item.validate());
      // 统一处理所有Promise结果
      Promise.all(tasks)
        .then(() => {
          cb(true);
        })
        .catch(() => {
          cb(false);
        });
    }
  }
};
</script>

<style scoped></style>
