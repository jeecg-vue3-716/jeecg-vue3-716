<template>
    <div>
        <el-row style="margin-top: 20px;display: flex;justify-content:space-between;">
            <div class="data-header-left">
                <el-select v-model="selectValue" style="width:100px;margin-left: 20px;" placeholder="Actions">
                    <el-option v-for="item in options" :key="item.value" :label="item.label"
                        :value="item.value"></el-option>
                </el-select>
                <el-button size="default" @click="" style="margin-left: 10px;">Delete</el-button>
            </div>
            <div class="data-header-right">
                <el-button type="danger" size="default" style="margin-right: 20px;" @click="">Delete
                    All</el-button>
            </div>
        </el-row>
        <el-input v-model="dataInput" size="large" placeholder="Search(e.g label:postive)" clearable @change=""
            style="margin: 20px 0px;"></el-input>
        <el-table ref="multipleTableRef" :data="tableData" style="width: 100%" >
            <el-table-column type="selection" width="55" />
            <el-table-column label="ID" width="120" prop="id"></el-table-column>
            <el-table-column label="Status" width="120">
                <template #default="scope">
                    <el-button size="small" type="warning" @click="handletest(scope.$index, scope.row)" >In progress</el-button>
                </template>
            </el-table-column>
            <el-table-column label="Text"  prop="text"/>
            <el-table-column label="Metadata" prop="metedata" width="120"/>
            <el-table-column label="Comments" prop="comments" width="120">
            </el-table-column>
            <el-table-column label="Actions" width="200">
                <template #default="scope">
                    <el-button size="small" type="primary" @click="handleEdit(scope.$index, scope.row)" >Edit</el-button>
                    <el-button size="small" type="primary" @click="handleDelete(scope.$index, scope.row)">Annotate</el-button>
                </template>
            </el-table-column>
        </el-table>

        <el-pagination
      v-model:current-page="currentPage4"
      v-model:page-size="pageSize4"
      :page-sizes="[3, 5, 7, 9]"
      :small="small"
      :disabled="disabled"
      :background="background"
      layout=" prev, pager, next, jumper,->,total, sizes"
      :total="10" style="margin-top: 20px;"
    />

    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'


const currentPage4 = ref(4)
const pageSize4 = ref(3)
const small = ref(false)
const background = ref(false)
const disabled = ref(false)
let selectValue = ref()
let dataInput = ref()
const handleDelete = (index: number, row: any) => {
  console.log(index, row)
}
const handletest = (index: number, row: any) => {
  console.log(index, row)
}
const handleEdit = (index: number, row: any) => {
  console.log(index, row)
}
const options = [
    {
        value: 'Option1',
        label: '新建',
    },
    {
        value: 'Option2',
        label: '导入文本',
    },
    {
        value: 'Option3',
        label: '导入演训数据',
    },

]
const tableData: any = [
    {
        id: '1',
        text: '第五十一条【战斗特点】进攻海上战斗舰艇编队战斗的主要特点：战斗进程短促，战机不宜捕捉，主动权易于转化，中远程精确打击为主',
        metedata: '{}',
        comments:'()'
    },
    {
        id: '2',
        text: '第五十一条【战斗特点】进攻海上战斗舰艇编队战斗的主要特点：战斗进程短促，战机不宜捕捉，主动权易于转化，中远程精确打击为主',
        metedata: '{}',
        comments:'()'
    },
    {
        id: '3',
        text: '第五十一条【战斗特点】进攻海上战斗舰艇编队战斗的主要特点：战斗进程短促，战机不宜捕捉，主动权易于转化，中远程精确打击为主',
        metedata: '{}',
        comments:'()'
    },
    {
        id: '4',
        text: '第五十一条【战斗特点】进攻海上战斗舰艇编队战斗的主要特点：战斗进程短促，战机不宜捕捉，主动权易于转化，中远程精确打击为主',
        metedata: '{}',
        comments:'()'
    },
    {
        id: '5',
        text: '第五十一条【战斗特点】进攻海上战斗舰艇编队战斗的主要特点：战斗进程短促，战机不宜捕捉，主动权易于转化，中远程精确打击为主',
        metedata: '{}',
        comments:'()'
    },
    {
        id: '6',
        text: '第五十一条【战斗特点】进攻海上战斗舰艇编队战斗的主要特点：战斗进程短促，战机不宜捕捉，主动权易于转化，中远程精确打击为主',
        metedata: '{}',
        comments:'()'
    },
    {
        id: '7',
        text: '第五十一条【战斗特点】进攻海上战斗舰艇编队战斗的主要特点：战斗进程短促，战机不宜捕捉，主动权易于转化，中远程精确打击为主',
        metedata: '{}',
        comments:'()'
    },
    
]

</script>

<style scoped lang="less"></style>