<template>
  <svg :class="[prefixCls, $attrs.class]" :style="getStyle" aria-hidden="true">
    <use :xlink:href="symbolId" />
  </svg>
</template>
<script lang="ts">
  import type { CSSProperties } from 'vue';
  import { defineComponent, computed } from 'vue';
  import { useDesign } from '/@/hooks/web/useDesign';

  export default defineComponent({
    name: 'SvgIcon',
    props: {
      prefix: {
        type: String,
        default: 'icon',
      },
      name: {
        type: String,
        required: true,
      },
      size: {
        type: [Number, String],
        default: 16,
      },
    },
    setup(props) {
      const { prefixCls } = useDesign('svg-icon');
      const symbolId = computed(() => `#${props.prefix}-${props.name}`);

      const getStyle = computed(
        (): CSSProperties => {
          const { size } = props;
          let s = `${size}`;
          s = `${s.replace('px', '')}px`;
          return {
            width: s,
            height: s,
          };
        }
      );
      return { symbolId, prefixCls, getStyle };
    },
  });
</script>
<style lang="less" scoped>
  @prefix-cls: ~'@{namespace}-svg-icon';

  .@{prefix-cls} {
    overflow: hidden;
    vertical-align: -0.15em;
    fill: currentColor;
  }
</style>
