<template>
  <wj-combo-box :displayMemberPath="'country'" :headerPath="'country'" :itemsSource="cv" :dropDownCssClass="'combo-dropdown'">
    <wj-item-template v-slot="ctx">
      <div class="item">
        <div class="itemHeader"><img :src="ctx.item.flag"/><b>{{ctx.item.country}}</b></div>
        Sales: <b>${{ctx.item.sales}}</b><br/>
        Expense: <b>${{ctx.item.expenses}}</b>
      </div>
    </wj-item-template>
  </wj-combo-box><br/><br/>
  <wj-flex-grid :itemsSource="cv" :selectionMode="'Row'">
    <wj-flex-grid-column :binding="'country'" :header="'Country'"></wj-flex-grid-column>
    <wj-flex-grid-column :binding="'sales'" :header="'Sales'" :width="'*'" :format="'c2'"></wj-flex-grid-column>
    <wj-flex-grid-column :binding="'expenses'" :header="'Expenses'" :width="'*'" :format="'c2'"></wj-flex-grid-column>
  </wj-flex-grid>
</template>

<script>
import '@grapecity/wijmo.styles/themes/wijmo.theme.material.css';
import '@grapecity/wijmo.vue2.input';
import * as wjCore from '@grapecity/wijmo';
import * as wjcInput from '@grapecity/wijmo.vue2.input';
import * as wjcGrid from '@grapecity/wijmo.vue2.grid';

export default {
  name: 'App',
  components: {
    'wj-combo-box': wjcInput.WjComboBox,
    'wj-item-template': wjcInput.WjItemTemplate,
    'wj-flex-grid': wjcGrid.WjFlexGrid,
    'wj-flex-grid-column': wjcGrid.WjFlexGridColumn
  },
  data() {
    return {
      cv: new wjCore.CollectionView([], {})
    };
  },
  created() {
    fetch('https://mocki.io/v1/eaf8d0a8-052c-4d2a-b105-da40855634fa').then(response => response.json()).then(data => (this.cv.sourceCollection = data));
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 30px;
}

.wj-control .wj-input-group .wj-form-control {
  background: hsl(0, 0%, 15%);
  color: hsl(0, 0%, 70%);
  font-weight: bold;
  padding: 10px 16px 8px;
  font-size: 16px;
}

.wj-control .wj-input-group .wj-input-group-btn {
  background: hsl(0, 0%, 15%);
}

.wj-control .wj-input-group-btn>.wj-btn.wj-btn-default:hover {
  background: hsl(0, 0%, 30%);
  transition: .4s;
}

.wj-control .wj-input-group-btn>.wj-btn.wj-btn-default:hover .wj-glyph-down {
  color: hsl(0, 0%, 85%);
  transition: .4s;
}

.wj-combobox {
  border-radius: 0px;
  border: 1px solid rgba(0, 0, 0, 0.5);
}

.wj-listbox-item {
  background: hsl(0, 0%, 15%);
  color: hsl(0, 0%, 70%);
}

.wj-listbox-item.wj-state-selected {
  background: hsl(0, 0%, 30%);
}

.wj-control .wj-input-group .wj-input-group-btn:last-child:not(:first-child)>.wj-btn {
  border-left: 1px solid hsl(0, 0%, 70%);
}

.combo-dropdown > .wj-listbox-item:hover {
  cursor: pointer;
  background: hsl(0, 0%, 30%) !important;
  transition: .3s;
}

.wj-glyph-down {
  color: hsl(0, 0%, 70%);
}

.item {
  margin: 2px;
}

.itemHeader {
  font-size: 16px;
  margin-bottom: 4px;
}

.wj-flexgrid {
  width: 450px;
}
</style>
