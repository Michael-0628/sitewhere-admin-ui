<template>
  <navigation-page icon="car" title="Assets"
    loadingMessage="Loading assets ..." :loaded="loaded">
    <div v-if="assets" slot="content">
      <v-container fluid grid-list-md style="background-color: #f5f5f5;">
        <v-layout row wrap>
           <v-flex xs6 v-for="(asset) in assets" :key="asset.token">
            <asset-list-entry :asset="asset" @assetOpened="onOpenAsset">
            </asset-list-entry>
          </v-flex>
        </v-layout>
      </v-container>
      <pager :results="results" :pageSizes="pageSizes"
        @pagingUpdated="updatePaging">
      </pager>
      <asset-create-dialog ref="add" @assetAdded="onAssetAdded"/>
    </div>
    <div slot="actions">
      <navigation-action-button icon="plus" tooltip="Add Asset"
        @action="onAddAsset">
      </navigation-action-button>
    </div>
  </navigation-page>
</template>

<script>
import Utils from "../common/Utils";
import NavigationPage from "../common/NavigationPage";
import NavigationActionButton from "../common/NavigationActionButton";
import Pager from "../common/Pager";
import AssetListEntry from "./AssetListEntry";
import AssetCreateDialog from "./AssetCreateDialog";
import { _listAssets } from "../../http/sitewhere-api-wrapper";

export default {
  data: () => ({
    results: null,
    paging: null,
    assets: [],
    pageSizes: [
      {
        text: "20",
        value: 20
      },
      {
        text: "50",
        value: 50
      },
      {
        text: "100",
        value: 100
      }
    ],
    loaded: false
  }),

  components: {
    NavigationPage,
    NavigationActionButton,
    Pager,
    AssetListEntry,
    AssetCreateDialog
  },

  methods: {
    // Update paging values and run query.
    updatePaging: function(paging) {
      this.$data.paging = paging;
      this.refresh();
    },

    // Refresh data.
    refresh: function() {
      this.$data.loaded = false;
      var paging = this.$data.paging.query;
      var component = this;
      var options = {};
      _listAssets(this.$store, options, paging)
        .then(function(response) {
          component.loaded = true;
          component.results = response.data;
          component.$data.assets = response.data.results;
        })
        .catch(function(e) {
          component.loaded = true;
        });
    },

    // Called on open.
    onOpenAsset: function(asset) {
      Utils.routeTo(this, "/assets/" + asset.token);
    },

    // Called to open dialog.
    onAddAsset: function() {
      this.$refs.add.onOpenDialog();
    },

    // Called on add.
    onAssetAdded: function() {
      this.refresh();
    }
  }
};
</script>

<style scoped>
</style>
