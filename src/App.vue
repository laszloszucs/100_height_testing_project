<template>
  <div id="app">
      <transition-expand :after-enter="afterEnter" :after-leave="afterLeave">
        <div v-show="isShowTableSettings" class="setting-container">
            <div id="settings" class="settings">
                <div>Table Setting 1</div>
                <div>Table Setting 2</div>
                <div>Table Setting 3</div>
                <div>Table Setting 1</div>
                <div>Table Setting 2</div>
                <div>Table Setting 3</div>
                <div>Table Setting 1</div>
                <div>Table Setting 2</div>
                <div>Table Setting 3</div>
            </div>
        </div>
    </transition-expand>
    <div class="buttons">
      <button @click="isShowTableSettings=!isShowTableSettings">
          {{ isShowTableSettings ? 'Hide' : 'Show' }}
      </button>
    </div>
    <div class="table">
        <DxDataGrid
            ref="dataGridRef"
            :data-source="dataSource"
            :show-borders="true"
        >
            <DxPaging :page-size="10"/>
            <DxPager
            :show-page-size-selector="true"
            :allowed-page-sizes="pageSizes"
            :show-info="true"
            height="100%"
            />

            <DxColumn data-field="CompanyName"/>
            <DxColumn data-field="City"/>
            <DxColumn data-field="State"/>
            <DxColumn data-field="Phone"/>
            <DxColumn data-field="Fax"/>
            <DxScrolling show-scrollbar="always" column-rendering-mode="virtual"/>
        </DxDataGrid>
    </div>
  </div>
</template>

<script>
import { DxDataGrid, DxColumn, DxPager, DxPaging, DxScrolling } from 'devextreme-vue/data-grid';
import { customers } from './assets/data.js';
import TransitionExpand from './components/TransitionExpand.vue';
export default {
  name: 'App',
  components: {
    DxDataGrid,
    DxColumn,
    DxPager,
    DxPaging,
    DxScrolling,
    TransitionExpand
  },
  data() {
    return {
      isShowTableSettings: true,
      dataSource: customers,
      pageSizes: [5, 10, 20]
    };
  },
  methods: {
    afterEnter() {
      this.dataGrid.repaint();
    },
    afterLeave() {
      this.dataGrid.repaint();
    }
  },
  computed: {
    dataGrid() {
        return this.$refs['dataGridRef'].instance;
    }
  }
}
</script>
