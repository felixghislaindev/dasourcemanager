<template>
  <div>
    <a-modal
      :visible="isSelectDatabseModalOpen"
      title="Select Database"
      okText="Continue"
      @ok="handleOk"
      @cancel="handleDatabaseModalCancel"
    >
      <div class="selection-phase-one" v-if="isDatabaseSelected">
        <h2>
          <a-icon type="database" class="database-icon" />A. Select Database
        </h2>
        <a-select
          default-value="Select Type of Database"
          style="width: 50%"
          class="select-input"
        >
          <a-select-option
            v-for="(databaseType, index) in databaseTypes"
            :key="index"
            :value="databaseType"
          >
            {{ databaseType }}
          </a-select-option>
        </a-select>
        <br />
        <a-select
          default-value="Select Database"
          style="width: 50%"
          class="select-input"
        >
          <a-select-option
            v-for="(database, index) in databases"
            :key="index"
            :value="database"
          >
            {{ database }}
          </a-select-option>
        </a-select>
        <br />
        <span class="database-name-label">Database Name:</span>
        <br />
        <a-input
          style="width: 50%"
          placeholder="Enter Database Name(ie.SQLite)"
          class="database-name"
        />
      </div>
    </a-modal>
    <a-modal
      :visible="isConectionTested"
      title="Select Database"
      okText="Continue"
      @ok="setDataSource"
      @cancel="handleConnectToDBModal"
    >
      <div class="selection-phase-two" v-if="isConectionTested">
        <div class="database-connection-entry">
          <h2>
            <a-icon type="database" class="database-icon" />B. Test Connection
          </h2>
          <a-input style="width: 50%" placeholder="Host" />
          <br />
          <a-input style="width: 50%" placeholder="Database Name" />
          <br />
          <a-input style="width: 50%" placeholder="User" />
          <br />
          <a-input style="width: 50%" placeholder="Password" />
        </div>
        <div class="conections">
          <span>Test Connection</span>
          <br />
          <a-icon
            type="database"
            class="database-connection-icon"
            :style="{ fontSize: '20px' }"
          />
          <a-progress
            :percent="100"
            size="small"
            style="width: 50%"
            status="active"
            :show-info="false"
          />
          <a-icon
            type="database"
            class="database-connection-icon"
            :style="{ fontSize: '21px' }"
          />
        </div>
      </div>
    </a-modal>
    <a-modal
      :visible="isDataSourceReady"
      title="Select Database"
      okText="Continue"
      @ok="saveDataSource"
      @cancel="cancelDataSourceModal"
    >
      <div class="selection-phase-three" v-show="isDataSourceReady">
        <h2>
          <a-icon type="database" class="database-icon" />C. Store Datasource
        </h2>
        <a-input style="width: 50%" placeholder="Data Source Name" />
      </div>
    </a-modal>
  </div>
</template>

<script>
import { Modal, Select, Input, Icon, Progress } from "ant-design-vue";
import Vue from "vue";
Modal.install(Vue);
// const FormItem = Form.Item;
const SelectOption = Select.Option;

export default {
  name: "SelectDatabase",
  data() {
    return {
      databaseTypes: ["SQL", "NoSQL", "Graph Database"],
      databases: ["MySQL", "Oracle", "Postgres", "MariaDB", "Other"],
      isDatabaseSelected: true,
      isConectionTested: false,
      isDataSourceReady: false,
      step: 1,
    };
  },
  components: {
    "a-modal": Modal,
    "a-select": Select,
    "a-input": Input,
    "a-icon": Icon,
    "a-progress": Progress,
    "a-select-option": SelectOption,
  },
  props: {
    isSelectDatabseModalOpen: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleOk() {
      this.handleDatabaseModalCancel()
        this.isConectionTested = true;
    },
    handleDatabaseModalCancel(e) {
      this.isSelectDatabseModalOpen = false;
      console.log(e);
    },
    handleConnectToDBModal(){
      this.isConectionTested = false;
    },
    handleSubmit() {
      console.log();
    },
    selectedOption() {},
    setDataSource() {
      if (this.isConectionTested) {
        this.handleConnectToDBModal()
        this.isDataSourceReady = true;
        
      }
    },
    saveDataSource() {},
    cancelDataSourceModal(){
      this.isDataSourceReady = false;
    }
  },
};
</script>

<style lang="css" scoped>
.ant-checkbox-group-item {
  display: block;
  margin-right: 0;
}
.database-name-label {
  margin-top: 35px;
}
.select-input {
  margin-bottom: 20px;
}
.ant-select-selection {
  margin-bottom: 10px;
}
.database-icon {
  margin-right: 8px;
}
.database-connection-icon {
  margin: 0 2px;
}
.selection-phase-two {
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  grid-template-rows: 1fr;
  gap: 0px 0px;
  grid-template-areas: ". .";
  justify-content: center;
  align-content: center;
}
</style>
