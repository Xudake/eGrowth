<template>
  <div class="e-growth-content">
    <div class="select-title">
      <a-space align="center" size="middle">
        <a-select default-value="巨量引擎" style="width: 120px" @change="handleChange">
          <a-select-option value="巨量引擎">巨量引擎</a-select-option>
        </a-select>
        <div class="title">视频素材管理</div>
      </a-space>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MaterialVideo',
  data () {
      return {
      }
  },
  methods: {
    handleChange (value) {
      console.log(value)
    }
  }
}
</script>

<style lang="less" scoped>
  .e-growth-content {
      background-color: #fff;
      border-radius: 4px;
      padding: 25px 20px;
      .select-title {
        .title {
          font-size: 16px;
          font-weight: bold;
          color: #000;
        }
      }
  }
</style>
