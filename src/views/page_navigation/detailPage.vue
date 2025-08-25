<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'detailPage',
});

const form = ref();

const formData = reactive({
});
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueText id="viy2Text_VdffA" ref="viy2Text_VdffA" :style="{ width: '100%', display: 'inline-block' }">
      Detail Page!
    </VueText>
    <VueText id="viy2Text_5AHLq" ref="viy2Text_5AHLq" :style="{ width: '100%', display: 'inline-block' }">
      New text area to check commit message
    </VueText>
  </VueForm>
</template>
