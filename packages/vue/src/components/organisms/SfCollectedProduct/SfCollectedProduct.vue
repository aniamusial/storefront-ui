<template>
  <div class="sf-collected-product">
    <slot name="remove" v-bind="{ removeHandler }">
      <SfCircleIcon
        icon="cross"
        class="sf-circle-icon--small sf-collected-product__remove sf-collected-product__remove--circle-icon"
        @click="removeHandler"
      />
      <SfButton
        class="sf-button--text sf-collected-product__remove sf-collected-product__remove--text"
        @click="removeHandler"
        >Remove</SfButton
      >
    </slot>
    <slot name="more-actions">
      <SfIcon
        icon="more"
        role="button"
        class="sf-collected-product__more-actions mobile-only"
      />
    </slot>
    <div class="sf-collected-product__aside">
      <slot name="image" v-bind="{ image, title }">
        <SfImage
          :src="image"
          :alt="title"
          :width="imageWidth"
          :height="imageHeight"
          class="sf-collected-product__image"
        />
      </slot>
      <slot name="input">
        <div class="sf-collected-product__quantity-wrapper">
          <SfQuantitySelector
            :qty="qty"
            class="sf-collected-product__quantity-selector"
            @input="$emit('input', $event)"
          />
        </div>
      </slot>
    </div>
    <div class="sf-collected-product__main">
      <div class="sf-collected-product__details">
        <slot name="title" v-bind="{ title }">
          <div class="sf-collected-product__title">{{ title }}</div>
        </slot>
        <slot name="price" v-bind="{ specialPrice, regularPrice }">
          <SfPrice
            v-if="regularPrice"
            :regular="regularPrice"
            :special="specialPrice"
          />
        </slot>
        <slot name="configuration" />
      </div>
      <div class="sf-collected-product__actions">
        <slot name="actions" />
      </div>
    </div>
  </div>
</template>
<script>
import SfPrice from "../../atoms/SfPrice/SfPrice.vue";
import SfIcon from "../../atoms/SfIcon/SfIcon.vue";
import SfImage from "../../atoms/SfImage/SfImage.vue";
import SfCircleIcon from "../../atoms/SfCircleIcon/SfCircleIcon.vue";
import SfButton from "../../atoms/SfButton/SfButton.vue";
import SfQuantitySelector from "../../atoms/SfQuantitySelector/SfQuantitySelector.vue";
export default {
  name: "SfCollectedProduct",
  components: {
    SfButton,
    SfIcon,
    SfImage,
    SfCircleIcon,
    SfPrice,
    SfQuantitySelector
  },
  model: {
    prop: "qty"
  },
  props: {
    /**
     * Product image
     * It should be an url of the product
     */
    image: {
      type: [String, Object],
      default: ""
    },
    /**
     * Product image width, without unit
     */
    imageWidth: {
      type: [String, Number],
      default: 140
    },
    /**
     * Product image height, without unit
     */
    imageHeight: {
      type: [String, Number],
      default: 200
    },
    /**
     * Product title
     */
    title: {
      type: String,
      default: ""
    },
    /**
     * Product regular price
     */
    regularPrice: {
      type: [Number, String],
      default: null
    },
    /**
     * Product special price
     */
    specialPrice: {
      type: [Number, String],
      default: null
    },
    /**
     * Selected quantity
     */
    qty: {
      type: [Number, String],
      default: 1
    }
  },
  methods: {
    removeHandler() {
      this.$emit("click:remove");
    }
  }
};
</script>
<style lang="scss">
@import "~@storefront-ui/shared/styles/components/organisms/SfCollectedProduct.scss";
</style>
