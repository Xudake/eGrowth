<template>
  <div>
    <a-select default-value="lucy" style="width: 120px" @change="handleChange">
      <a-select-option value="jack">
        Jack
      </a-select-option>
      <a-select-option value="lucy">
        Lucy
      </a-select-option>
      <a-select-option value="disabled" disabled>
        Disabled
      </a-select-option>
      <a-select-option value="Yiminghe">
        yiminghe
      </a-select-option>
    </a-select>
  </div>
</template>

<script>
export default {
  name: 'SelectTitle',
  props: {
    selectData: {
      type: Array,
      default: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['巨量引擎']
      }
    },
    // 表单校验用字段
    // eslint-disable-next-line
    title: {
      type: String
    }
  },
  data () {
    return {
      content: null,
      editorOption: {
        // some quill options
      }
    }
  },
  methods: {

  },
  watch: {

  }
}
</script>

<style lang="less" scoped>

</style>
