<template>
  <BaseLoading v-if="isLoadingDataset" />
  <InternalPage v-else>
    <template v-slot:header>
      <HeaderFeedbackTaskComponent
        :datasetId="datasetId"
        :breadcrumbs="breadcrumbs"
      />
    </template>
    <template v-slot:page-header>
      <TopDatasetSettingsFeedbackTaskContent
        :separator="!isAdminOrOwnerRole"
        @goToDataset="goToDataset"
      />
    </template>
    <template v-slot:page-content>
      <SettingsInfoReadOnly
        v-if="!isAdminOrOwnerRole"
        :settings="datasetSetting"
      />
      <BaseTabsAndContent
        v-else
        :tabs="tabs"
        tab-size="large"
        class="settings__tabs-content"
      >
        <template v-slot="{ currentComponent }">
          <component
            :is="currentComponent"
            :key="currentComponent"
            :settings="datasetSetting"
          />
        </template>
      </BaseTabsAndContent>
    </template>
  </InternalPage>
</template>

<script>
import InternalPage from "@/layouts/InternalPage";
import { useDatasetSettingViewModel } from "./useDatasetSettingViewModel";

export default {
  name: "SettingPage",
  components: {
    InternalPage,
  },
  setup() {
    return useDatasetSettingViewModel();
  },
};
</script>

<styles lang="scss" scoped>
.settings {
  &__tabs {
    &-content {
      display: flex;
      flex-direction: column;
      height: 100%;
      min-height: 0;
      .tabs {
        flex-wrap: wrap;
      }
    }
  }
}
</styles>
