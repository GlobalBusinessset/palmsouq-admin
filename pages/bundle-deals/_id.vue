<template>
  <data-page
    ref="dataPage"
    set-api="setBundleDeal"
    get-api="getBundleDeal"
    empty-store-variable="allBundleDeals"
    route-name="bundle-deals"
    :name="$t('profile.dleDeal')"
    gate="bundle_deal"
    :validation-keys="['title', 'buy', 'free']"
    :result="result"
    @result="result = $event"
  >

    <template v-slot:form="{hasError}">

      <div class="input-wrapper">
        <label>{{ $t('index.title') }}</label>
        <input
          type="text"
          :placeholder="$t('index.title')"
          name="title"
          v-model="result.title"
          ref="title"
          :class="{invalid: !!!result.title && hasError}"
        >
        <span
          class="error"
          v-if="!!!result.title && hasError"
        >
          {{ $t('category.req', { type: $t('index.title')}) }}
        </span>
      </div>

      <div class="dply-felx align-start j-left inputs mlr--7-5 d-block-sm">
        <div class="input-wrapper mlr-7-5">
          <div class="flex-v-centered flex-xs">
            <span class="mr-15 mb-xs-10">{{ $t('brand.free') }}</span>
            <input
              type="number"
              step="any"
              :placeholder="$t('brand.free')"
              v-model="result.free"
              :class="{invalid: !!!result.free && hasError}"
            >
          </div>

          <span
            class="error"
            v-if="!!!result.free && hasError"
          >
            {{ $t('category.req', { type: $t('brand.freeCount')}) }}
          </span>

        </div>

        <div class="input-wrapper mlr-7-5">
          <div class="flex-v-centered flex-xs">
            <span class="mr-15 mb-xs-10">{{ $t('brand.buy') }}</span>
            <input
              type="number"
              step="any"
              :placeholder="$t('brand.buy')"
              v-model="result.buy"
              :class="{invalid: !!!result.buy && hasError}"
            >
          </div>

          <span
            class="error"
            v-if="!!!result.buy && hasError"
          >
            {{ $t('category.req', { type: $t('brand.buyCount')}) }}
          </span>

        </div>
      </div>

    </template>
  </data-page>
</template>

<script>

  import DataPage from "~/components/partials/DataPage";
  import Dropdown from "~/components/Dropdown";
  import util from "~/mixin/util";

  export default {
    name: "tax-rule",
    middleware: ['common-middleware', 'auth'],
    data() {
      return {
        result: {
          id: '',
          title: '',
          buy: 0,
          free: 0
        }
      }
    },
    mixins: [util],
    components: {
      DataPage,
      Dropdown
    },
    computed: {},
    methods: {
      dropdownSelected(data) {
        this.result.status = data.key
      },
    },
    async mounted() {
    }
  }
</script>

<style scoped>

</style>
