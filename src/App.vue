<template>
  <div>
<div>
  <b-button v-b-modal.modal-1 @click="getSelectedRows()">Get Selected Row</b-button>

  <b-modal id="modal-1" title="Stock">
   
    <EditForm :stock-data="this.stockselection" />
   
      <template v-slot:modal-footer="{ cancel }">
        <b-button @click="cancel()">Cancel</b-button>
      </template>

  </b-modal>
</div>

    <ag-grid-vue style="width: 800px; height: 400px;"
        class="ag-theme-alpine"
        :columnDefs="columnDefs"
        :rowData="rowData"
        rowSelection="multiple"
        @grid-ready="onGridReady">
    </ag-grid-vue>

  </div>
</template>

<script>
    import { AgGridVue } from "ag-grid-vue";
    import EditForm from '@/components/EditForm';

    export default {
        name: 'App',
        data() {
            return {
                columnDefs: null,
                rowData: null,
                gridApi: null,
                columnApi: null,
                stockselection: [
                  {
                    id: 0,
                    sku: "",
                    store: "",
                    style: ""
                  }
                 ],         
            }
        },
        components: {
            AgGridVue,
            EditForm
        },
        methods: {
            onGridReady(params) {
                this.gridApi = params.api;
                this.columnApi = params.columnApi;
            },
            getSelectedRows() {
                const selectedNodes = this.gridApi.getSelectedNodes();
                const selectedData = selectedNodes.map( node => node.data );
            //    const selectedDataStringPresentation = selectedData.map( node => `${node.make} ${node.model} ${node.price}`).join(', ');
            
              this.stockselection =  [
                  {
                    id: selectedData[0].partnerStockId,
                    sku: selectedData[0].productSKU,
                    store: selectedData[0].store,
                    style: selectedData[0].styleOption
                  }
                ]     
               
                
            },

        },
        beforeMount() {
            this.columnDefs = [
              {field: 'partnerStockId', sortable: true, filter: true, checkboxSelection: true},
              { field: 'productSKU', sortable: true, filter: true },
              { field: 'store', sortable: true, filter: true },
              { field: 'styleOption', sortable: true, filter: true }
            ];

        fetch('https://localhost:5001/api/ist/v1/partner-stock')
          .then(result => result.json())
          .then(rowData => this.rowData = rowData);
        }
    }
</script>


<style lang="scss">
  @import "../node_modules/ag-grid-community/dist/styles/ag-grid.css";
  @import "../node_modules/ag-grid-community/dist/styles/ag-theme-alpine.css";
</style>
