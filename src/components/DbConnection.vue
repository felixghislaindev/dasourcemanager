<template>
  <div>
    <a-modal
      :visible="isDbConnectionModalOpen"
      title="Select the Datasource"
      okText="Continue"
      @ok="handleSetDataObject"
      @cancel="handleCancel"
    >
      <h2>Select the Datasource:</h2>
      <div class="datasource-list">
        <a-radio-group v-model="value" @change="onChange">
          <a-radio
            :style="radioStyle"
            v-for="(datasource, index) in dataSources"
            :key="index"
            :value="index"
          >
            <span>{{ datasource.name }}</span>
          </a-radio>
        </a-radio-group>
      </div>
    </a-modal>

    <a-modal
      :visible="isDataObjectModalOpen"
      title="Select the Datasource"
      okText="Continue"
      @ok="handleSelectColumn"
      @cancel="handleCancel"
    >
      <h2>Select Table(s):</h2>
      <a-transfer
        :data-source="mockData"
        :target-keys="targetKeys"
        :render="(item) => item.title"
        @change="handleChange"
      />
    </a-modal>
    <a-modal
      :visible="isSelectColumnModalOpen"
      title="Select the Datasource"
      okText="Continue"
      @ok="handleStoreDataObject"
      @cancel="handleCancel"
    >
      <h2>Select Columns(s):</h2>
      <a-transfer
        :data-source="columnMockData"
        :target-keys="columnsTargetKeys"
        :render="(item) => item.title"
        @change="handleColumnChange"
      />
    </a-modal>
    <a-modal
      :visible="isStoreDataObjectModalOpen"
      title="Select the Datasource"
      okText="Continue"
      @ok="handleOk"
      @cancel="handleCancel"
    >
      <h2>Store Data Object:</h2>
      <a-input style="width: 50%" placeholder="Data Source Name" />
    </a-modal>
  </div>
</template>

<script>
import { Modal, Radio, Transfer, Input} from "ant-design-vue";
import Vue from "vue";
Modal.install(Vue);
// const FormItem = Form.Item;
const radioGroup = Radio.Group;

export default {
  name: "DbConnection",
  data() {
    return {
      mockData: [],
      targetKeys: [],
      columnMockData:[],
      columnsTargetKeys:[],
      value: 0,
      radioStyle: {
        display: "block",
        height: "30px",
        lineHeight: "30px",
      },
      dataSources: [
        {
          name: "DsKaxanDBMongoDB",
          tables: ["Event", "people"],
          columns: ["type", "id", "desc"],
        },
        { name: "DsClientsDBDynamoDB", tables: ["tasks", "issues"] },
      ],
      isDataObjectModalOpen: false,
      isSelectColumnModalOpen:false,
      isStoreDataObjectModalOpen:false,
    };
  },
  mounted() {
    this.getMock();
  },
  components: {
    "a-modal": Modal,
    "a-radio": Radio,
    "a-radio-group": radioGroup,
    "a-transfer": Transfer,
    "a-input": Input,
  },
  props: {
    isDbConnectionModalOpen: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleOk(e) {
      console.log(e);
    },
    handleCancel() {
      this.$emit("canceDblModal");
    },
    handleSubmit() {
      console.log();
    },
    selectedOption() {},
    onChange() {},
    handleSetDataObject() {
      this.$emit("canceDblModal");
      this.isDataObjectModalOpen = true;
    },
    getMock() {
      const targetKeys = [];
      const mockData = [];
      for (let i = 0; i < this.dataSources[0].tables.length; i++) {
        const data = {
          key: i.toString(),
          title: `${this.dataSources[0].tables[i]}`,
          description: `description of content${i + 1}`,
        };
        mockData.push(data);
      }
      this.mockData = mockData;
      this.targetKeys = targetKeys;
    },
    handleChange(targetKeys, direction, moveKeys) {
      console.log(targetKeys, direction, moveKeys);
      this.targetKeys = targetKeys;
    },
    handleSelectColumn() {
      this.isDataObjectModalOpen = false;
      this.isSelectColumnModalOpen = true;
      this.getColumnsMock()
    },
    getColumnsMock() {
      const targetKeys = [];
      const mockData = [];
      for (let i = 0; i < this.dataSources[0].columns.length; i++) {
        const data = {
          key: i.toString(),
          title: `${this.dataSources[0].columns[i]}`,
          description: `description of content${i + 1}`,
        };
        mockData.push(data);
      }
      this.columnMockData = mockData;
      this.columnsTargetKeys = targetKeys;
    },
    handleColumnChange(targetKeys){
      this.columnsTargetKeys = targetKeys;
    },
    handleStoreDataObject(){
      this.isSelectColumnModalOpen =false
      this.isStoreDataObjectModalOpen = true;
    }
  },
};
</script>

<style lang="css">
.ant-checkbox-group-item {
  display: block;
  margin-right: 0;
}
.datasource-list {
  overflow-y: auto;
  height: 300px;
  outline: solid 1.2px;
  padding: 20px;
}
</style>
