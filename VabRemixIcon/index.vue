<template>
  <div
    v-if="isExternal"
    :style="styleExternalIcon"
    class="svg-external-icon svg-icon"
    v-on="$listeners"
  />
  <svg v-else :class="svgClass" aria-hidden="true" v-on="$listeners">
    <use :xlink:href="iconName" />
  </svg>
</template>

<script>
  import { isExternal } from '@/utils/validate'

  export default {
    name: 'VabRemixIcon',
    props: {
      iconClass: {
        type: String,
        required: true,
      },
      className: {
        type: String,
        default: '',
      },
    },
    computed: {
      isExternal() {
        return isExternal(this.iconClass)
      },
      iconName() {
        return `#remix-icon-${this.iconClass}`
      },
      svgClass() {
        if (this.className) {
          return 'svg-icon ' + this.className
        } else {
          return 'svg-icon'
        }
      },
      styleExternalIcon() {
        return {
          mask: `url(${this.iconClass}) no-repeat 50% 50%`,
          '-webkit-mask': `url(${this.iconClass}) no-repeat 50% 50%`,
        }
      },
    },
  }
</script>

<style lang="scss" scoped>
  .svg-icon {
    width: 1.125em;
    height: 1.125em;
    overflow: hidden;
    fill: currentColor;

    &:hover {
      opacity: 0.8;
    }
  }

  .svg-external-icon {
    display: inline-block;
    background-color: currentColor;
    mask-size: cover !important;
  }
</style>
