<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

import categoryPopupComp from '/src/views/parent-child/valueListChild.vue';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'valueListParent',
});

const form = ref();
const category = ref();

const formData = reactive({
  category: '',
});

const categorySelect = (selectedObject) => {
  const fullName = `${selectedObject.firstName} ${selectedObject.lastName}`;
  console.log(fullName);
};
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      label="Category"

      prop="category"
    >
      <VueValueList

        id="category"

        ref="category"

        v-model="formData.category"

        popup-type="dialog"
        dialog-width="500"

        :use-popup="true"

        :popup-component="categoryPopupComp"

        @select="categorySelect"
      />
    </VueFormItem>
  </VueForm>
</template>
