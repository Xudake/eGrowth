<template>
  <div class="e-growth-content">
    <div class="e-growth-content-top">
        <div class="select-title">
          <a-space align="center" size="middle">
            <div class="title">视频素材管理</div>
            <a-select default-value="巨量引擎" style="width: 120px" @change="handleChange">
              <a-select-option value="巨量引擎">巨量引擎</a-select-option>
            </a-select>
          </a-space>
        </div>
        <div class="table-page-search-wrapper">
          <a-form layout="inline">
            <a-row :gutter="48">
              <a-col :md="8" :sm="24">
                <a-form-item label="素材ID">
                  <a-input placeholder=""/>
                </a-form-item>
              </a-col>
              <a-col :md="8" :sm="24">
                <a-form-item label="类型">
                  <a-select v-model="queryParam.type" placeholder="请选择" default-value="0">
                    <a-select-option value="0">全部</a-select-option>
                    <a-select-option value="1">横版视频</a-select-option>
                    <a-select-option value="2">竖版视频</a-select-option>
                  </a-select>
                </a-form-item>
              </a-col>
              <a-col :md="8" :sm="24">
                <a-form-item label="创建时间">
                  <a-range-picker v-model="queryParam.time" style="width: 100%"/>
                </a-form-item>
              </a-col>
              <a-col :md="8" :sm="24">
                <a-form-item label="关联账户">
                  <a-select v-model="queryParam.account" placeholder="请选择" default-value="0">
                    <a-select-option value="0">全部</a-select-option>
                    <a-select-option value="1">账户A12312312账户A12312312账户A12312312账户A12312312账户A12312312账户A12312312账户A12312312账户A12312312账户A12312312账户A12312312账户A12312312账户A12312312账户A12312312账户A12312312账户A12312312</a-select-option>
                    <a-select-option value="2">账户B12312312</a-select-option>
                  </a-select>
                </a-form-item>
              </a-col>
              <a-col :md="8" :sm="24">
                <a-form-item label="审核状态">
                  <a-select v-model="queryParam.status" placeholder="请选择" default-value="0">
                    <a-select-option value="0">全部</a-select-option>
                    <a-select-option value="1">待审核</a-select-option>
                    <a-select-option value="2">审核通过</a-select-option>
                    <a-select-option value="3">审核未通过</a-select-option>
                  </a-select>
                </a-form-item>
              </a-col>
              <a-col :md="8" :sm="24">
                <a-form-item label="运行状态">
                  <a-select v-model="queryParam.useStatus" placeholder="请选择" default-value="0">
                    <a-select-option value="0">全部</a-select-option>
                    <a-select-option value="1">进行中</a-select-option>
                    <a-select-option value="2">暂停</a-select-option>
                  </a-select>
                </a-form-item>
              </a-col>
              <a-col :md="24" :sm="24">
                <!-- <span class="table-page-search-submitButtons" :style="{ float: 'left', overflow: 'hidden' }">
                  <a-button type="primary"><a-icon type="upload"/>上传视频</a-button>
                  <a-button type="primary" style="margin-left: 12px" :disabled="true">批量删除</a-button>
                </span> -->
                <span class="table-page-search-submitButtons" :style="{ float: 'right', overflow: 'hidden' }">
                  <a-button type="primary">查询</a-button>
                  <a-button style="margin-left: 12px">重置</a-button>
                </span>
              </a-col>
            </a-row>
          </a-form>
        </div>
    </div>
    <a-card :bordered="false" style="margin-top: 20px">
      <div :style="{'margin-bottom': '20px' }">
        <a-button type="primary"><a-icon type="plus"/>上传视频</a-button>
        <a-button type="primary" style="margin-left: 12px" :disabled="true">批量删除</a-button>
      </div>
      <a-table
        :columns="columns"
        :data-source="data"
        :row-key="record => record.id"
        :loading="loading"
        @change="handleTableChange"
        :row-selection="rowSelection"
        bordered>
        <div slot="videoImage" slot-scope="record">
          <div class="table-video-img" :style="{'background-image': 'url(' + record.videoImage + ')'}">
            <a-icon type="play-circle" :style="{'position': 'relative'}"/>
          </div>
        </div>
        <span slot="action">
          <a>暂停使用</a>
          <a-divider type="vertical" />
          <a>账户关联</a>
          <a-divider type="vertical" />
          <a>删除</a>
        </span>
      </a-table>
    </a-card>
  </div>
</template>

<script>
const columns = [
  {
    title: '视频',
    scopedSlots: { customRender: 'videoImage' }
    // dataIndex: 'videoImage'
  },
  {
    title: '审核状态',
    dataIndex: 'status'
  },
  {
    title: '状态',
    dataIndex: 'useStatus'
  },
  {
    title: '视频ID',
    dataIndex: 'id',
    sorter: (a, b) => a.id - b.id
  },
  {
    title: '来源',
    dataIndex: 'come'
  },
  {
    title: '类型',
    dataIndex: 'type'
  },
  {
    title: '时长',
    dataIndex: 'time'
  },
  {
    title: '创建时间',
    dataIndex: 'createTime'
  },
  {
    title: '关联账户',
    dataIndex: 'account'
  },
  {
    title: '格式',
    dataIndex: 'video'
  },
  {
    title: '质量',
    dataIndex: 'size'
  },
  {
    title: '操作',
    scopedSlots: { customRender: 'action' },
    width: '200px'
  }
]
const data = [
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 1,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  },
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 2,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  },
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 3,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  },
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 4,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  },
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 5,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  },
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 6,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  },
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 7,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  },
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 8,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  },
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 9,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  },
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 10,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  },
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 11,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  },
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 12,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  },
  {
    videoImage: 'https://f.yhres.com/lianhua/1118/banner3.jpg',
    status: 1,
    useStatus: 2,
    id: 13,
    come: 'come',
    type: 'type',
    time: 'time',
    createTime: 'createTime',
    account: 'account',
    video: 'video',
    size: 'size'
  }
]

const rowSelection = {
  onChange: (selectedRowKeys, selectedRows) => {
    console.log(`selectedRowKeys: ${selectedRowKeys}`, 'selectedRows: ', selectedRows)
  },
  onSelect: (record, selected, selectedRows) => {
    console.log(record, selected, selectedRows)
  },
  onSelectAll: (selected, selectedRows, changeRows) => {
    console.log(selected, selectedRows, changeRows)
  }
}

export default {
  name: 'MaterialVideo',
  data () {
      return {
        queryParam: {},
        columns,
        rowSelection,
        data: [],
        loading: true
      }
  },
  mounted () {
    setTimeout(() => {
      this.data = data
      this.loading = false
    }, 5000)
  },
  methods: {
    handleChange (value) {
      console.log(value)
    },
    handleTableChange (pagination, filters, sorter) {
      console.log(pagination)
    }
  }
}
</script>

<style lang="less" scoped>
  .e-growth-content {
      // background-color: #fff;
      border-radius: 4px;
      // padding: 25px 20px;

      .e-growth-content-top {
        background-color: #fff;
        border-radius: 4px;
        padding: 24px 24px 0;
      }

      .select-title {
        margin-bottom: 30PX;
        .title {
          font-size: 16px;
          font-weight: bold;
          color: #000;
        }
      }
  }

  .table-video-img {
    width: 100px;
    height: 50px;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center center;
    background-color: #ccc;
    border-radius: 4px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    font-size: 26px;
    cursor: pointer;
    &::before {
      content: '';
      position: absolute;
      width: 100%;
      height: 100%;
      background-color: rgba(255,255,255,0.5);
    }
  }
</style>
