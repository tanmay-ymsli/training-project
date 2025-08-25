<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

const router = useRouter();

defineOptions({
  name: 'headerPage',
});

const form = ref();
const openDetailsPageBtn = ref();

const formData = reactive({
});

const openDetailsPageBtnClick = () => {
  openDetailsPage();
};

function openDetailsPage() {
  router.push('detailPage');
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueButton id="openDetailsPageBtn" ref="openDetailsPageBtn" icon-position="left" @click="openDetailsPageBtnClick">
      Open Details
    </VueButton>
  </VueForm>
</template>
