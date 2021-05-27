<template>
  <div>
    <a-modal
      :visible="isModalOpen"
      title="Select the Datasource"
      okText="Continue"
      @ok="handleOk"
      @cancel="handleCancel"
    >
      <a-radio-group v-model="value" @change="onChange">
        <a-radio
          :style="radioStyle"
          v-for="(option, index) in connectionOptions"
          :key="index"
          :value="index"
        >
          <a-icon :type="option.iconType" class="connection-icon" />
          <span>{{ option.title }}</span>
        </a-radio>
      </a-radio-group>
    </a-modal>
    <SelectDatabase :isSelectDatabseModalOpen="isSelectDatabaseModalSelected" />
    <CreateNewTable :isCreateTableModalOpen="isCreateNewTableChosen" />
    <SelectCollection :isSelectCollectionModalOpen="isSelectCollectionChosen" />
  </div>
</template>

<script>
import { Modal, Icon, Radio } from "ant-design-vue";
import CreateNewTable from "./CreateNewTable";
import SelectCollection from "./SelectCollection";
import SelectDatabase from "./SelectDatabase";
import Vue from "vue";
Modal.install(Vue);
// const FormItem = Form.Item;
const radioGroup = Radio.Group;
export default {
  name: "CreateConnectionModal",
  data() {
    return {
      value: 0,
      radioStyle: {
        display: "block",
        height: "30px",
        lineHeight: "30px",
      },
      connectionOptions: [
        {
          title: "Database",
          iconType: "database",
        },
        {
          title: "Web Service",
          iconType: "code-sandbox",
        },
        {
          title: "Data Feed",
          iconType: "cloud-download",
        },
        {
          title: "File",
          iconType: "file",
        },
      ],
      // "Database", "Web Service", "Data Feed", "File"
      isSelectCollectionChosen: false,
      isCreateNewTableChosen: false,
      isSelectDatabaseModalSelected: false,
      selectedOption: "",
    };
  },
  components: {
    "a-modal": Modal,
    "a-icon": Icon,
    "a-radio": Radio,
    "a-radio-group": radioGroup,
    CreateNewTable,
    SelectCollection,
    SelectDatabase,
  },
  props: {
    isModalOpen: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleOk() {
      // this.isModalOpen = false;
      this.isSelectDatabaseModalSelected = true;
      this.handleCancel();
    },
    handleCancel() {
      this.$emit("cancelModal");
    },
    setSelectedOption(e) {
      this.selectedOption = e;
    },
    onChange(e) {
      console.log("radio checked", e.target.value);
    },
  },
};
</script>

<style lang="css">
ul {
  list-style-type: none;
}
.connection-icon {
  margin-right: 8px;
}
.ant-checkbox-group-item {
  display: block;
  margin-right: 0;
}
</style>
