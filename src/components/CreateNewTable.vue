<template>
  <div>
    <a-modal :visible="isCreateTableModalOpen" title="Create New Table" @ok="handleOk" @cancel="handleCancel">
      <a-checkbox
        v-for="(option, index) in connectionOptions"
        :key="index"
        @change="selectedOption"
        class="options-checkbox"
      >
        {{option}}
      </a-checkbox>
    </a-modal>
  </div>
</template>

<script>
import { Modal, Checkbox } from "ant-design-vue";
import Vue from "vue";
Modal.install(Vue);
// const FormItem = Form.Item;

export default {
  name: "CreateNewTable",
  data() {
    return {
      connectionOptions: ["Sql", "No Sql"],
    };
  },
  components: {
    "a-modal": Modal,
    "a-checkbox": Checkbox,
  },
  props: {
    isCreateTableModalOpen: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleOk(e) {
      console.log(e);
    },
    handleCancel(e) {
      console.log(e);
    },
    handleSubmit() {
      console.log();
    },
    selectedOption() {},
  },
};
</script>

<style lang="css" >
.ant-checkbox-group-item {
    display: block;
    margin-right: 0;
}
</style>
