<template>
  <data-page
    ref="dataPage"
    set-api="setProductCollection"
    get-api="getProductCollection"
    route-name="product-collections"
    empty-store-variable="allProductCollections"
    :name="$t('dataPage.prodCol')"
    :validation-keys="['title', 'slug']"
    :result="result"
    gate="product_collection"
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
          @change="slugChange"
          :class="{invalid: !!!result.title && hasError}"
        >
        <span
          class="error"
          v-if="!!!result.title && hasError"
        >
          {{ $t('category.req', { type: $t('index.title')}) }}
        </span>
      </div>

      <div class="input-wrapper">
        <label>{{ $t('category.slug') }}</label>
        <input
          type="text"
          :placeholder="$t('category.slug')"
          name="slug"
          v-model="result.slug"
          ref="slug"
          :class="{invalid: !!!result.slug && hasError}"
        >
        <span
          class="error"
          v-if="!!!result.slug && hasError"
        >
          {{ $t('category.req', { type: $t('category.slug')}) }}
        </span>
      </div>


      <div class="input-wrapper">
        <div class="dply-felx j-left mb-20 mb-sm-15">
            <span class="mr-15">
               {{ $t('category.status') }}
            </span>

          <dropdown
            :selectedKey="`${result.status}`"
            :options="statusObj"
            @clicked="dropdownSelected"
          />
        </div>
      </div>
    </template>
  </data-page>
</template>

<script>

  import DataPage from "~/components/partials/DataPage";
  import Dropdown from "~/components/Dropdown";
  import util from "~/mixin/util";
  import {mapGetters} from 'vuex'

  export default {
    name: "tax-rule",
    middleware: ['common-middleware', 'auth'],
    data() {
      return {
        result: {
          id: '',
          title: '',
          slug: '',
          status: 2
        }
      }
    },
    mixins: [util],
    components: {
      DataPage,
      Dropdown
    },
    computed: {
      ...mapGetters('language', ['currentLanguage']),
    },
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
