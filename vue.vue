<template>
  <div class="myContainer">
    <div class="myConter">
      <a-col class="gutter-row" :span="24">
        <div class="myDiv">
          <a-table :columns="columns" :dataSource="idc_list">
            <template slot="manage" slot-scope="text, record">
              <a-icon
                type="edit"
                class="icon"
                @click="showDrawerUpdate(
                      record.key,
                      record.name,
                      record.remarks
                  )"
              />
            </template>
          </a-table>
        </div>
      </a-col>
    </div>

    <a-drawer
      title="修改机房信息"
      :width="350"
      @close="onCloseUpdate"
      :visible="visible_update"
      :wrapStyle="{height: 'calc(100% - 108px)',overflow: 'auto',paddingBottom: '108px'}"
    >
      <a-form :form="formUpdate" layout="vertical" @submit="handleSubmitUpdate">
        <a-row :gutter="16">
          <a-col :span="24">
            <a-form-item label="机房名称">
              <a-input
                v-decorator="['idc_name', {
                  initialValue:def_name,
                  rules: [{ required: true, message: '请输入机房名称' }]
                }]"
                placeholder="请输入机房名称"
              />
            </a-form-item>
          </a-col>
          <a-col :span="24">
            <a-form-item label="备注">
              <a-input
                v-decorator="['remarks', {
                  initialValue:def_remarks,
                  rules: [{ required: true, message: '请输入备注' }]
                }]"
                placeholder="请输入备注"
              />
            </a-form-item>
          </a-col>
        </a-row>
        <div
          :style="{
          position: 'absolute',
          left: 0,
          bottom: 0,
          width: '100%',
          borderTop: '1px solid #e9e9e9',
          padding: '10px 16px',
          background: '#fff',
          textAlign: 'right',
        }"
        >
          <a-button :style="{marginRight: '8px'}" @click="onClose">关闭</a-button>
          <a-button type="primary" html-type="submit">修改</a-button>
        </div>
      </a-form>
    </a-drawer>
  </div>
</template>

<script>
const columns = [
  {
    title: "机房名称",
    dataIndex: "name"
  },
  {
    title: "备注",
    dataIndex: "remarks"
  },
  {
    title: "",
    dataIndex: "operation",
    scopedSlots: { customRender: "manage" },
    width: "6%"
  }
];

export default {
  name: "assetsRoom",
  data() {
    return {
      idc_list: [],
      columns,
      is_loading: false,
      formUpdate: this.$form.createForm(this),
      visible: false,
      visible_update: false,
      sotext: "",
      key: 0,
      def_name: "",
      def_remarks: ""
    };
  },
  mounted() {
    this.onLoad();
  },
  methods: {
    onLoad(search = "", curr_page = 1) {
      this.is_loading = true;

      this.idc_list = [
        {
          key: 1,
          name: "xxx1",
          remarks: "xxxx2"
        },
        {
          key: 2,
          name: "aaaa1",
          remarks: "aaaa2"
        },
        {
          key: 3,
          name: "cccc1",
          remarks: "ccc2"
        },
        {
          key: 4,
          name: "eeee1",
          remarks: "eeee2"
        }
      ];

      this.is_loading = false;
    },
    so() {
      this.onLoad(this.sotext, 1);
    },
    showDrawer() {
      this.visible = true;
    },
    onClose() {
      this.visible = false;
    },
    showDrawerUpdate(key, name, remarks) {
      this.def_name = name;
      this.def_remarks = remarks;
      this.key = key;

      this.visible_update = true;
    },
    onCloseUpdate() {
      this.visible_update = false;
    }
  }
};
</script>

<style scoped>
th.column-money,
td.column-money {
  text-align: right !important;
}
</style>
