<template>
  <div id="app">
    <div class="names">
      <h2>{{name}}</h2>

      <div class="box">
        <ImportExcelCommon title="上传" @getResult="getMyExcelData"></ImportExcelCommon>
      </div>



      <div v-if="tableData.length>0">
        <el-table
                :data="tableData"
                style="width: 100%"
        >
          <el-table-column v-for="item in titles"
                  :prop="item.prop"
                  :label="item.label">
          </el-table-column>

        </el-table>

      </div>

    </div>
  </div>
</template>

<script>
  import ImportExcelCommon from './excel'

export default {
  name: "importExcelCommon",
  components: {
    ImportExcelCommon
  },

  data(){
    return {
      name:"月度汇总表转全国考勤汇总表",
      tableData:[],
      titles:[]
    }
  },

  methods: {
    getMyExcelData(data) {
      // data为读取Excel的原始数据，这里可以对Excel进行格式校验和数据格式化处理

      console.log(data);

      let titles=[]
      let tableData=[]
      for(let i in data[2]){
        titles.push({
          prop:'title'+i,
          label:data[2][i]
        })
      }

      this.titles=titles


      tableData=data.slice(2,data.length)


      console.log(tableData);

      let tableDatas=[]

      for(let i in tableData){

          tableDatas[i]={
            title0: tableData[i][0],
            title1: tableData[i][1],
            title2: tableData[i][2],
            title3: tableData[i][3],
            title4: tableData[i][4],
            title5: tableData[i][5],
            title6: tableData[i][6],
            title7: tableData[i][7],
            title8: tableData[i][8],
            title9: tableData[i][9],
            title10: tableData[i][10],
            title11: tableData[i][11],
            title12: tableData[i][12],
            title13: tableData[i][13],
            title14: tableData[i][14],
            title15: tableData[i][15],
            title16: tableData[i][16],
            title17: tableData[i][17],
            title18: tableData[i][18],
            title19: tableData[i][19],
            title20: tableData[i][20],
        }

      }

      console.log(data);
      console.log(tableDatas);




      this.tableData=tableDatas




    },
  },




}
</script>

<style>
#app {
  font-family: Helvetica, sans-serif;
  text-align: center;
}


  .box{
    width: 100px;
    height: 50px;
    background: #037afe;
    color: #ffffff;
    text-align: center;
    border-radius: 15px;
    line-height: 50px;
    margin: 0 auto;
    cursor: pointer;
  }

</style>
