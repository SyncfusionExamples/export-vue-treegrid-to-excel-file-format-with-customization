<template>
  <ejs-treegrid ref="treegrid" :dataSource="data" childMapping="subtasks" 
    :treeColumnIndex="1" :height='450' :allowPaging="true"
    :allowExcelExport="true" :toolbar="toolbarOptions" :toolbarClick="toolbarBtnClick">
    <e-columns>
        <e-column field='ID' headerText='S.No' width='90' textAlign='Right'></e-column>
        <e-column field='Name' headerText='Shipment Name' width='220'></e-column>
        <e-column field='category' headerText='Category' width='220'></e-column>
        <e-column field='unitPrice' headerText='Unit Price($)' format='c2' width='120' textAlign='Right'></e-column>
        <e-column field='price' headerText='Price($)' width='100' format='c' textAlign='Right'></e-column>
    </e-columns>
  </ejs-treegrid>
</template>
<script>
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Page, ExcelExport, Toolbar } from "@syncfusion/ej2-vue-treegrid";
import {summaryData} from './data.js';

export default{
  name: 'App',
  components: {
    'ejs-treegrid': TreeGridComponent,
    'e-columns': ColumnsDirective,
    'e-column': ColumnDirective
  },
  data: () => {
    return {
      data: summaryData,
      toolbarOptions: ['ExcelExport', 'CsvExport']
    }
  },
  methods:{
    toolbarBtnClick(args){
      var treegridObj = this.$refs.treegrid.ej2Instances;
      if(args['item'].text === "Excel Export"){
        treegridObj.excelExport({
          fileName: "SummaryData.xlsx",
          theme:{
            header:{fontColor:"#64FA50", fontSize:10, fontName:"Calibri", bold:true},
            record: {fontSize:8, fontName:"Calibri", fontColor:"#0000FF"}
          },
          header:{
            headerRows: 1,
            rows:[
              {
                cells: [
                  {colSpan:4, value:"Shipment Details", style:{fontColor: '#C67878', fontSize: 20, hAlign: 'Center', bold: true,}}
                ]
              }
            ]
          },
          footer:{
            footerRows: 1,
            rows:[
              {
                cells: [
                  {colSpan:4, value:"!Visit Again!", style:{fontColor: '#C67878', fontSize: 16, hAlign: 'Center', bold: true,}}
                ]
              }
            ]
          }
        }
        );
      }else if(args['item'].text === "CSV Export"){
        treegridObj.csvExport();
      }
    }
  },
  provide:{
    treegrid: [Page, ExcelExport, Toolbar]
  }
}
</script>

<style>
  @import "../node_modules/@syncfusion/ej2-base/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-calendars/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-dropdowns/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-vue-grids/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-vue-treegrid/styles/material.css";
</style>
