<template>
  <div>
    <div class="create-connection-section">
      <!-- will hold button to create connection -->
      <a-button @click="handleCreateConnection" class="create-connection"
        >Select Datasource</a-button
      >
      <a-button @click="handleConnectToDB" class="connect-to-db"
        >Connect To DB</a-button
      >
      <CreateConnectionModal
        :isModalOpen="isDbModalOpen"
        @cancelModal="handleCancelConnection"
      />
      <DbConnection
        :isDbConnectionModalOpen="isOpen"
        @canceDblModal="handleCancelDbConnection"
      />
    </div>
    <div class="listing-info"></div>
    <div class="connections-listing">
      <!-- will hold a tble displayin the connections created -->
      <h3 class="title">Connection Listings</h3>
      <a-tabs default-active-key="1" @change="selecTab" class="tab-menu">
        <a-tab-pane key="1" tab="Overview">
          <a-list
            class="demo-loadmore-list"
            item-layout="horizontal"
            :data-source="data"
          >
            <a-list-item>
              <a slot="actions">View</a>
              <a slot="actions">Delete</a>

              <div>
                <div class="title">Connection to monngo</div>
                <div class="desc">
                  Lorem ipsum dolor sit amet, consectetur adipisicing elit.
                  Magni aperiam ex sint quo nemo tempora dignissimos maiores,
                  rem possimus fugit accusantium dolor,
                </div>
              </div>
            </a-list-item>
            <a-list-item>
              <a slot="actions">View</a>
              <a slot="actions">Delete</a>

              <div>
                <div class="title">Connection to sql1</div>
                <div class="desc">
                  Lorem ipsum dolor sit amet, consectetur adipisicing elit.
                  Magni aperiam ex sint quo nemo tempora dignissimos maiores,
                  rem possimus fugit accusantium dolor, 
                </div>
              </div>
            </a-list-item>
          </a-list>
        </a-tab-pane>
        <a-tab-pane key="2" tab="Resources" force-render>
          <div class="grid-doc-hub-container">
            <div class="db-display">
              <div class="title">Db Connections</div>
              <a-directory-tree
                multiple
                default-expand-all
                @select="onSelect"
                @expand="onExpand"
              >
                <a-tree-node key="0-0" title="parent 0">
                  <a-tree-node key="0-0-0" title="leaf 0-0" is-leaf />
                  <a-tree-node key="0-0-1" title="leaf 0-1" is-leaf />
                </a-tree-node>
                <a-tree-node key="0-1" title="parent 1">
                  <a-tree-node key="0-1-0" title="leaf 1-0" is-leaf />
                  <a-tree-node key="0-1-1" title="leaf 1-1" is-leaf />
                </a-tree-node>
              </a-directory-tree>
            </div>
            <div class="db-collection-display">
              <div class="title">Collections</div>
              <a-directory-tree
                multiple
                default-expand-all
                @select="onSelect"
                @expand="onExpand"
              >
                <a-tree-node key="0-0" title="parent 0">
                  <a-tree-node key="0-0-0" title="leaf 0-0" is-leaf />
                  <a-tree-node key="0-0-1" title="leaf 0-1" is-leaf />
                </a-tree-node>
                <a-tree-node key="0-1" title="parent 1">
                  <a-tree-node key="0-1-0" title="leaf 1-0" is-leaf />
                  <a-tree-node key="0-1-1" title="leaf 1-1" is-leaf />
                </a-tree-node>
              </a-directory-tree>
            </div>
            <div class="db-main-display">test5</div>
          </div>
        </a-tab-pane>
        <a-tab-pane key="3" tab="Settings"> Content of Tab Pane 3 </a-tab-pane>
      </a-tabs>
    </div>
  </div>
</template>

<script>
import { Button, Tabs, List, Tree } from "ant-design-vue";
import CreateConnectionModal from "./CreateConnectionModal";
import DbConnection from "./DbConnection";
const TabPane = Tabs.TabPane;
const ListItem = List.Item;
const TreeNode = Tree.TreeNode;
export default {
  name: "Dashboard",
  data() {
    return {
      data: [
        {
          gender: "Connection to Mongo",
          name: {
            title: "Mr",
            first: "Akseli",
            last: "Ahonen",
          },
          email: "akseli.ahonen@example.com",
          nat: "FI",
        },
        {
          gender: "Connection to Sql",
          name: {
            title: "Mr",
            first: "Akseli",
            last: "Ahonen",
          },
          email: "akseli.ahonen@example.com",
          nat: "FI",
        },
      ],
      isOpen: false,
      isDbModalOpen: false,
    };
  },
  methods: {
    selecTab(key) {
      console.log(key);
    },
    handleCreateConnection() {
      this.isOpen = true;
    },
    handleCancelConnection() {
      this.isDbModalOpen = false;
    },
    handleConnectToDB() {
      this.isDbModalOpen = true;
    },
    handleCancelDbConnection() {
      this.isOpen = false;
    },
    onSelect(keys, event) {
      console.log("Trigger Select", keys, event);
    },
    onExpand() {
      console.log("Trigger Expand");
    },
  },
  components: {
    "a-button": Button,
    "a-tabs": Tabs,
    "a-tab-pane": TabPane,
    "a-list": List,
    "a-list-item": ListItem,
    "a-directory-tree": Tree,
    "a-tree-node": TreeNode,
    CreateConnectionModal,
    DbConnection,
  },
};
</script>

<style lang="css" scoped>
.create-btn {
  border: none;
  background: none;
  cursor: pointer;
  letter-spacing: 1px;
  font-weight: 700;
  padding: 15px 30px;
  outline: none;
  transition: all 0.3s;
  background-color: #1dd1a1;
}
.demo-loadmore-list {
  min-height: 350px;
  min-width: 150px;
  display: block;
}
.title {
  margin: 30px;
}
.create-connection,
.connect-to-db {
  margin-left: 10px;
}
.grid-doc-hub-container {
  display: grid;
  grid-template-columns: 0.7fr 0.9fr 1.4fr;
  grid-template-rows: 1fr;
  gap: 0px 0px;
  grid-template-areas: ". . .";
}
</style>
