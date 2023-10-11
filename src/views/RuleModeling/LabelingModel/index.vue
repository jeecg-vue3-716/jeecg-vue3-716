<template>
    <div>
        <el-card style="margin: 10px 10px;">
            <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
                <el-tab-pane label="Project" name="first"></el-tab-pane>
                <el-tab-pane label="Auto Labeling" name="second">
                    <el-button type="primary" size="large" @click="dialogTableVisible = true">Create</el-button>
                    <el-button size="large">Delete</el-button>
                </el-tab-pane>
            </el-tabs>

        </el-card>
        <el-dialog v-model="dialogTableVisible">
            <el-steps :active="active" finish-status="success">
                <el-step title="Step 1" />
                <el-step title="Step 2" />
                <el-step title="Step 3" />
                <el-step title="Step 4" />
            </el-steps>
            <el-card v-if="cardNumber == 1" style="margin-top: 20px;">
                <el-row style="font-size: 20px;">Select a config template</el-row>
                <el-row style="font-size: 15px;">You can select the template to create the
                    auto-labelingconfiguration.true</el-row>
                <el-row style="margin: 10px 0px;">
                    <el-select v-model="value1" placeholder="SquenceLabeling" size="large" style="width: 100%">
                        <el-option v-for="item in options1" :key="item.value1" :label="item.label" :value="item.value1" />
                    </el-select>
                </el-row>
                <el-row>
                    <el-select v-model="value2" placeholder="SquenceLabeling" size="large" style=" width: 100%">
                        <el-option v-for="item in options2" :key="item.value2" :label="item.label" :value="item.value2" />
                    </el-select>
                </el-row>

            </el-card>
            <el-card v-if="cardNumber == 2" style="margin-top: 20px;">
                <el-row style="font-size: 20px;">Set parameters</el-row>
                <el-row style="font-size: 15px;">You can set parameters to fetch API response. </el-row>
                <el-row style="margin:10px 0px;">
                    <el-input v-model:url="url" placeholder="url" size="large" clearable @change=""></el-input>

                </el-row>
                <el-row style="margin:10px 0px;">
                    <el-input v-model:method="method" placeholder="method" size="large" clearable @change=""></el-input>

                </el-row>
                <el-row style="margin: 10px 0px;">
                    <el-select v-model="value1" placeholder="params" size="large" style="width: 100%;">
                        <el-option v-for="item in options1" :key="item.value1" :label="item.label" :value="item.value1" />
                    </el-select>
                </el-row>
                <el-row style="margin: 10px 0px;">
                    <el-select v-model="value1" placeholder="headers" size="large" style="width: 100%;">
                        <el-option v-for="item in options1" :key="item.value1" :label="item.label" :value="item.value1" />
                    </el-select>
                </el-row>
                <el-row style="margin: 10px 0px;">
                    <el-select v-model="value1" placeholder="body" size="large" style="width: 100%;">
                        <el-option v-for="item in options1" :key="item.value1" :label="item.label" :value="item.value1" />
                    </el-select>
                </el-row>
                <el-row style="font-size: 20px;margin-top: 30px;">Test the parameters</el-row>
                <el-row style="font-size: 15px;">Before proceeding, you need to test the parameters whether they can fetch
                    API response. Please input sample text and press the Test button.</el-row>
                <el-row style="margin:10px 0px;">
                    <el-input v-model:method="method" placeholder="Sample Text" size="large" clearable
                        @change=""></el-input>
                </el-row>
                <el-row style="font-size: 20px;margin-top: 30px;">Response</el-row>
                <el-input v-model:method="method" placeholder="[]" size="large" clearable @change=""></el-input>
            </el-card>
            <el-card v-if="cardNumber == 3" style="margin-top: 20px;">
                <el-row style="font-size: 20px;">Set mapping template</el-row>
                <el-row style="font-size: 15px;">Now, you can successfuly fetch the API response. Next, you need to convert
                    API response to doccano format with the mapping template.</el-row>
                <el-row style="font-size: 20px; margin-top: 20px;">Response</el-row>
                <el-input v-model:method="method" placeholder="[]" size="large" clearable @change=""></el-input>
                <el-row style="font-size: 20px; margin-top: 20px;">doccano format</el-row>
                <el-input v-model:method="method" placeholder="[]" size="large" clearable @change=""></el-input>
                <el-row style="font-size: 20px;margin-top: 20px;">Mapping template</el-row>
                <el-row style="font-size: 15px;">You can set mapping template(Jinja2 format) to convert API response to
                    doccano format. In the template, you can refer to the API response by the input variable. If you want to
                    know the Jinja2 notation, please refer to the site.</el-row>
                <el-input v-model:method="method" type="textarea" :rows='6' placeholder="Mapping Template" clearable
                    @change="" style="margin: 20px 0px;"></el-input>
                <el-row style="font-size: 20px; margin-top: 20px;">Result</el-row>
                <el-input v-model:method="method" placeholder="[]" size="large" clearable @change=""></el-input>
            </el-card>
            <el-card v-if="cardNumber == 4" style="margin-top: 20px;">
                <el-row style="font-size: 20px;">Configure label mappings</el-row>
                <el-row style="font-size: 15px;">Once you fetch the API response, you need to convert the label in the
                    response into the one which you defined at the label page.</el-row>
                <el-row style="font-size: 20px; margin-top: 20px;">Response</el-row>
                <el-input v-model:method="method" placeholder="[]" size="large" clearable @change=""></el-input>
                <el-button type="primary" style="margin: 20px 0px;">Add</el-button>
                <el-table border>
                    <el-table-column label="From" />
                    <el-table-column label="To" />
                    <el-table-column label="Actions" />
                </el-table>
                <el-pagination v-model:current-page="currentPage4" v-model:page-size="pageSize4"
                    :page-sizes="[5, 10, 20, 30]" :small="small" :disabled="disabled" :background="background"
                    layout="prev, pager, next, jumper,->,total, sizes" :total="50" style="margin: 20px 0px;" />
                <el-row style="font-size: 20px; margin-top: 20px;">Response</el-row>
                <el-input v-model:method="method" placeholder="[]" size="large" clearable @change=""></el-input>
            </el-card>
            <el-row style="display: flex;justify-content: flex-end;">
                <el-button type="primary" style="margin-top: 12px" @click="prev">Prev</el-button>
                <el-button type="primary" style="margin-top: 12px" @click="next">Next step</el-button>
            </el-row>
        </el-dialog>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { TabsPaneContext } from 'element-plus'
const dialogTableVisible = ref(false)
const activeName = ref('second')
const cardNumber = ref(1)
const handleClick = (tab: TabsPaneContext, event: Event) => {
    console.log(tab, event)
}
const active = ref(1)

const next = () => {
    if (cardNumber.value == 4) {
        dialogTableVisible.value = false
        //连接接口，上传数据
    }
    active.value++
    cardNumber.value++
}
const prev = () => {
    if (cardNumber.value == 1) {

        //prev按钮应该被禁用
    }
    active.value--
    cardNumber.value--
}
//选模型假数据
const value1 = ref('')
const value2 = ref('')
const options1 = [
    {
        value1: 'Option1',
        label: 'SquenceLabeling',
    },
    {
        value1: 'Option2',
        label: 'SquenceLabeling',
    },
    {
        value1: 'Option3',
        label: 'SquenceLabeling',
    }
]
const options2 = [
    {
        value2: 'Option1',
        label: 'bert',
    },
    {
        value2: 'Option2',
        label: 'gpt',
    },
    {
        value2: 'Option3',
        label: 'xinghuo',
    }
]
const url = ref('')
const method = ref('')

//第4页 分页器
const currentPage4 = ref(4)
const pageSize4 = ref(100)
const small = ref(false)
const background = ref(false)
const disabled = ref(false)
</script>

<style scoped lang="less">
.demo-tabs>.el-tabs__content {
    padding: 32px;
    color: #6b778c;
    font-size: 32px;
    font-weight: 600;
}
</style>