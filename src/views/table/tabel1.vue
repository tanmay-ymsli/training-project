<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';
import { useApi } from '@/composables/useApi';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'tabel1',
});

const form = ref();
const dataTable = ref();
const viy2InputBox_UGBZh = ref();
const viy2InputNumber_UGGdV = ref();
const viy2DateTimePicker_UGMpZ = ref();
const addBtn = ref();
const delBtn = ref();

const formData = reactive({
  fullNameInput: '', salaryInput: undefined, dojInput: '',
});

const dataTableEditConfig = reactive({
  trigger: 'click',

});

const dataTableMouseConfig = reactive({

  extension: true,

});

const dataTableRowConfig = reactive({
  isCurrent: true,
});

const tableContentApi = useApi({
  method: 'post',
  localData: [
    {
      fullName: 'Tanmay Maheshwari',
      salary: 65000,
      doj: '2021-06-15',
    },
    {
      fullName: 'Ananya Sharma',
      salary: 72000,
      doj: '2020-03-12',
    },
    {
      fullName: 'Rohit Verma',
      salary: 58000,
      doj: '2022-09-01',
    },
    {
      fullName: 'Neha Gupta',
      salary: 81000,
      doj: '2019-11-25',
    },
    {
      fullName: 'Arjun Singh',
      salary: 60000,
      doj: '2023-02-10',
    },
  ],

}, {
  manual: true,
});
const tableContent = tableContentApi.data;

const dataTableFullNameEditRender = computed(() => {
  return {
    enabled: false,
    attrs: {

      textAlign: 'center',

    },
  };
});

const dataTableDojEditRender = computed(() => {
  return {
    enabled: false,
    attrs: {

      textAlign: 'center',

    },
  };
});

const dataTableSalaryEditRender = computed(() => {
  return {
    enabled: true,
    attrs: {

      useSeparator: true,
      textAlign: 'center',

    },
  };
});

const addBtnClick = () => {
  displayRecords();
};
const delBtnClick = () => {
  deleteRecord();
};

function displayRecords() {
  tableContentApi.runAsync();
}

function deleteRecord(name) {
  tableContent.value = tableContent.filter(obj => obj.fullName != name);
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueTable

      id="dataTable"
      ref="dataTable"

      :data="tableContent"

      :edit-config="dataTableEditConfig"
      :mouse-config="dataTableMouseConfig"
      :row-config="dataTableRowConfig"
    >
      <VueIndexColumn

        align="center"

        width="50px"

        min-width="50px"

        header-align="center"
      />

      <VueInputColumn

        :edit-render="dataTableFullNameEditRender"

        field="fullName"

        align="center"

        width="200px"

        header-align="center"

        title="Full Name"
      />
      <VueDateTimeColumn

        :edit-render="dataTableDojEditRender"

        field="doj"

        align="center"

        width="200px"

        title="Date of Joining"

        header-align="center"
      />
      <VueNumberColumn

        :edit-render="dataTableSalaryEditRender"

        field="salary"

        align="center"

        width="200px"

        title="Salary"

        header-align="center"
      />
    </VueTable>

    <VueFormItem

      label="Full Name"

      prop="fullNameInput"
    >
      <VueInput

        id="viy2InputBox_UGBZh"

        ref="viy2InputBox_UGBZh"
        v-model="formData.fullNameInput"

        data-type="string"
      />
    </VueFormItem>

    <VueFormItem

      label="Salary"

      prop="salaryInput"
    >
      <VueInputNumber

        id="viy2InputNumber_UGGdV"

        ref="viy2InputNumber_UGGdV"
        v-model="formData.salaryInput"

        :min="0"
      />
    </VueFormItem>

    <VueFormItem

      label="Date of Joining"

      prop="dojInput"
    >
      <VueDatePicker

        id="viy2DateTimePicker_UGMpZ"
        ref="viy2DateTimePicker_UGMpZ"

        v-model="formData.dojInput"
      />
    </VueFormItem>

    <VueButton id="addBtn" ref="addBtn" icon-position="left" @click="addBtnClick">
      RETRIEVE
    </VueButton>
    <VueButton id="delBtn" ref="delBtn" icon-position="left" @click="delBtnClick">
      DELETE
    </VueButton>
  </VueForm>
</template>
