<template>
  <span class="content" @click="btnClick">
    <input id="upload-file" class="input-file" type="file" @change="exportData"
           accept=".csv, application/vnd.openxmlformats-officedocument.spreadsheetml.sheet, application/vnd.ms-excel" />
    {{title}}
  </span>
</template>

<script>
    import XLSX from 'xlsx'
    export default {
        name: "ImportExcelCommon",
        props: {
            title: {
                type: String,
                default: '导入表格'
            }
        },
        methods: {
            btnClick() {
                document.getElementById('upload-file').click();
            },
            exportData(event) {
                if(!event.currentTarget.files.length) {
                    return;
                }
                const that = this;
                // 拿取文件对象
                let f = event.currentTarget.files[0];
                // 用FileReader来读取
                let reader = new FileReader();
                // 重写FileReader上的readAsBinaryString方法
                const rABS = true;
                reader.onload = e => {
                    let dataResult = e.target.result;
                    if (!rABS) dataResult = new Uint8Array(dataResult);
                    const workbook = XLSX.read(dataResult, {
                        type: rABS ? 'binary' : 'array',
                    });
                    // 假设我们的数据在第一个标签
                    const firstWorksheet = workbook.Sheets[workbook.SheetNames[0]];
                    // XLSX自带了一个工具把导入的数据转成json
                    const jsonArr = XLSX.utils.sheet_to_json(firstWorksheet, { header: 1 });
                    // 通过自定义的方法处理Json，比如加入state来展示
                    that.$emit("getResult", jsonArr);
                    document.getElementById('upload-file').value = null;
                };
                if (rABS) reader.readAsBinaryString(f);
                else reader.readAsArrayBuffer(f);
                return false;
            },
        }
    }
</script>

<style scoped>
    .input-file {
        display: none;
    }
    .content{
        margin-right: 5px;
    }
</style>
