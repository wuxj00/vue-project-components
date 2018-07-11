<template>
<div style="width: 150px;height: 150px;margin-right: 30px">
    <progress-ring :percent="0.75" :radius="50"
                    :formatter="val => `114个`"
                    :colors="['#2ED698', '#2BD2C7', '#29CEF2']"></progress-ring>
    <div class="legend">
        <span class='legend-icon' style="background-color: #28CEEC"></span>
        <span class="legend-text">渐变环形进度圈</span>
    </div>
</div>
</template>
<script>
import ProgressRing from '@/components/progressRing';

export default {
  components: {
    ProgressRing
  }
};
</script>
<style lang="scss" scoped>
  .legend{
    position: relative;
    transform: translateY(20px);
    text-align: center;
    &-icon{
      border-radius: 5px;
      display: inline-block;
      width: 16px;
      height: 8px;
    }
    &-text{
      display: inline-block;
      font-size: 12px;
      color:#80D0F8;
    }
  }
</style>
