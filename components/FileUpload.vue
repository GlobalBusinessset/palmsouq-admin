<template>
  <div class="file-wrapper" :class="{ 'has-error': uploadMessage }">
    <div :style="imageWrapStyle">
      <div :style="imageContainerStyle" class="file-input">
        <input
          type="file"
          accept="image/*"
          @change="fileChanged"
          ref="fileInput"
        />

        <img
          style="width: 100%"
          v-if="!fileUploading"
          :src="previewImageUrl"
          :alt="imageTitle"
          @error="onError"
        />
      </div>

      <span v-if="uploadMessage" class="error mb-10">
        {{ uploadMessage }}
      </span>
    </div>

    <ajax-button
      class="w-100"
      :class="`${btnType}-btn`"
      type="button"
      color="primary"
      :text="btnText"
      :only-icon="onlyIcon"
      :fetching-data="fileUploading"
      @clicked="$refs.fileInput.click()"
    />
  </div>
</template>

<script>
import AjaxButton from "~/components/AjaxButton";
import util from "~/mixin/util";
import validation from "~/mixin/validation";
import LazyImage from "./LazyImage";

export default {
  name: "FileUpload",
  data() {
    return {
      uploadMessage: null,
    };
  },
  mixins: [util, validation],
  components: {
    LazyImage,
    AjaxButton,
  },
  props: {
    btnType: {
      type: String,
      default: "outline",
    },
    fileUploading: {
      type: Boolean,
      default: false,
    },
    imageUrl: {
      type: String,
      default: "",
    },
    image: {
      type: String,
      default: "",
    },
    imageTitle: {
      type: String,
      default: "",
    },
    onlyIcon: {
      type: String,
      default: null,
    },
    imageWrapStyle: {
      type: [Object, Array],
      default: null,
    },
    imageContainerStyle: {
      type: [Object, Array],
      default: null,
    },
    btnText: {
      type: String,
      default: function () {
        return this.$t("profile.upload");
      },
    },
  },
  computed: {
    previewImageUrl() {
      return this.imageUrl || this.getImageURL(this.imageName) || "";
    },
    imageName() {
      if (this.image?.trim()) {
        return this.image;
      }
      return this.defaultImage;
    },
  },
  methods: {
    fileChanged(event) {
      const file = event.target.files[0];
      if (file) {
        this.uploadMessage = this.isValidImage(file);
        if (!this.uploadMessage) {
          this.$emit("file-upload", file);
        }
      }
    },
    onError(e) {

      e.target.src = this.getImageURL()
    },
  },
};
</script>

<style lang="stylus"></style>
