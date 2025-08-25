<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';
import { useApi } from '@/composables/useApi';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'form1',
});

const form = ref();
const fname = ref();
const lname = ref();
const textarea = ref();
const numberpick = ref();
const calendar = ref();
const apitest = ref();
const position = ref();
const checkbox = ref();
const printBtn = ref();
const setBtn = ref();

const formData = reactive({
  firstName: '', lastName: '', textarea: '', number: undefined, datepicker: '', apitest: '', position: '', checkbox: [],
});

const apicallApi = useApi({
  url: 'https://api.sampleapis.com/coffee/hot',
  method: 'get',
  responseType: 'json',
  		      contentType: 'application/json',

});
const apicall = apicallApi.data;
const apitestcallApi = useApi({
  url: 'https://api.sampleapis.com/coffee/hot',
  method: 'get',
  responseType: 'json',

});
const apitestcall = apitestcallApi.data;
const pageDataSet_GsGGt_OG8NAApi = useApi({
  method: 'post',
  localData: [
    { stored: 'A', display: 'Attack' },
    { stored: 'M', display: 'Midfield' },
    { stored: 'D', display: 'Defense' },
  ],

});
const pageDataSet_GsGGt_OG8NA = pageDataSet_GsGGt_OG8NAApi.data;
const positionDatasetApi = useApi({
  method: 'post',
  localData: [
    { stored: 'A', display: 'Attack' },
    { stored: 'M', display: 'Midfield' },
    { stored: 'D', display: 'Defense' },
  ],

});
const positionDataset = positionDatasetApi.data;

const printBtnClick = () => {
  printFormData();
};
const setBtnClick = () => {
  formData.firstName = 'Hello';
  formData.lastName = 'World';
};

function printFormData() {
  console.log(formData.firstName);
  console.log(formData.lastName);
  console.log(formData.position);
  console.log(formData.checkbox);
}

const arr = [
  {
    id: '1',
    value: 'one',
  },
  {
    id: '2',
    value: 'two',
  },
];
const arr2 = [
  {
    id: '3',
    value: 'three',
  },
  {
    id: '4',
    value: 'four',
  },
];
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      :label="t('label.firstName')"

      prop="firstName"
    >
      <VueInput

        id="fname"

        ref="fname"

        v-model="formData.firstName"

        data-type="string"
        :autofocus="true"

        :clearable="true"
      />
    </VueFormItem>

    <VueFormItem

      :label="t('label.lastName')"

      prop="lastName"
    >
      <VueInput

        id="lname"

        ref="lname"
        v-model="formData.lastName"

        data-type="string"
      />
    </VueFormItem>

    <VueFormItem

      label="Text Area"

      prop="textarea"
    >
      <VueInput
        id="textarea"

        ref="textarea"
        v-model="formData.textarea"

        type="textarea"
      />
    </VueFormItem>

    <VueFormItem

      label="Number"

      prop="number"
    >
      <VueInputNumber

        id="numberpick"
        ref="numberpick"

        v-model="formData.number"
      />
    </VueFormItem>

    <VueFormItem

      label="Calendar"

      prop="datepicker"
    >
      <VueDatePicker

        id="calendar"
        ref="calendar"

        v-model="formData.datepicker"
      />
    </VueFormItem>

    <VueFormItem

      label="apitest"

      prop="apitest"
    >
      <VueRadioGroup

        id="apitest"

        ref="apitest"
        v-model="formData.apitest"

        direction="horizontal"

        split-size="default"
      >
        <VueRadio
          v-for="option in apitestcall"
          :key="option.id"
          :label="option.id"
          :name="option.name"
          :disabled="option.disabled"
        >
          {{ option.title }}
        </VueRadio>
      </VueRadioGroup>
    </VueFormItem>

    <VueFormItem

      label="Position"

      prop="position"
    >
      <VueRadioGroup

        id="position"

        ref="position"
        v-model="formData.position"

        direction="horizontal"

        split-size="default"
      >
        <VueRadio
          v-for="option in positionDataset"
          :key="option.stored"
          :label="option.stored"
          :name="option.name"
          :disabled="option.disabled"
        >
          {{ option.display }}
        </VueRadio>
      </VueRadioGroup>
    </VueFormItem>

    <VueFormItem

      label="Checkbox"

      prop="checkbox"
    >
      <VueCheckboxGroup

        id="checkbox"
        ref="checkbox"

        v-model="formData.checkbox"

        split-size="default"
      >
        <VueCheckbox
          v-for="option in positionDataset"
          :key="option.stored"
          :label="option.stored"
          :name="option.name"
          :disabled="option.disabled"
          :border="true"
        >
          {{ option.display }}
        </VueCheckbox>
      </VueCheckboxGroup>
    </VueFormItem>

    <VueButton id="printBtn" ref="printBtn" icon-position="left" @click="printBtnClick">
      Print
    </VueButton>
    <VueButton id="setBtn" ref="setBtn" icon-position="left" @click="setBtnClick">
      Set
    </VueButton>
  </VueForm>
</template>
