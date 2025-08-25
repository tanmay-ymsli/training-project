<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

import childSubpagePage from '/src/views/parent-child/child.vue';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'parent',
});

const form = ref();
const parenttext = ref();
const childSubpage = ref();

const formData = reactive({
  parenttext: '',
});

function onChildDataCapture(event) {
  console.log(event);
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      label="Parent Input"

      prop="parenttext"
    >
      <VueInput

        id="parenttext"

        ref="parenttext"
        v-model="formData.parenttext"

        data-type="string"
      />
    </VueFormItem>

    <childSubpagePage

      id="childSubpage"
      ref="childSubpage"

      last-name-parent="Maheshwari"

      :parent-input="formData.parenttext"
      @on-child-emit="onChildDataCapture"
    />
  </VueForm>
</template>
