### 1.使用Checkbox多选框循环遍历（动态生成）

#### 1.1 效果

![image-20220613170047389](https://gitee.com/v876774538/my-img/raw/master/image-20220613170047389.png)

#### 1.2 解释

![image-20220630111156506](https://gitee.com/v876774538/my-img/raw/master/image-20220630111156506.png)

![image-20220630111232929](https://gitee.com/v876774538/my-img/raw/master/image-20220630111232929.png)

![image-20220630111305040](https://gitee.com/v876774538/my-img/raw/master/image-20220630111305040.png)

![image-20220630111331352](https://gitee.com/v876774538/my-img/raw/master/image-20220630111331352.png)

![image-20220630111341686](https://gitee.com/v876774538/my-img/raw/master/image-20220630111341686.png)

#### 1.3 具体代码

```vue
<template>
  <div class="index">
    <a-card title="店铺权限" :bordered="false" class="card">
      <a-form :form="form">
        <a-row>
          <a-checkbox :checked="checkAll()" v-model="isAll" @change="handleAll"> 全部店铺 </a-checkbox>
        </a-row>
        <a-row v-for="(item, index) in storeList" :key="index">
          <a-form-item>
            <a-checkbox :checked="checkAll(index)" v-model="item.checked" @change="handleChangeAll($event, index)">
              {{ item.label }}
            </a-checkbox>
            <a-row class="checkboxGroup">
              <a-checkbox
                v-for="(item, index) in item.children"
                :key="index"
                :checked="item.checked"
                v-model="item.checked"
                @change="handleChangeBox()"
                class="checkbox"
              >
                {{ item.label }}
              </a-checkbox>
            </a-row>
          </a-form-item>
          <a-divider v-if="index != storeList.length - 1" />
        </a-row>
      </a-form>
    </a-card>
  </div>
</template>

<script>

const storeList = [
  {
    id: 0,
    parentId: null,
    label: 'Qoo10店铺',
    checked: false,
    children: [
      {
        id: 0,
        label: 'Qoo10一店',
        parentId: 0,
        checked: false,
        children: null,
      },
      {
        id: 1,
        label: 'Qoo10二店',
        parentId: 0,
        checked: false,
        children: null,
      },
      {
        id: 2,
        label: 'Qoo10三店',
        parentId: 0,
        checked: false,
        children: null,
      },
    ],
  },
  {
    id: 1,
    parentId: null,
    label: 'Rakuten店铺',
    checked: false,
    children: [
      {
        id: 0,
        label: 'Rakuten一店',
        parentId: 1,
        checked: false,
        children: null,
      },
      {
        id: 1,
        label: 'Rakuten二店',
        parentId: 1,
        checked: false,
        children: null,
      },
      {
        id: 2,
        label: 'Rakuten三店',
        parentId: 1,
        checked: false,
        children: null,
      },
      {
        id: 3,
        label: 'Rakuten四店',
        parentId: 1,
        checked: false,
        children: null,
      },
    ],
  },
]

export default {
  name: 'EditBypassAccount',
  data() {
    return {
      // 店铺权限列表
      storeList,
      // 全选
      isAll: false,
    }
  },
  computed: {},
  watch: {},
  mounted() {
  },
  methods: {
    handleChangeBox() {
      console.log(this.storeList)
    },
    handleChangeAll(e, index) {
      // 全选/取消全选子店铺
      this.storeList[index].children.map((item) => {
        item.checked = e.target.checked
      })
    },
    // 反选全选
    checkAll(index) {
      let flag = true
      if (index >= 0) {
        // 判断是否所有子店铺被选中
        this.storeList[index].children.map((item) => {
          if (item.checked == false) {
            flag = false
            // 修改全选状态
            this.storeList[index].checked = flag
            return flag
          }
        })
        // 修改全选状态
        this.storeList[index].checked = flag
        return flag
      } else {
        this.storeList.map((item) => {
          if (item.checked == false) {
            flag = false
            // 修改全选状态
            this.isAll = flag
            return flag
          }
        })
        // 修改全选状态
        this.isAll = flag
        return flag
      }
    },
    handleAll(e) {
      // 全选/取消全选所有店铺
      for (var i = 0; i < this.storeList.length; i++) {
        this.storeList[i].children.map((item) => {
          item.checked = e.target.checked
        })
      }
    },
  },
}
</script>

<style lang="less" scoped>
.index {
  // 卡片
  .card {
    margin-top: 20px;
  }
  // 按钮
  .btn {
    width: 130px;
  }
  .checkboxGroup {
    margin-left: 30px;
    .checkbox {
      width: 120px;
    }
  }
}
</style>
```

### 2.表格动态合并行

#### 2.1 后端表格数据

```js
const responseSource = [
  {
    id: '1531553632599388166',
    spuCode: 'A15',
    spuImg:
      'https://axure-file.lanhuapp.com/8ca3bf46-a8c4-4b5f-9fd2-e395ff7d4ec1__44ba96da3b665644f519f398ea6db9af.svg',
    spuTitle: 'iphone16',
    remark: null,
    classificationId: '-2',
    userId: '1',
    createTime: '2022-06-14 10:53:27',
    updateTime: null,
    productSkuList: [
      {
        id: '1531553632964292613',
        skuCode: 'QWE',
        spuCode: 'A15',
        skuDetailId: null,
        spuTitle: null,
        skuAttribute: 'red*4.7',
        skuType: 2,
        price: '93',
        weight: '0.00',
        size: '0.00*31*51',
        skuImage:
          'https://axure-file.lanhuapp.com/8ca3bf46-a8c4-4b5f-9fd2-e395ff7d4ec1__44ba96da3b665644f519f398ea6db9af.svg',
        skuNumber: null,
        productSkuDetailResponseList: [
          {
            skuDetailId: 'QWE11',
            number: '1',
            skuCode: 'QWE',
            skuImage:
              'https://axure-file.lanhuapp.com/8ca3bf46-a8c4-4b5f-9fd2-e395ff7d4ec1__44ba96da3b665644f519f398ea6db9af.svg',
            skuAttribute: 'blue*5.3',
            skuType: '1',
            spuCode: 'A15',
          },
          {
            skuDetailId: 'QWE12',
            number: '1',
            skuCode: 'QWE',
            skuImage:
              'https://axure-file.lanhuapp.com/8ca3bf46-a8c4-4b5f-9fd2-e395ff7d4ec1__44ba96da3b665644f519f398ea6db9af.svg',
            skuAttribute: 'yellow*10',
            skuType: '1',
            spuCode: 'A15',
          },
        ],
      },
      {
        id: '1531553632964292614',
        skuCode: 'QWE11',
        spuCode: 'A15',
        skuDetailId: null,
        spuTitle: null,
        skuAttribute: 'blue*5.3',
        skuType: 1,
        price: '999',
        weight: '50.00',
        size: '15*10*5',
        skuImage:
          'https://axure-file.lanhuapp.com/8ca3bf46-a8c4-4b5f-9fd2-e395ff7d4ec1__44ba96da3b665644f519f398ea6db9af.svg',
        skuNumber: null,
        productSkuDetailResponseList: [],
      },
    ],
  },
  {
    id: '1531553632599388165',
    spuCode: 'A20',
    spuImg: 'http://dummyimage.com/400x400',
    spuTitle: 'iphone20',
    remark: null,
    classificationId: '23',
    userId: '1',
    createTime: '2022-06-14 10:53:23',
    updateTime: null,
    productSkuList: [
      {
        id: '1531553632964292610',
        skuCode: 'ASD',
        spuCode: 'A20',
        skuDetailId: null,
        spuTitle: null,
        skuAttribute: 'BLUE',
        skuType: 1,
        price: '96',
        weight: '44.00',
        size: '0.00*70*71',
        skuImage: 'http://dummyimage.com/400x400',
        skuNumber: null,
        productSkuDetailResponseList: [],
      },
    ],
  },
]
```

#### 2.2 二次处理表格数据

为每一项附上rowSpan（需要合并的行数）

```js
// 行合并 处理后端返回表格数据
handleResponseSource() {
  let responseSource = this.responseSource
  let arr = []
  responseSource.map((item) => {
    const len = item.productSkuList.length
    item.productSkuList.map((item1, index) => {
      arr = [
        ...arr,
        {
          spuId: item.id,
          spuImg: item.spuImg,
          spuTitle: item.spuTitle,
          spuCode: item.spuCode,
          classificationId: item.classificationId,
          createTime: item.createTime,
          updateTime: item.updateTime,
          skuId: item1.id,
          skuCode: item1.skuCode,
          skuAttribute: item1.skuAttribute,
          skuType: item1.skuType,
          price: item1.price,
          weight: item1.weight,
          size: item1.size,
          skuImage: item1.skuImage,
          productSkuDetail: item1.productSkuDetailResponseList,
          rowSpan: index === 0 ? len : 0,
          checked: false,
        },
      ]
      return arr
    })
    return arr
  })
  this.dataSource = arr.map((item, index) => {
    item.key = index
    return item
  })
  console.log('1111', this.dataSource)
},
```

处理后的数据

![image-20220622142540548](https://gitee.com/v876774538/my-img/raw/master/image-20220622142540548.png)

![image-20220622142634292](https://gitee.com/v876774538/my-img/raw/master/image-20220622142634292.png)

#### 2.3 columns

**customCell**可以和**scopedSlots**同时使用

```js
// 表头
const columns = [
  {
    dataIndex: 'checkbox',
    slots: { title: 'checkboxTitle' },
    customCell: (record) => {
      if (record.rowSpan === 0) {
        return null
      }
      const data = {
        attrs: {
          rowSpan: record.rowSpan ? record.rowSpan : 1,
        },
      }
      return data
    },
    scopedSlots: { customRender: 'checkbox' },
  },
  {
    title: 'SPU图片',
    dataIndex: 'SPUimg',
    customCell: (record) => {
      if (record.rowSpan === 0) {
        return null
      }
      const data = {
        attrs: {
          rowSpan: record.rowSpan ? record.rowSpan : 1,
        },
      }
      return data
    },
    scopedSlots: { customRender: 'SPUimage' },
  },
  {
    title: 'SPU信息',
    dataIndex: 'SPUinfo',
    customCell: (record) => {
      if (record.rowSpan === 0) {
        return null
      }
      const data = {
        attrs: {
          rowSpan: record.rowSpan ? record.rowSpan : 1,
        },
      }
      return data
    },
    scopedSlots: { customRender: 'SPUinfo' },
  },
  {
    title: 'SKU图片',
    dataIndex: 'SKUimage',
    scopedSlots: { customRender: 'SKUimage' },
  },
  {
    title: 'SKU信息',
    dataIndex: 'SKUinfo',
    scopedSlots: { customRender: 'SKUinfo' },
  },
  {
    title: '价格',
    dataIndex: 'price',
    scopedSlots: { customRender: 'price' },
  },
  {
    title: '重量（g）',
    dataIndex: 'weight',
    scopedSlots: { customRender: 'weight' },
  },
  {
    title: '尺寸（cm）',
    dataIndex: 'size',
    scopedSlots: { customRender: 'size' },
  },
  {
    title: '时间',
    dataIndex: 'time',
    scopedSlots: { customRender: 'time' },
  },
  {
    title: '操作',
    dataIndex: 'action',
    width: '130px',
    scopedSlots: { customRender: 'action' },
  },
]
```

#### 2.4 表格部分（html）

```html
<a-table
ref="table"
size="default"
:rowKey="dataSource.key"
:columns="columns"
:data-source="dataSource"
showPagination="auto"
>
<span slot="checkboxTitle">
  <a-checkbox :checked="checkAll()" v-model="isAll" @change="handleChangeAll"></a-checkbox>
</span>
<span slot="checkbox" slot-scope="text, record">
  <a-checkbox
    :checked="record.checked"
    v-model="record.checked"
    @change="handleChange($event, record.key)"
  ></a-checkbox>
</span>
<span slot="SPUimage" slot-scope="text, record">
  <template>
    <img class="image" :src="record.spuImg" alt="" />
  </template>
</span>
<span slot="SPUinfo" slot-scope="text, record">
  <template>
    <div class="box">
      <div class="row">产品标题：{{ record.spuTitle }}</div>
      <div class="row">SPU：{{ record.spuCode }}</div>
      <div class="row">分类：{{ record.classificationId }}</div>
      <div class="row">备注：{{ record.remark }}</div>
    </div>
  </template>
</span>
<span slot="SKUimage" slot-scope="text, record">
  <template>
    <img class="image" :src="record.skuImage" alt="" />
  </template>
</span>
<span slot="SKUinfo" slot-scope="text, record">
  <template>
    <div class="box">
      <div class="row">SKU：{{ record.skuCode }}</div>
      <div class="row">属性：{{ record.skuAttribute }}</div>
      <div class="row">
        SKU类型：{{ record.skuType | skuTypeFilter }}
        <a v-if="record.skuType == 2" @click="handleSKUDetailsModal(record.productSkuDetail)">详情</a>
      </div>
    </div>
  </template>
</span>
<span slot="price" slot-scope="text, record">
  <template>
    <editable-cell :text="text" @change="onCellChange(record.key, 'price', $event)" />
  </template>
</span>
<span slot="weight" slot-scope="text, record">
  <template>
    <editable-cell :text="text" @change="onCellChange(record.key, 'weight', $event)" />
  </template>
</span>
<span slot="size" slot-scope="text, record">
  <template>
    <editable-cell :text="text" @change="onCellChange(record.key, 'size', $event)" />
  </template>
</span>
<span slot="time" slot-scope="text, record">
  <template>
    <div class="box">
      <div class="row">创建时间：{{ record.createTime }}</div>
      <div class="row">更新时间：{{ record.updateTime }}</div>
    </div>
  </template>
</span>
<span slot="action" slot-scope="text, record">
  <template>
    <a-space direction="vertical">
      <a @click="handleEdit(record)">编辑</a>
      <a @click="handleSub(record)">推送</a>
      <a @click="handleSub(record)">删除</a>
      <a @click="handleSub(record)">备注</a>
    </a-space>
  </template>
</span>
</a-table>
```

#### 2.5 具体代码

```vue
<template>
  <div class="index">
    <a-row :gutter="24">
      <a-col :md="24" :lg="4">
        <a-card title="商品分类" :bordered="false">
          <a-icon slot="extra" type="setting" @click="categoryHandleAdd" />
          <a-tree
            :show-line="showLine"
            :show-icon="showIcon"
            :default-expanded-keys="['0-0-0', '0-0-1', '0-0-2']"
            @select="onSelect"
            :treeData="treeData"
            :defaultExpandAll="defaultExpandAll"
          >
          </a-tree>
        </a-card>
      </a-col>
      <a-col :md="24" :lg="20">
        <a-card :bordered="false">
          <div class="table-page-search-wrapper">
            <a-form layout="inline" :label-col="labelCol">
              <a-row :gutter="48">
                <a-col :md="24" :sm="24">
                  <a-form-item label="搜索类型">
                    <a-button :type="searchType == 1 ? 'primary' : ''" @click="searchType = 1">SKU</a-button>
                    <a-button :type="searchType == 2 ? 'primary' : ''" @click="searchType = 2">SPU</a-button>
                    <a-button :type="searchType == 3 ? 'primary' : ''" @click="searchType = 3">产品标题</a-button>
                  </a-form-item>
                </a-col>
              </a-row>
              <a-row :gutter="48">
                <a-col :md="8" :sm="24">
                  <a-form-item label="搜索">
                    <a-input v-model="queryParam.id" placeholder="" />
                  </a-form-item>
                </a-col>
                <a-col :md="4" :sm="24">
                  <a-select placeholder="请选择" default-value="0">
                    <a-select-option value="0">模糊</a-select-option>
                    <a-select-option value="1">精确</a-select-option>
                  </a-select>
                </a-col>
                <a-col :md="8" :sm="24">
                  <a-button type="primary" @click="$refs.table.refresh(true)">查询</a-button>
                </a-col>
              </a-row>
              <a-row :gutter="48">
                <a-col :md="8" :sm="24">
                  <a-form-item label="排序">
                    <a-select placeholder="请选择" default-value="0">
                      <a-select-option value="0">按创建时间</a-select-option>
                      <a-select-option value="1">按更新时间</a-select-option>
                    </a-select>
                  </a-form-item>
                </a-col>
              </a-row>
            </a-form>
          </div>
          <a-divider />
          <a-row justify="space-between">
            <a-col :span="12">
              <a-checkbox v-model="checked">显示组合SKU详情</a-checkbox>
            </a-col>
            <a-col :span="12" style="text-align: right">
              <a-space>
                <a-button type="danger" @click="handleAdd" style="margin-right: 10px">添加产品</a-button>
                <a-button type="primary" @click="handleAdd" style="margin-right: 10px">刷新列表</a-button>
                <!-- <a-button type="primary" @click="handleAdd" style="margin-right: 10px">批量操作</a-button> -->
                <a-dropdown>
                  <a-menu slot="overlay">
                    <a-menu-item key="1" @click="goPath('/product/productLibrary/bulkEdit')">批量编辑</a-menu-item>
                    <a-menu-item key="2">批量设置产品分类</a-menu-item>
                    <a-menu-item key="3">批量推送</a-menu-item>
                    <a-menu-item key="4">批量删除</a-menu-item>
                  </a-menu>
                  <a-button type="primary">批量操作</a-button>
                </a-dropdown>
                <!-- <a-button type="primary" @click="handleAdd" style="margin-right: 10px">导入数据</a-button> -->
                <a-dropdown>
                  <a-menu slot="overlay">
                    <a-menu-item key="1">导入SPU</a-menu-item>
                    <a-menu-item key="2">导入组合SKU</a-menu-item>
                  </a-menu>
                  <a-button type="primary">导入数据</a-button>
                </a-dropdown>
                <!-- <a-button type="primary" @click="handleAdd">导出数据</a-button> -->
                <a-dropdown>
                  <a-menu slot="overlay">
                    <a-menu-item key="1">导出勾选产品</a-menu-item>
                    <a-menu-item key="2">导出全部产品</a-menu-item>
                  </a-menu>
                  <a-button type="primary">导出数据</a-button>
                </a-dropdown>
              </a-space>
            </a-col>
          </a-row>
          <a-divider />
          <a-table
            ref="table"
            size="default"
            :rowKey="dataSource.key"
            :columns="columns"
            :data-source="dataSource"
            showPagination="auto"
          >
            <span slot="checkboxTitle">
              <a-checkbox :checked="checkAll()" v-model="isAll" @change="handleChangeAll"></a-checkbox>
            </span>
            <span slot="checkbox" slot-scope="text, record">
              <a-checkbox
                :checked="record.checked"
                v-model="record.checked"
                @change="handleChange($event, record.key)"
              ></a-checkbox>
            </span>
            <span slot="SPUimage" slot-scope="text, record">
              <template>
                <img class="image" :src="record.spuImg" alt="" />
              </template>
            </span>
            <span slot="SPUinfo" slot-scope="text, record">
              <template>
                <div class="box">
                  <div class="row">产品标题：{{ record.spuTitle }}</div>
                  <div class="row">SPU：{{ record.spuCode }}</div>
                  <div class="row">分类：{{ record.classificationId }}</div>
                  <div class="row">备注：{{ record.remark }}</div>
                </div>
              </template>
            </span>
            <span slot="SKUimage" slot-scope="text, record">
              <template>
                <img class="image" :src="record.skuImage" alt="" />
              </template>
            </span>
            <span slot="SKUinfo" slot-scope="text, record">
              <template>
                <div class="box">
                  <div class="row">SKU：{{ record.skuCode }}</div>
                  <div class="row">属性：{{ record.skuAttribute }}</div>
                  <div class="row">
                    SKU类型：{{ record.skuType | skuTypeFilter }}
                    <a v-if="record.skuType == 2" @click="handleSKUDetailsModal(record.productSkuDetail)">详情</a>
                  </div>
                </div>
              </template>
            </span>
            <span slot="price" slot-scope="text, record">
              <template>
                <editable-cell :text="text" @change="onCellChange(record.key, 'price', $event)" />
              </template>
            </span>
            <span slot="weight" slot-scope="text, record">
              <template>
                <editable-cell :text="text" @change="onCellChange(record.key, 'weight', $event)" />
              </template>
            </span>
            <span slot="size" slot-scope="text, record">
              <template>
                <editable-cell :text="text" @change="onCellChange(record.key, 'size', $event)" />
              </template>
            </span>
            <span slot="time" slot-scope="text, record">
              <template>
                <div class="box">
                  <div class="row">创建时间：{{ record.createTime }}</div>
                  <div class="row">更新时间：{{ record.updateTime }}</div>
                </div>
              </template>
            </span>
            <span slot="action" slot-scope="text, record">
              <template>
                <a-space direction="vertical">
                  <a @click="handleEdit(record)">编辑</a>
                  <a @click="handleSub(record)">推送</a>
                  <a @click="handleSub(record)">删除</a>
                  <a @click="handleSub(record)">备注</a>
                </a-space>
              </template>
            </span>
          </a-table>
          <!-- 弹窗 -->
          <a-modal title="组合SKU详情" v-model="showSKUDetailsModal">
            <template slot="footer">
              <a-button @click="handleSKUDetailsModalCancel">关闭</a-button>
            </template>
            <a-table size="small" :data-source="SKUDetailsList" :columns="innerColumns">
              <span slot="skuImage" slot-scope="text, record">
                <template>
                  <img class="image" :src="record.skuImage" alt="" />
                </template>
              </span>
            </a-table>
          </a-modal>
          <create-form
            ref="createModal"
            :visible="visible"
            :loading="confirmLoading"
            :model="mdl"
            :status="status"
            @cancel="handleCancel"
            @ok="handleOk"
          />

          <goods-category-Form
            ref="goodsCategoryForm"
            :visible="categoryVisible"
            :loading="categoryConfirmLoading"
            :model="categoryMdl"
            @cancel="categoryHandleCancel"
            @ok="categoryHandleOk"
          />
          <step-by-step-modal ref="modal" @ok="handleOk" />
        </a-card>
      </a-col>
    </a-row>
  </div>
</template>

<script>
import moment from 'moment'
import { STable, Ellipsis } from '@/components'
// import { getRoleList, getServiceList } from '@/api/manage'
import CreateForm from './modules/CreateForm'
import goodsCategoryForm from './modules/goodsCategoryForm.vue'

// 表头
const columns = [
  {
    dataIndex: 'checkbox',
    slots: { title: 'checkboxTitle' },
    customCell: (record) => {
      if (record.rowSpan === 0) {
        return null
      }
      const data = {
        attrs: {
          rowSpan: record.rowSpan ? record.rowSpan : 1,
        },
      }
      return data
    },
    scopedSlots: { customRender: 'checkbox' },
  },
  {
    title: 'SPU图片',
    dataIndex: 'SPUimg',
    customCell: (record) => {
      if (record.rowSpan === 0) {
        return null
      }
      const data = {
        attrs: {
          rowSpan: record.rowSpan ? record.rowSpan : 1,
        },
      }
      return data
    },
    scopedSlots: { customRender: 'SPUimage' },
  },
  {
    title: 'SPU信息',
    dataIndex: 'SPUinfo',
    customCell: (record) => {
      if (record.rowSpan === 0) {
        return null
      }
      const data = {
        attrs: {
          rowSpan: record.rowSpan ? record.rowSpan : 1,
        },
      }
      return data
    },
    scopedSlots: { customRender: 'SPUinfo' },
  },
  {
    title: 'SKU图片',
    dataIndex: 'SKUimage',
    scopedSlots: { customRender: 'SKUimage' },
  },
  {
    title: 'SKU信息',
    dataIndex: 'SKUinfo',
    scopedSlots: { customRender: 'SKUinfo' },
  },
  {
    title: '价格',
    dataIndex: 'price',
    scopedSlots: { customRender: 'price' },
  },
  {
    title: '重量（g）',
    dataIndex: 'weight',
    scopedSlots: { customRender: 'weight' },
  },
  {
    title: '尺寸（cm）',
    dataIndex: 'size',
    scopedSlots: { customRender: 'size' },
  },
  {
    title: '时间',
    dataIndex: 'time',
    scopedSlots: { customRender: 'time' },
  },
  {
    title: '操作',
    dataIndex: 'action',
    width: '130px',
    scopedSlots: { customRender: 'action' },
  },
]
const innerColumns = [
  {
    title: 'SKU图片',
    dataIndex: 'skuImage',
    scopedSlots: { customRender: 'skuImage' },
  },
  {
    title: 'SKU',
    dataIndex: 'skuCode',
  },
  {
    title: '属性',
    dataIndex: 'skuAttribute',
  },
  {
    title: '数量',
    dataIndex: 'number',
  },
]
// 表格数据
const responseSource = [
  {
    id: '1531553632599388166',
    spuCode: 'A15',
    spuImg:
      'https://axure-file.lanhuapp.com/8ca3bf46-a8c4-4b5f-9fd2-e395ff7d4ec1__44ba96da3b665644f519f398ea6db9af.svg',
    spuTitle: 'iphone16',
    remark: null,
    classificationId: '-2',
    userId: '1',
    createTime: '2022-06-14 10:53:27',
    updateTime: null,
    productSkuList: [
      {
        id: '1531553632964292613',
        skuCode: 'QWE',
        spuCode: 'A15',
        skuDetailId: null,
        spuTitle: null,
        skuAttribute: 'red*4.7',
        skuType: 2,
        price: '93',
        weight: '0.00',
        size: '0.00*31*51',
        skuImage:
          'https://axure-file.lanhuapp.com/8ca3bf46-a8c4-4b5f-9fd2-e395ff7d4ec1__44ba96da3b665644f519f398ea6db9af.svg',
        skuNumber: null,
        productSkuDetailResponseList: [
          {
            skuDetailId: 'QWE11',
            number: '1',
            skuCode: 'QWE',
            skuImage:
              'https://axure-file.lanhuapp.com/8ca3bf46-a8c4-4b5f-9fd2-e395ff7d4ec1__44ba96da3b665644f519f398ea6db9af.svg',
            skuAttribute: 'blue*5.3',
            skuType: '1',
            spuCode: 'A15',
          },
          {
            skuDetailId: 'QWE12',
            number: '1',
            skuCode: 'QWE',
            skuImage:
              'https://axure-file.lanhuapp.com/8ca3bf46-a8c4-4b5f-9fd2-e395ff7d4ec1__44ba96da3b665644f519f398ea6db9af.svg',
            skuAttribute: 'yellow*10',
            skuType: '1',
            spuCode: 'A15',
          },
        ],
      },
      {
        id: '1531553632964292614',
        skuCode: 'QWE11',
        spuCode: 'A15',
        skuDetailId: null,
        spuTitle: null,
        skuAttribute: 'blue*5.3',
        skuType: 1,
        price: '999',
        weight: '50.00',
        size: '15*10*5',
        skuImage:
          'https://axure-file.lanhuapp.com/8ca3bf46-a8c4-4b5f-9fd2-e395ff7d4ec1__44ba96da3b665644f519f398ea6db9af.svg',
        skuNumber: null,
        productSkuDetailResponseList: [],
      },
    ],
  },
  {
    id: '1531553632599388165',
    spuCode: 'A20',
    spuImg: 'http://dummyimage.com/400x400',
    spuTitle: 'iphone20',
    remark: null,
    classificationId: '23',
    userId: '1',
    createTime: '2022-06-14 10:53:23',
    updateTime: null,
    productSkuList: [
      {
        id: '1531553632964292610',
        skuCode: 'ASD',
        spuCode: 'A20',
        skuDetailId: null,
        spuTitle: null,
        skuAttribute: 'BLUE',
        skuType: 1,
        price: '96',
        weight: '44.00',
        size: '0.00*70*71',
        skuImage: 'http://dummyimage.com/400x400',
        skuNumber: null,
        productSkuDetailResponseList: [],
      },
    ],
  },
]
const statusMap = {
  0: {
    status: 'default',
    text: '关闭',
  },
  1: {
    status: 'processing',
    text: '运行中',
  },
  2: {
    status: 'success',
    text: '已上线',
  },
  3: {
    status: 'error',
    text: '异常',
  },
}
const treeData = [
  {
    id: 100,
    key: 100,
    isEdit: false,
    isNewItem: false,
    title: '所有分类',
    depth: 0,
    scopedSlots: { title: 'custom' },
    children: [
      {
        id: 2,
        key: 2,
        isEdit: false, // 是否处于编辑状态
        isNewItem: false, // 该节点是否是新增节点
        title: '未分类',
        depth: 1, // 该节点的层级
        scopedSlots: { title: 'custom' },
        children: [],
      },
    ],
  },
]
// 可编辑单元格
const EditableCell = {
  template: `
      <div class="editable-cell">
        <div v-if="editable" class="editable-cell-input-wrapper">
          <a-input :value="value" @change="handleChange" @pressEnter="check" /><a-icon
            type="check"
            class="editable-cell-icon-check"
            @click="check"
          />
        </div>
        <div v-else class="editable-cell-text-wrapper">
          <div>{{ value || ' ' }}</div>
          <a-icon type="edit" class="editable-cell-icon" @click="edit" />
        </div>
      </div>
    `,
  props: {
    text: String,
  },
  data() {
    return {
      value: this.text,
      editable: false,
    }
  },
  methods: {
    handleChange(e) {
      const value = e.target.value
      this.value = value
    },
    check() {
      this.editable = false
      this.$emit('change', this.value)
    },
    edit() {
      this.editable = true
    },
  },
}
export default {
  name: 'product',
  components: {
    STable,
    Ellipsis,
    CreateForm,
    goodsCategoryForm,
    EditableCell, // 可编辑单元格
  },
  data() {
    return {
      showLine: true,
      showIcon: false,
      checked: false,
      searchType: 1,
      labelCol: { style: { width: '80px' } },
      // create model
      visible: false,
      categoryVisible: false,
      confirmLoading: false,
      categoryConfirmLoading: false,
      mdl: null,
      categoryMdl: null,
      // 高级搜索 展开/关闭
      advanced: false,
      // 查询参数
      queryParam: {},
      columns,
      innerColumns,
      responseSource, // 后端表格数据
      dataSource: [], // 处理后表格数据
      SKUDetailsList: [], // sku详情
      isAll: false,
      status: 1, // 1 添加产品 2 编辑产品
      // 弹窗
      showSKUDetailsModal: false,
      // 加载数据方法 必须为 Promise 对象
      // loadData: (parameter) => {
      //   const requestParameters = Object.assign({}, parameter, this.queryParam)
      //   console.log('loadData request parameters:', requestParameters)
      //   return getServiceList(requestParameters).then((res) => {
      //     return res.result
      //   })
      // },
      selectedRowKeys: [],
      selectedRows: [],
      treeData,
    }
  },
  filters: {
    statusFilter(type) {
      return statusMap[type].text
    },
    statusTypeFilter(type) {
      return statusMap[type].status
    },
    skuTypeFilter(type) {
      switch (type) {
        case 1:
          return '单个SKU'
        case 2:
          return '组合SKU'
      }
    },
  },
  created() {
    // getRoleList({ t: new Date() })
  },
  mounted() {
    this.handleResponseSource()
  },
  computed: {
    rowSelection() {
      return {
        selectedRowKeys: this.selectedRowKeys,
        onChange: this.onSelectChange,
      }
    },
  },
  methods: {
    // 可编辑单元格
    onCellChange(key, dataIndex, value) {
      const dataSource = [...this.dataSource]
      const target = dataSource.find((item) => item.key === key)
      if (target) {
        target[dataIndex] = value
        this.dataSource = dataSource
      }
    },
    // 行合并 处理后端返回表格数据
    handleResponseSource() {
      let responseSource = this.responseSource
      let arr = []
      responseSource.map((item) => {
        const len = item.productSkuList.length
        item.productSkuList.map((item1, index) => {
          arr = [
            ...arr,
            {
              spuId: item.id,
              spuImg: item.spuImg,
              spuTitle: item.spuTitle,
              spuCode: item.spuCode,
              classificationId: item.classificationId,
              createTime: item.createTime,
              updateTime: item.updateTime,
              skuId: item1.id,
              skuCode: item1.skuCode,
              skuAttribute: item1.skuAttribute,
              skuType: item1.skuType,
              price: item1.price,
              weight: item1.weight,
              size: item1.size,
              skuImage: item1.skuImage,
              productSkuDetail: item1.productSkuDetailResponseList,
              rowSpan: index === 0 ? len : 0,
              checked: false,
            },
          ]
          return arr
        })
        return arr
      })
      this.dataSource = arr.map((item, index) => {
        item.key = index
        return item
      })
      console.log('1111', this.dataSource)
    },
    handleChange(e, index) {
      console.log(index)
      let rowSpan = this.dataSource[index].rowSpan
      console.log(rowSpan)
      for (var i = 0; i < rowSpan; i++) {
        this.dataSource[index++].checked = e.target.checked
      }
      console.log(this.dataSource)
    },
    handleChangeAll(e) {
      this.dataSource.map((item) => {
        item.checked = e.target.checked
      })
    },
    checkAll() {
      let flag = true
      // 判断是否所有被选中
      this.dataSource.map((item) => {
        if (item.checked == false) {
          flag = false
          this.isAll = flag
          return flag
        }
      })
      this.isAll = flag
      return flag
    },
    categoryHandleOk() {},
    onSelect(selectedKeys, info) {
      console.log('selected', selectedKeys, info)
    },
    handleAdd() {
      this.mdl = null
      this.visible = true
      this.status = 1
    },
    categoryHandleAdd() {
      this.categoryMdl = null
      this.categoryVisible = true
    },
    handleEdit(record) {
      this.visible = true
      this.mdl = { ...record }
      this.status = 2
    },
    handleOk() {
      const form = this.$refs.createModal.form
      this.confirmLoading = true
      form.validateFields((errors, values) => {
        if (!errors) {
          if (values.id > 0) {
            // 修改 e.g.
            new Promise((resolve, reject) => {
              setTimeout(() => {
                resolve()
              }, 1000)
            }).then((res) => {
              this.visible = false
              this.confirmLoading = false
              // 重置表单数据
              form.resetFields()
              // 刷新表格
              this.$refs.table.refresh()

              this.$message.info('修改成功')
            })
          } else {
            // 新增
            new Promise((resolve, reject) => {
              setTimeout(() => {
                resolve()
              }, 1000)
            }).then((res) => {
              this.visible = false
              this.confirmLoading = false
              // 重置表单数据
              form.resetFields()
              // 刷新表格
              this.$refs.table.refresh()

              this.$message.info('新增成功')
            })
          }
        } else {
          this.confirmLoading = false
        }
      })
    },
    categoryHandleCancel() {
      this.categoryVisible = false

      const form = this.$refs.goodsCategoryForm.form
      form.resetFields() // 清理表单数据（可不做）
    },
    handleCancel() {
      this.visible = false

      const form = this.$refs.createModal.form
      form.resetFields() // 清理表单数据（可不做）
    },
    // 弹窗
    handleSKUDetailsModal(data) {
      console.log('111', data)
      this.SKUDetailsList = data
      this.showSKUDetailsModal = true
    },
    handleSKUDetailsModalCancel() {
      this.showSKUDetailsModal = false
    },
    handleSub(record) {
      if (record.status !== 0) {
        this.$message.info(`${record.no} 订阅成功`)
      } else {
        this.$message.error(`${record.no} 订阅失败，规则已关闭`)
      }
    },
    onSelectChange(selectedRowKeys, selectedRows) {
      this.selectedRowKeys = selectedRowKeys
      this.selectedRows = selectedRows
    },
    toggleAdvanced() {
      this.advanced = !this.advanced
    },
    resetSearchForm() {
      this.queryParam = {
        date: moment(new Date()),
      }
    },
    // 页面跳转
    goPath(path, query) {
      this.$router.push({
        path: path,
        query: query,
      })
    },
  },
}
</script>
<style lang="less" scoped>
.fontColorRed {
  color: #d9001b;
}
// 表格
/deep/.ant-table-thead > tr > th {
  background: #fff;
  text-align: center;
}
/deep/.ant-table-tbody > tr > td {
  background: #fff;
  text-align: center;
}
.box {
  .row {
    max-width: 200px;
    -webkit-line-clamp: 2;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    overflow: hidden;
    // white-space: nowrap;
    text-overflow: ellipsis;
    text-align: left;
  }
}
.image {
  width: 80px;
}
</style>
```

#### 2.6 参考

antdesgintable合并表格实现表格一行对多行的效果 - 百度文库 https://wenku.baidu.com/view/d7142c35a11614791711cc7931b765ce05087a00.html

antd的customRender怎么用 - SegmentFault 思否 https://segmentfault.com/q/1010000023578435/

### 3.sku算法：笛卡尔乘积

#### 3.1 代码

```js
cartesianProduct() {
  let spec = [['100011-iPhone13'], ['Red', 'Blue'], ['M', 'L']]
  let sku = spec.reduce(
    (x, y) => {
      let arr = []
      x.forEach((x) => y.forEach((y) => arr.push(x.concat([y]))))
      return arr
    },
    [[]]
  )

  console.log(sku)
},
```

#### 3.2 结果

![image-20220630092058346](https://gitee.com/v876774538/my-img/raw/master/image-20220630092058346.png)

### 4.Vue中动态引入图片路径

```vue
 <img :src="weather ? require(`../../../assets/mainHome/${weather}.png`) : ''"/> 
```

### 5.销毁组件、重置组件方式

**使用v-if**

在组件上定义v-if一个布尔变量：

1.变量改为false

2.变量改为true

![image-20220701135752853](https://gitee.com/v876774538/my-img/raw/master/image-20220701135752853.png)

### 6.数组对象去重

```js
var arr = [{
  key: '01',
  value: '西施'
}, {
  key: '02',
  value: '王昭君'
}, {
  key: '03',
  value: '杨玉环'
}, {
  key: '04',
  value: '貂蝉'
}, {
  key: '01',
  value: '西施'
}, {
  key: '01',
  value: '西施'
}];
```

```js
var obj = {};
arr = arr.reduce(function (item, next) {
  obj[next.key] ? '' : obj[next.key] = true && item.push(next);
  return item;
}, []);
console.log(arr); // [{key: "01", value: "西施"},{key: "02", value: "王昭君"},{key: "03", value: "杨玉环"},{key: "04", value: "貂蝉"}]
```

### 7.数组对象深拷贝

```js
this.copyData = JSON.parse(JSON.stringify(this.field))
```

数组对象做还原备份需要注意**深拷贝**

**浅拷贝只拷贝地址**，将导致备份数据随原数据一起改变！！！

### 8.JS遍历树状数据，选择需要的字段重构一个新的树状数据

#### 8.1 原数据结构

```json
treeData = [
{
"id": 1,
"parentId": 0,
"type": "结生上取段日名求将查由六才酸商验又每。",
"referenceId": 234,
"sort": 29,
"code": "你计世派列太是后气住内带却所就。",
"name": "直按种白亲叫也总较机低及省。",
"userCount": 196,
"description": "空价等名共通七斗海共度实养族识观东。",
"modifyDate": null,
"makeBillMan": "test",
"createDate": null,
"modifier": "test",
"deleteFlag": false,
"children": [
  {
    "id": 2,
    "parentId": 1,
    "type": "结生上取段日名求将查由六才酸商验又每。",
    "referenceId": 234,
    "sort": 29,
    "code": "你计世派列太是后气住内带却所就。",
    "name": "直按种白亲叫也总较机低及省。",
    "userCount": 196,
    "description": "空价等名共通七斗海共度实养族识观东。",
    "modifyDate": null,
    "makeBillMan": "test",
    "createDate": null,
    "modifier": "test",
    "deleteFlag": false,
    "children": [
      {
        "id": 3,
        "parentId": 2,
        "type": "结生上取段日名求将查由六才酸商验又每。",
        "referenceId": 234,
        "sort": 29,
        "code": "你计世派列太是后气住内带却所就。",
        "name": "直按种白亲叫也总较机低及省。",
        "userCount": 196,
        "description": "空价等名共通七斗海共度实养族识观东。",
        "modifyDate": null,
        "makeBillMan": "test",
        "createDate": null,
        "modifier": "test",
        "deleteFlag": false,
        "children": []
      }
    ]
  }
]
}
```

#### 8.2 重构

要求：新建的数组要有和源数据一样的结构，其中只保留label=name，和children字段，children数组为空时去掉children字段。

```js
data() {
  return {
    treeData: null,
    newTreeList: []
  }
},
created() {
  this.getTreeList([this.treeData],this.newTreeList);
},
methods：{
  // 递归树状数据
  getTreeList(treeList,newTreeList) {
    treeList.map(c=>{
      let tempData={
        label:c.name
      }
      if(c.children && c.children.length>0){
        tempData.children=[]
        this.getTreeList(c.children,tempData.children)
      }
      newTreeList.push(tempData)
    })
  }
}
```

#### 8.4 有多棵树的情况

```js
this.responseTreeData.forEach((item) => {
  this.handleResponseTreeData([item], this.treeData)
})
```

```js
 methods: {
    handleResponseTreeData(treeList, newTreeList) {
      treeList.map((item) => {
        
        let tempData={
          id: item.classificationId,
          key: item.classificationId,
          isEdit: false,
          title: item.classificationName,
          // depth: 
          scopedSlots: { title: 'custom' },
          children: item.children
        }
        if (item.children && item.children.length > 0) {
          tempData.children = []
          this.handleResponseTreeData(item.children, tempData.children)
        }
        newTreeList.push(tempData)
      })
    },
}
```

### 9.判断某个字符在字符串中出现的次数

```js
var string='0,0,0,0,1,1,0,1,1,0,1,0,0,1,1,1,1,0,1,1,0,0,1,1,1,';
var n=(str.split('0')).length-1; //定义查找的对象为 0
console.log("共出现="+n+'次'); //打印结果
```

### 10.点击复制链接

```vue
<template>
  <div class="index">
    <a-card
      :bordered="false"
      title=" 邀请奖励在任务完成时候下发，请在【账户中心】【资金管理-佣金】中查看"
      headStyle="color:#FF0000"
    >
      <a-space size="large">
        <div class="title">邀请商家链接</div>
        <a-button type="primary" @click="copyLink">复制</a-button>
      </a-space>
      <div style="margin-top:20px">
        <a ref="link">http://saaszgzz.24x3600.com/h5/#/pages/index/BusinessRegister?inviterUserCode=a58729de</a>
      </div>
    </a-card>
  </div>
</template>

<script>
/**
 *  商家邀请码
 * @Author zzl
 * @Date 2022/7/8 17:02.
 */

export default {
  mounted() {},
  components: {},
  props: {},
  data() {
    return {}
  },
  computed: {},
  methods: {
    // 复制链接
    copyLink() {
      let url = this.$refs.link.innerHTML;
      const input = document.createElement('input')
      document.body.appendChild(input)
      input.setAttribute('value', url)
      input.select()
      document.execCommand('Copy')
      this.$message.info('复制链接成功！')
    },
  },
  watch: {},
  filters: {},
  beforeDestroy() {},
}
</script>

<style lang="less" scoped>
.index {
  .title {
    font-size: 26px;
    font-weight: bold;
    color: #333;
  }
}
</style>
```

### 11.antd上传图片

#### 11.1 页面

```html
<a-form-item label="申诉截图">
    <a-upload v-decorator="['slideShow']" :customRequest="uploadImages" :show-upload-list="false">
      <div v-if="fileList.length < 5">
        <a-button type="primary"><a-icon type="plus"></a-icon>图片上传</a-button>
      </div>
    </a-upload>
    <div class="images" v-if="fileList.length != 0">
      <img class="innerImage" v-for="(item,index) in fileList" :key="index" :src="item" alt="">
    </div>
</a-form-item>
```



```html
<a-form-item label="收款码">
    <a-upload name="file" list-type="picture-card" class="avatar-uploader" :show-upload-list="false"
        :action="action" :customRequest="uploadImage">
        <div v-if="form.QRcode">
            <img :src="form.QRcode" alt="" style="width: 86px;height: 86px">
        </div>
        <div v-else>
            <a-icon :type="uploading ? 'loading' : 'plus'"></a-icon>
            <div class="ant-upload-text">上传收款码</div>
        </div>
    </a-upload>
</a-form-item>
```

```js
export default {
    data() {
        action: '', //上传图片地址
    }
}
```

#### 11.2 上传

```js
import { uploadFile } from '@/api/merchantIndex'
```

```js
// 上传申诉截图
uploadImages(e) {
  const formData = new FormData()
  formData.append('file', e.file)
  formData.append('type', 'image')
  this.uploading = true
  this.form.QRcode = ''
  this.$forceUpdate()
  uploadFile(formData).then((res) => {
    if (!res.success) {
      this.$message.error(res.message)
      return false
    }
    this.uploading = false
    this.$message.success('上传成功！')
    this.fileList.push(res.data.data)
  })
},
```

封装上传请求

`http.js`

```js
// 上传图片
function httpUpload(url, params) {
    return request({
        url,
        method: 'post',
        headers: {
            headers: {
                'Content-Type': 'multipart/form-data',
            }
        },
        data: params
    })
}

export default {
    httpUpload,
}
```

`main.js`

```js
import http from './utils/http'

Vue.prototype.$httpUpload = http.httpUpload
```

```js
// 上传图片
uploadImage(e) {
    const formData = new FormData()
    formData.append('file', e.file)
    this.uploading = true
    this.form.QRcode = ''
    this.$forceUpdate()
    this.$httpUpload(this.APIURL.ossUploadFile, formData).then((res) => {
        if (!res.success) {
            this.$message.error(res.message)
            return false
        }
        this.uploading = false
        this.$message.success('上传成功', 1)
        this.form.QRcode = res.data
        // this.$forceUpdate()
    }).catch((err) => {
        this.$message.error(err.message)
    })
},
```

### 12.自定义表格分页器

```js
pagination: {
    pageSize: 10,
    total: 0,
    current: 1,
    showQuickJumper: true,
    showTotal: total => `共${this.pagination.total}条`,
    showSizeChanger: true,
    pageSizeOptions:['10','15','20','30'],
    onShowSizeChange:(current, pageSize) => this.pagination.pageSize = pageSize
},
```

![image-20220720171844823](https://gitee.com/v876774538/my-img/raw/master/image-20220720171844823.png)

### 13.图片预览

```vue
<img
  :src="topUpData.scanCodeImageToPay"
  alt=""
  class="image"
  @click="handlePreview(topUpData.scanCodeImageToPay)"
/>
```

```vue
<pic-preview :img-list="previewImg" :file-preview-show="previewShow" @close="hidePreview" />
```

```js
import PicPreview from '@/components/Image/PicPreview'
```

```js
components: {
    VideoModal,
    PicPreview
},
data() {
return {
  previewImg: [], // 预览图片
  previewShow: false, // 控制预览弹窗
}
},
```

```js
// 图片预览
handlePreview(previewImg) {
  this.previewImg.push(previewImg)
  this.previewShow = true
},
hidePreview() {
  this.previewImg = []
  this.previewShow = false
},
```

### 14.浮点数计算精确度的问题

#### 14.1 问题

3.95*3

![image-20220722150418223](https://gitee.com/v876774538/my-img/raw/master/image-20220722150418223.png)

#### 14.2 解决

利用`toFiexed`四舍五入取指定位数的小数点

```js
computed: {
    sumPrice() {
      let num = 0
      let sum = 0
      if (this.form.address != '') {
        let arr = this.form.address.split('\n')
        console.log('arr', arr)
        num = arr.length
        sum = (this.form.price * num).toFixed(2)
      }
      return sum
    },
},
```

### 15.$set赋值

#### 15.1 针对数组对象

![image-20220725141017386](https://gitee.com/v876774538/my-img/raw/master/image-20220725141017386.png)

#### 15.2 针对数组

```js
this.$set(arr,index,value)
```

### 16.遍历树 树转一级数组

#### 16.1 原树

![image-20220728180627233](https://gitee.com/v876774538/my-img/raw/master/image-20220728180627233.png)

#### 16.2 处理后

![image-20220728180702938](https://gitee.com/v876774538/my-img/raw/master/image-20220728180702938.png)

#### 16.3 实现

```js
// 遍历树
traversalTree(treeList, newList) {
  treeList.forEach((item) => {
    newList.push({
      id: item.id,
      name: item.name
    })
    if (!isNone(item.second)) {
      this.traversalTree(item.second, newList)
    }
  })
}
```

```js
// 获取资讯分类列表
getInformationCategoryList() {
  InformationApi.getInformationCategoryList().then((res) => {
    this.informationCategoryTreeList = res.data
    console.log(this.informationCategoryTreeList)
    this.traversalTree(this.informationCategoryTreeList, this.informationCategoryList)
  })
},
```

### 17.uni-app 左侧滚动导航栏

#### 17.1 实现

```vue
<template>
	<view class="index">
		<view class="bg"></view>
		<view class="header">
			<view class="integral">
				<text>{{integral.integral}}</text><text class="tip">≈ {{approximate(integral.integral)}}元</text>
			</view>
			<view class="choice">
					<button @click="jump()" class="btn">
						积分流水
					</button>
					<button @click="exchange()" class="btn">
						积分兑换记录
					</button>
			</view>
		</view>
		<view class="hotList">
			<view class="header">
				<view>热兑榜单</view>
				<view class="more">更多<image src="../../static/arrow-right.png" mode=""></image>
				</view>
			</view>
			<view class="content">
				<view class="li" v-for="(item, index) in hotExchangeListTop" :key="index">
					<view class="left">
						<image class="crown" :src="'../../static/no' + (index + 1) + '.png'" mode=""></image>
						<image class="productImg" :src="item.goodsImg" mode=""></image>
						<view class="center">
							<view class="title overflow-hidden">{{ item.goodsName }}</view>
							<view class="integral">{{ item.integral }}积分</view>
						</view>
					</view>
					<view class="right">
						销量{{ item.salesNum }}
					</view>
				</view>
			</view>
		</view>
		<view class="main" v-if="integralList.length!=0">
			<!-- 左侧导航 -->
			<scroll-view class="nav" scroll-y scroll-with-animation :scroll-top="verticalNavTop"
				style="height:calc(100vh - 375upx)">
				<view class="navItem" :class="index == tabCur ? 'text-green cur' : ''" v-for="(item, index) in list"
					:key="index" :data-id="index" @tap="tabSelect">
					{{item.name}}
				</view>
			</scroll-view>
			<!-- 右侧 -->
			<scroll-view class="scro" scroll-y scroll-with-animation style="height:calc(100vh - 375upx)"
				:scroll-into-view="'main-'+mainCur" @scroll="verticalMain">
				<view class="content" v-for="(item, index) in list" :key="index" :id="'main-'+index">
					<view class="li" v-for="(item1, index1) in item.list" :key="index1">
						<view class="left">
							<image :src="item1.goodsImg" mode=""></image>
						</view>
						<view class="right">
							<view class="row title overflow-hidden">{{item1.goodsName}}</view>
							<view class='row'>销量{{item1.salesNum}}</view>
							<view class="row1">
								<view class="integral">
									{{item1.integral}}积分
								</view>
								<button @click="goDetails(item1)">立即兑换</button>
							</view>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
		<view class="emptyList" v-else>
			<image src="https://gas-api.thkj66.com/gas-img/static/emptyList.png" mode="widthFix"></image>
			<view class="">
				暂无数据
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				integral: '',
				integralList: [], // 积分商品列表
				hotExchangeListTop: [], // 热兑榜单前三
				// pageNo: 1,
				contentText: {
					contentdown: "上拉显示更多",
					contentrefresh: "正在加载...",
					contentnomore: "没有更多数据了"
				},

				// otherLoadStatue: "loading", //'loading','noMore'

				// 左侧垂直导航栏
				verticalNavTop: 0,
				tabCur: 0,
				mainCur: 0,
				list: [],
				load: true,

			}
		},
		onLoad() {
			// this.otherLoadStatue = "loading";
			this.integral = uni.getStorageSync('userInfo');

			// this.pageNo = 1;
			this.integralList = [];
			this.getHotExchangeListTop();
			this.exchangeList();

		},
		onUnload() {
			// 销毁时跳转到指定界面
			// uni.reLaunch({
			// 	url:"/pages/mine/index"
			// })
			uni.switchTab({
				url: '/pages/mine/index'
			})
		},
		onShow() {

		},
		filters: {
			removeTAG(str) {
				return str.replaceAll(/&lt;.*?&gt;/g, "");
			}
		},
		methods: {
			// 约等于
			approximate(val) {
				return (val / 100).toFixed(2)
			},
			jump() {
				uni.navigateTo({
					url: '/pages/integral/index'
				})
			},
			exchange() {
				uni.navigateTo({
					url: '/pages/integral/exchange'
				})
			},
			goDetails(item) {
				let details = JSON.stringify(item)
				uni.navigateTo({
					url: '/pages/integral/integraStore?details=' + encodeURIComponent(details)
				})
			},
			goBack() {
				uni.switchTab({
					url: '/pages/mine/index'
				})
			},

			// 热兑榜单前三商品列表
			getHotExchangeListTop() {
				this.$http('GET', this.$APIURL.hotExchangeListTop, {}).then(res => {
					if (res.code !== this.config.SUCCESS) {
						this.utils.showToast(res.message)
						return false
					}
					// console.log('热兑榜单',res.data)
					this.hotExchangeListTop = res.data
				})
			},

			// 积分兑换列表
			exchangeList() {
				uni.showLoading({
					title: '加载中'
				})
				this.$http('GET', this.$APIURL.integralExchangeList, {
					// pageSize: 5,
					// pageNo: this.pageNo,
				}).then(res => {
					if (res.code !== this.config.SUCCESS) {
						this.utils.showToast(res.message);
						return false;
					}
					// console.log(res.data);
					// this.integralList = res.data;
					// 过滤掉分类中商品为空的
					res.data.map(item => {
						if (item.list != '') {
							this.integralList.push(item);
						}
					})
					// console.log('integralList', this.integralList)
					let list = [{}];
					for (let i = 0; i < this.integralList.length; i++) {
						list[i] = {};
						list[i].name = this.integralList[i].className;
						list[i].id = i;
						list[i].list = this.integralList[i].list;
					}
					this.list = list;
					this.listCur = list[0];
					// console.log('list', this.list)
					uni.hideLoading();
					// if (res.data.length < 5) {
					// 	this.otherLoadStatue = "noMore"
					// }
				})
			},

			// 左侧导航栏
			tabSelect(e) {
				// console.log(e);
				this.tabCur = e.currentTarget.dataset.id;
				this.mainCur = e.currentTarget.dataset.id;
				this.verticalNavTop = (e.currentTarget.dataset.id - 1) * 50
			},
			verticalMain(e) {
				// #ifdef MP-ALIPAY
				return false //支付宝小程序暂时不支持双向联动 
				// #endif
				let that = this;
				let tabHeight = 0;
				if (this.load) {
					for (let i = 0; i < this.list.length; i++) {
						let view = uni.createSelectorQuery().select("#main-" + this.list[i].id);
						view.fields({
							size: true
						}, data => {
							this.list[i].top = tabHeight;
							tabHeight = tabHeight + data.height;
							this.list[i].bottom = tabHeight;
						}).exec();
					}
					this.load = false
				}
				let scrollTop = e.detail.scrollTop + 10;
				for (let i = 0; i < this.list.length; i++) {
					if (scrollTop > this.list[i].top && scrollTop < this.list[i].bottom) {
						this.verticalNavTop = (this.list[i].id - 1) * 50
						this.tabCur = this.list[i].id
						// console.log(scrollTop)
						return false
					}
				}
			}

		},
		//上拉加载
		onReachBottom() {
			// if (this.otherLoadStatue == 'loading') {
			// this.pageNo++;
			// this.exchangeList();
			// }
			this.integralList = []
			this.exchangeList();

		},
		//下拉刷新
		onPullDownRefresh() {
			// console.log('刷新')
			// this.otherLoadStatue = "loading";
			this.integral = uni.getStorageSync('userInfo');
			// this.pageNo = 1;
			this.integralList = [];
			this.exchangeList();
			uni.stopPullDownRefresh()
		},
	}
</script>

<style lang="less" scoped>
	.index {
		width: 100%;
		height: 100%;
		background: linear-gradient(0deg, #F3F5F9 60%, #2298FE 100%);
		// padding: 20rpx;
		// box-sizing: border-box;

		.line {
			width: 100%;
			height: 48rpx;
			background: #F4F4F4;
		}

		.bg {
			height: 630rpx;
			width: 100%;
			position: absolute;
			top: 0;
			background: url(../../static/bg.png);
			background-size: 100%;
		}

		.header {
			width: 100%;
			margin-bottom: 40rpx;
			box-sizing: border-box;

			.integral {
				width: 100%;
				height: 142rpx;
				line-height: 142rpx;
				font-size: 96rpx;
				font-family: Source Han Sans SC;
				font-weight: 500;
				color: #FFFFFF;
				vertical-align: bottom;
				text-align: center;

				.tip {
					font-size: 28rpx;
					font-weight: 400;
				}
			}

			.choice {
				margin-top: 30rpx;
				display: flex;
				justify-content: center;

				.btn {
					font-size: 28rpx;
					width: 200rpx;
					height: 60rpx;
					line-height: 60rpx;
					color: #fff;
					background-color: transparent;
					border: 1px solid #fff;
					border-radius: 30rpx;
					text-align: center;
				}

				.btn:first-child {
					margin-right: 68rpx;
				}
			}
		}

		.hotList {
			background-color: #fff;
			border-radius: 20rpx;
			margin: 0 30rpx;
			padding: 30rpx;
			box-sizing: border-box;
			margin-bottom: 30rpx;

			.header {
				font-size: 32rpx;
				font-family: Source Han Sans SC;
				font-weight: bold;
				color: #333;
				display: flex;
				flex-direction: row;
				justify-content: space-between;

				.more {
					font-size: 28rpx;
					font-weight: normal;
					color: #999;
					display: flex;
					align-items: center;

					image {
						width: 24rpx;
						height: 24rpx;
						margin-left: 10rpx;
					}
				}
			}

			.content {
				display: flex;
				flex-direction: column;

				.li {
					display: flex;
					flex-direction: row;
					justify-content: space-between;
					align-items: center;
					margin-bottom: 30rpx;

					.left {
						display: flex;
						flex-direction: row;
						justify-content: space-around;
						align-items: center;

						.crown {
							width: 46rpx;
							height: 46rpx;
							margin-right: 20rpx;
						}

						.productImg {
							width: 82rpx;
							height: 82rpx;
							margin-right: 30rpx;
						}

						.center {
							.title {
								font-size: 32rpx;
								font-family: Source Han Sans SC;
								font-weight: bold;
								color: #333;
							}

							.integral {
								color: #F75649;
							}
						}
					}

					.right {
						font-size: 24rpx;
						font-family: Source Han Sans SC;
						color: #F9842A;
					}

				}

				.li:last-child {
					margin-bottom: 0;
				}
			}
		}

		.main {
			// box-sizing: border-box;
			margin: 30rpx;
			margin-bottom: 0;
			margin-top: 0;
			display: flex;
			border-radius: 20rpx;
			overflow: hidden;
			z-index: 1;

			// 左侧导航栏
			.nav {
				width: 200upx;
				white-space: initial;
				background-color: #EFF2F7;
			}

			.navItem {
				width: 100%;
				height: 50px;
				line-height: 50px;
				text-align: center;
				margin: 0;
				border: none;
				position: relative;
				color: #999999;
			}

			.cur {
				background-color: #fff;
				color: #000000;
			}

			.cur::after {
				content: "";
				width: 8upx;
				height: 30upx;
				border-radius: 0 10upx 10upx 0;
				position: absolute;
				background-color: #2298FE;
				top: 0;
				left: 0upx;
				bottom: 0;
				margin: auto;
			}

			.content {
				width: 550upx;
				display: flex;
				flex-direction: column;
				background-color: #fff;
				box-sizing: border-box;

				.li {
					display: flex;
					flex-direction: row;
					align-items: center;
					margin: 30rpx;
					padding-bottom: 30rpx;
					box-sizing: border-box;
					border-bottom: 1px solid #EEEEEE;
					font-family: Source Han Sans SC;

					.left {
						width: 160upx;
						height: 160upx;
						overflow: hidden;
						padding: 4rpx;
						box-sizing: border-box;
						border-radius: 10rpx;
						box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.16);
						margin-right: 20rpx;

						image {
							width: 100%;
							height: 100%;
						}
					}

					.right {
						width: 320upx;
						height: 200upx;
						display: flex;
						flex-direction: column;
						justify-content: space-around;

						.row {
							font-size: 24rpx;
							color: #999;

						}

						.row1 {
							display: flex;
							flex-direction: row;
							align-items: center;
							justify-content: space-between;

							button {
								width: 128rpx;
								height: 46rpx;
								line-height: 46rpx;
								background: #409EFF;
								border-radius: 40rpx;
								box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.16);
								opacity: 1;
								font-size: 24rpx;
								font-family: Source Han Sans SC;
								font-weight: 400;
								color: #FFFFFF;
								// padding:9rpx 28rpx;
							}

							.integral {
								font-size: 28rpx;
								color: #F75649;
								font-weight: 500;
							}
						}

						.title {
							font-size: 32rpx;
							color: #333;
							font-weight: bold;
						}
					}
				}

				.li:last-child {
					border-bottom: 0;
				}
			}

			.content:first-child {
				border-radius: 0 20rpx 0 0;
				overflow: hidden;
			}

			.content:last-child {
				border-radius: 0 0 20rpx 0;
				overflow: hidden;
			}
		}

		.emptyList {
			width: 100%;
			height: calc(100% - 274upx);
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;

			image {
				width: 445rpx;
				height: 276rpx;
				margin-bottom: 72rpx;
			}

			view {
				font-size: 28upx;
				color: #666666;
			}
		}
	}

	.overflow-hidden {
		width: 280rpx;
		display: inline-block;
		/* 内联元素需加上 */
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}
</style>

```

#### 17.2 效果图

![image-20220801145849141](https://gitee.com/v876774538/my-img/raw/master/image-20220801145849141.png)

### 18.uni-app 动态显示时间

#### 18.1 实现

```html
<text class="punch-time">{{ clock | FormatTime }}</text>
```

```js
data() {
    return {
      clock: Date.parse(new Date()),
    };
  },

 mounted() {
    let _this = this;
    setInterval(function () {
      _this.clock = Date.parse(new Date());
    }, 1000);
  },

 filters: {
    FormatTime: function (val) {
      return getDate(val, "hour");//根据传参不同显示的时间类型也不同
    },
},
```

```js
//format.js:
export function getDate(datetime, startType) {
  var date = new Date(datetime); //时间戳为10位需*1000，时间戳为13位的话不需乘1000
  var year = date.getFullYear(),
    month = ("0" + (date.getMonth() + 1)).slice(-2),
    sdate = ("0" + date.getDate()).slice(-2),
    hour = ("0" + date.getHours()).slice(-2),
    minute = ("0" + date.getMinutes()).slice(-2),
    second = ("0" + date.getSeconds()).slice(-2);
  // 拼接
  // var result = year + "-"+ month +"-"+ sdate +" "+ hour +":"+ minute +":" + second;
  // 返回
  // return result;
  let resStr = "";
  if (startType === "year")
    resStr =
      year +
      "-" +
      month +
      "-" +
      sdate +
      " " +
      hour +
      ":" +
      minute +
      ":" +
      second;
  if (startType === "day") resStr = year + "-" + month + "-" + sdate;
  if (startType === "month") resStr = month + "-" + sdate;
  if (startType === "hour") resStr = hour + ":" + minute + ":" + second;
  return resStr;
}
```

#### 18.2 效果

![image-20220811135734167](https://gitee.com/v876774538/my-img/raw/master/image-20220811135734167.png)

### 19. uni-app 分页

#### 19.1 pages.json 设置可下拉

```json
{
    "path": "pages/healthLife/healthyDiet/healthyDiet",
    "style": {
        "navigationBarTitleText": "健康饮食",
        "enablePullDownRefresh": true,
        "app-plus": {
            "titleNView": true
        }
    }
},
```

#### 19.2 html

```html
<uni-load-more :status="loadStatus" :content-text="contentText"></uni-load-more>
```

#### 19.3 js

```js
import uniLoadMore from '@/components/uni-load-more/uni-load-more.vue';
export default {
    components: {
        uniLoadMore
    },
	data() {
        return {
            pagination: {
                pageSize: 10,
                pageNo: 1,
            },
            contentText: {
                contentdown: "上拉显示更多",
                contentrefresh: "正在加载...",
                contentnomore: "没有更多数据了"
            },
            loadStatus: "loading", //'loading','noMore'
            list: [], // 忌口食物列表
        };
    },
    methods: {
    	// 获取资讯列表
        getInfomationArticle() {
            this.$http('get', this.APIURL.infomationArticle, {
                pageSize: this.pagination.pageSize,
                pageNo: this.pagination.pageNo,
                typeId: this.selectTab,
            }).then((res) => {
                uni.stopPullDownRefresh()
                if (!res.success) {
                    this.utils.showToast(res.message)
                    return false
                }
                this.list = this.list.concat(res.data.records)
                if (res.data.records.length < this.pagination.pageSize) {
                    setTimeout(() => {
                        this.loadStatus = "noMore"
                    }, 500)
                }
            })
        },
    },
    // 上拉加载
    onReachBottom() {
        console.log('上拉')
        if (this.loadStatus == 'loading') {
            this.pagination.pageNo++;
            this.getInfomationArticle();
        }
    },
    // 下拉刷新
    onPullDownRefresh() {
        this.loadStatus = "loading";
        this.pagination.pageNo = 1;
        this.list = [];
        this.getInfomationArticle();
    },
}
```

### 20.antd上传图片

```html
<a-upload accept=".jpg,.jpeg,.png,.JPG,.JPEG,.gif" :customRequest="imageEvaluateUploadImage">
  <a-button class="uploadBtn" type="primary">上传图片</a-button>
</a-upload>
```

```js
import {uploadFile} from "@/utils/util";
```

```js
async imageEvaluateUploadImage(e) {
  let result = await uploadFile(e.file)
  console.log('result',result.url)	// 获得上传文件的路径
},
```

### 21.修改placeholder文字样式

```css
input::placeholder {
  font-size: 16px;
  font-family: Source Han Sans CN;
  font-weight: 400;
  // color: #999999;
  color: #EB4025;
}
```

### 22.GET请求发送数组数据

```js
checkedList = ['Amazon', 'Qoo10', 'Rakuten', 'Wowma', 'Yahoo']
```

```js
// 获取店铺报表统计数据
getStoreReportData() {
  this.$saasGet(this.APIURL.getStoreReportData, {
    platformCodes: this.checkedList.join(','),
    storeCode: this.queryParams.storeCode,
    currency: this.queryParams.currency
  }).then((res) => {
    if (!res.success) {
      this.$message.error(res.message)
      return false
    }
    this.storeReportData = res.data
  }).catch((err) => {
    this.$message.error(err.message)
  })
},
```

![image-20220819093719717](https://gitee.com/v876774538/my-img/raw/master/image-20220819093719717.png)

### 23.绝对定位垂直居中

```css
.father {
	position: relative;	// 子绝父相
}
```

```css
.son {
	position: absolute;
	height: 28px;
	top: 50%;	// 父盒子高度的50%
	margin-top: -14px;	// 减去自身的一半
}
```

### 24.a-table翻页勾选（保存所有页面的勾选项）

```html
<a-table ref="table" size="default" :rowKey="(record) => record.id" :columns="columns" :data-source="skuList1" :rowSelection="rowSelection1" :pagination="false" :loading="loading" style="margin-top: 20px">
    <span slot="SKUimage" slot-scope="text, record">
      <template>
        <img class="SKUimage" :src="record.skuImage" alt="" />
      </template>
    </span>
    <span slot="SKUinfo" slot-scope="text, record">
      <template>
        <div class="info">SKU：{{ record.skuCode }}</div>
        <div class="info">属性：{{ record.skuAttribute }}</div>
        <div class="info">SKU类型：{{ record.skuType | skuTypeFilter }}</div>
        <div class="info">SPU：{{ record.spuCode }}</div>
      </template>
    </span>
</a-table>
```

```js
export default {
  data() {
    return {
      ...
      //   表格
      selectedRowKeys1: [],
      selectedRows1: [],
      chooseSkuList: [],
      chooseSkuList1: [],
      ...
    }
  },
  computed: {
    rowSelection1() {
      return {
        selectedRowKeys: this.selectedRowKeys1,
        onChange: this.onSelectChange1,
        onSelect: this.onSelect1,
      }
    },
  },
  methods: {
    // 表格
    // 表格多选
    onSelectChange1(selectedRowKeys, selectedRows) {
      this.selectedRowKeys1 = selectedRowKeys
      this.selectedRows1 = selectedRows
    },
    onSelect1(record, selected, selectedRows) {
      //  console.log(selectedRows, record, selected, 111111);
        // 勾选→push到数组中保存
       if (selected) {
        this.chooseSkuList1.push(record)
       }
        // 取消勾选→删除数组中的对应项
       else {
        this.chooseSkuList1.map((x, item) => {
          if (x.id == record.id) {
            this.chooseSkuList1.splice(item, 1)
          }
        })
       }
      //  console.log(this.chooseSkuList1)
    },
  mounted() { },
}
```

![image-20220823143210534](https://gitee.com/v876774538/my-img/raw/master/image-20220823143210534.png)

### 25.键值对遍历

```js
for (var key in this.dataSource.saleMap) {
  var date = key
  var value = this.dataSource.saleMap[key]
  // console.log(key, value)
  this.GMVdata.push({
    date: date,
    value: value
  })
}
```

### 26.根据日期排序

```js
    this.GMVdata.sort(function (a, b) { return a.date > b.date ? 1 : -1})
```

### 27.千分位逗号分隔

#### 27.1 添加过滤器

```js
numFilter: (val, fix = 2) => {
  val = val * 1 // 保证为数字型
  val = val.toFixed(fix)  // 保留2位小数
  val = val + ''  // 转换为字符串
  var int = val.slice(0, fix * -1 -1) // 整数
  var ext = val.slice(fix * -1 -1)  // 小数
  int = int.split('').reverse().join('')  // 翻转整数字符串
  var temp = ''
  for (var i = 0; i < int.length; i++) {
    temp += int[i]
    if ((i + 1) % 3 == 0 && i != int.length - 1) {
      temp += ',';  // 每隔3个数字拼接一个逗号
    }
  }
  temp = temp.split('').reverse().join('')  // 翻转
  temp = temp + ext;  // 拼接
  return temp
}
```

#### 27.2 使用

```html
<a-card :bordered="false">
  <span slot="title">汇总数据（货币单位：{{ currency }}）</span>
  <a-select slot="extra" :default-value="currencyList[0]" v-model="currency" @change="getOrderSummary">
    <a-select-option v-for="(item, index) in currencyList" :key="index" :value="item">
      {{ item }}
    </a-select-option>
  </a-select>
  <a-row :gutter="48" class="content">
    <a-col :md="8" class="box">
      <div class="val">{{ orderSummary.totalSale | numFilter(2) }}</div>
      <div class="label">总销售额（GMV）</div>
    </a-col>
    <a-col :md="8" class="box">
      <div class="val">{{ orderSummary.totalOrder | numFilter(0) }}</div>
      <div class="label">总订单数量</div>
    </a-col>
    <a-col :md="8" class="box">
      <div class="val">{{ orderSummary.perGuestPrice | numFilter(2) }}</div>
      <div class="label">客单价</div>
    </a-col>
  </a-row>
</a-card>
```

![image-20220824095848237](https://gitee.com/v876774538/my-img/raw/master/image-20220824095848237.png)

### 28.路由传参

#### 28.1 传参

```js
this.$router.push({
  path: '/describe',
  query: {
    id: id
  }
})

this.$router.push({
    name: 'Name',
    params: {
        id: id
    }
})
```

#### 28.2 接收

```js
this.$route.query.id	// 页面刷新后不丢失

this.$route.params.id	// 页面刷新后丢失
```

### 29.git使用

#### 29.1 项目分组

![image-20220831112257945](https://gitee.com/v876774538/my-img/raw/master/image-20220831112257945.png)

![image-20220831112342149](https://gitee.com/v876774538/my-img/raw/master/image-20220831112342149.png)

![image-20220831112433389](https://gitee.com/v876774538/my-img/raw/master/image-20220831112433389.png)

![image-20220831112447060](https://gitee.com/v876774538/my-img/raw/master/image-20220831112447060.png)

#### 29.2 具体项目

![image-20220831112713110](https://gitee.com/v876774538/my-img/raw/master/image-20220831112713110.png)

#### 29.3 命令

##### 29.3.1 git命令

```
git clone git地址	// 拉取代码

git pull
git add .
git commit -m"gx"
git push	// 上传代码

git checkout 分支名	// 切换分支
```

##### 29.3.2 npm命令

```
npm install	// 安装依赖
npm run serve	// 运行

cnpm run build 	// 打包
```

### 30.关闭ESLINT

`vue.config.js`

```
  lintOnSave: false, // 关闭eslint检查
```

### 31.a-table代码模板

```html
<a-table 
    :columns="columns"
    :data-source="dataSource"
    :pagination="pagination"
    :loading="loading"
    :rowKey="(record) => record.id"
    :row-selection="rowSelection"
    @change="onPageChange"
    :scroll="{ x: 1100 }"
    class="table">

</a-table>
```

```js
data() {
    return {
        columns: [
            {
                title: '',
                dataIndex: '',
                key: '',
                align: 'center'
            }
        ],    // 表头
        dataSource: [], // 表格资源
        loading: false, // 加载状态
        pagination: {
            pageSize: 10,
            total: 0,
            current: 1,
            showQuickJumper: true,
            showTotal: (total) => `共${this.pagination.total}条`,
            showSizeChanger: true,
            pageSizeOptions: ['10', '15', '20', '30'],
            onShowSizeChange: (current, pageSize) => (this.pagination.pageSize = pageSize),
            // hideOnSinglePage: true,	// 单页隐藏
        },
        selectedRows: [],	// 选中的行
        selectedRowKeys: [],    // 选中的行的key
    }
},
computed: {
    // 表格选择
    rowSelection() {
        return {
            selectedRowKeys: this.selectedRowKeys,    // 一定要加上这一行，清除才有效
            onChange: (selectedRowKeys, selectedRows) => {
                this.selectedRows = selectedRows
                this.selectedRowKeys = selectedRowKeys
            },
        }
    },
},
methods: {
    // 翻页
    onPageChange(e) {
        this.pagination.current = e.current
        // 重新加载
        
    },
    // 清除批量勾选
    clearSelectRows() {
        this.selectedRowKeys = []
    },
},
```

### 32.antd 默认中文

#### 32.1 src\core\bootstrap.js

![image-20220905114248044](https://gitee.com/v876774538/my-img/raw/master/image-20220905114248044.png)

#### 32.2 src\locales\index.js

![image-20220905114353332](https://gitee.com/v876774538/my-img/raw/master/image-20220905114353332.png)

#### 32.3 src\store\modules\app.js

![image-20220905114437453](https://gitee.com/v876774538/my-img/raw/master/image-20220905114437453.png)

### 33.请求封装

#### 33.1 封装地址

1. api/home.js

   ```js
   // 暴露模块请求地址
   export const Home = {
       warehouseList: '/warehouse/list',   // 仓库列表
       setDefaultWarehouse: '/user/setDefaultWarehouse',   // 设置默认仓库
   }
   ```

2. api/index.js

   ```js
   // 存放集合
   import { Login } from './login'
   import { Home } from './home'
   
   const APIURL = Object.assign(
       Login,
       Home,
   )
   export default APIURL
   ```

3. main.js

   ```js
   import api from './api/index'	// 全局引入
   
   Vue.prototype.APIURL = api	// 挂载到原型
   ```

#### 33.2 封装请求

1. utils/http.js

   ```js
   import request from '@/utils/request'
   // get
   function httpGet(url, params) {
       return request({
           url,
           method: 'get',
           params
       })
   }
   // post
   function httpPost(url, params) {
       return request({
           url,
           method: 'post',
           headers: {
               'Content-Type': 'application/json;charset=UTF-8'
           },
           data: JSON.stringify(params),
       })
   }
   // 导出
   function httpExcel(url, params) {
       return request({
           url,
           method: 'post',
           headers: {
               'Content-Type': 'application/json;charset=UTF-8'
           },
           responseType: 'arraybuffer',
           data: JSON.stringify(params)
       })
   }
   // 导出
   function httpExcel(url, params) {
       return request({
           url,
           method: 'get',
           params,
           responseType: 'blob',
       })
   }
   // 上传图片
   function httpUpload(url, params) {
       return request({
           url,
           method: 'post',
           headers: {
               headers: {
                   'Content-Type': 'multipart/form-data',
               }
           },
           data: params
       })
   }
   
   export default {
       httpGet,
       httpPost,
       httpExcel,
       httpUpload,
   }
   ```

2. main.js

   ```js
   import http from './utils/http'	// 全局引入
   
   Vue.prototype.$httpGet = http.httpGet
   Vue.prototype.$httpPost = http.httpPost
   Vue.prototype.$httpExcel = http.httpExcel
   Vue.prototype.$httpUpload = http.httpUpload	// 挂载
   ```

3. 字节流文件打开方法

   util.js

   ```js
   // 导出
   // type：excel application/vnd.ms-excel zip application/zip
   function exportApi(type, res, name) {
     const link = document.createElement('a')
     let blob = new Blob([res], {
       type
     })
     link.style.display = 'none'
     link.href = URL.createObjectURL(blob)
     // link.download = res.headers['content-disposition'] //下载后文件名
     var date = new Date()
     link.download = name + '_' + date.getFullYear() + '-' + (date.getMonth() * 1 + 1) + '-' +
       date.getDate() + ' ' + date.getHours() + '_' + date.getMinutes() + '_' + date.getSeconds() //下载的文件名
     document.body.appendChild(link)
     link.click()
     document.body.removeChild(link)
   }
   ```

   util也可以挂载到原型

   main.js

   ```js
   import utils from '@/utils/util'
   Vue.prototype.utils = utils
   ```

   使用

   ```js
   this.$httpExcel(this.APIURL.exportUpc, {
       poolId: this.form.poolId,
       status: this.form.status
   }).then((res) => {
       this.utils.exportApi('application/vnd.ms-excel', res, this.form.name)
       this.$emit('ok')
   }).catch((err) => {
       this.$message.error(err.message)
   })
   ```


### 34.点击复制表格中的地址

```html
<a-table :columns="columns" :data-source="dataSource" :pagination="pagination" :loading="loading"
    @change="onPageChange">
    <div slot="action" slot-scope="text, record">
        <a-space>
            <a href="javascript:;" @click="copyAddr(record.address)">复制地址</a>
            <a href="javascript:;" v-if="record.isDefault == 1">默认地址</a>
            <a href="javascript:;" v-else>设为默认</a>
        </a-space>
    </div>
</a-table>
```

```js
// 复制地址
copyAddr(addr) {
    // 模拟 输入框
    var cInput = document.createElement("input");
    cInput.value = addr;
    document.body.appendChild(cInput);
    cInput.select(); // 选取文本框内容

    // 执行浏览器复制命令
    // 复制命令会将当前选中的内容复制到剪切板中（这里就是创建的input标签）
    // Input要在正常的编辑状态下原生复制方法才会生效

    document.execCommand("copy");

    this.$message.success("复制成功！");
    // 复制成功后再将构造的标签 移除
    document.body.removeChild(cInput);
},
```

![image-20220908111644122](https://gitee.com/v876774538/my-img/raw/master/image-20220908111644122.png)

### 35.富文本内容回显 图片样式限制

通过`v-html`回显富文本内容时可能存在图片超出容器范围的问题，普通的样式修改并不起效，此时需要对图片样式进行限制：

```css
// 使用less深度选择器
<style lang="less" scoped>
    @import '~@/assets/css/base.less';
    .content {
           /deep/ img {
                width:1rem;
           }
    } 
</style>
```

### 36.解决select下拉菜单数据量过大造成的卡顿问题

#### 36.1 组件

```vue
<!-- 下拉菜单滚动加载 -->
<template>
    <div>
        <a-select v-bind="$attrs" v-on="$listeners" :style="{width:`${width}px`}" v-model="selected" :showSearch="true"
            :allowClear="true" :placeholder="placeholder" option-filter-prop="children" @search="handlerFilterOption"
            @popupScroll="handlerScroll" @blur="handlerSelected" @change="handlerChange"
            @dropdownVisibleChange="handlerDropdown">
            <a-select-option v-for="(item,index) in uniqFilterSelectOptions" :key="index" :value="item.name"
                @click="handleSelectItem(item)">
                {{item.name}}
            </a-select-option>
        </a-select>
    </div>
</template>

<script>
// 引入loadsh 用于对下拉操作进行防抖操作
import _ from 'loadsh'
export default {
    name: 'SelectLoadByScroll',
    components: {},
    model: {
        prop: 'value',
        event: 'change'
    },
    props: {
        // 父组件通过v-model实现父子组件数据选择同步
        value: {
            type: [Array, Number, String],
            default: undefined
        },
        options: {  // 下拉列表数据
            type: Array,
            default: () => ([])
        },
        width: {
            type: Number,
            default: () => (200)
        },
        maxShowStrips: { // 初始化和每次滚动显示的最大条数
            type: Number,
            default: () => (15)
        },
        placeholder: {
            type: String,
            default: () => ''
        }
    },
    data() {
        return {
            userSearch: '', // 用户搜索时的内容
            filterOptions: [], // 过滤用户输入后的option
            selected: undefined, // 选择的数据
            selectedItem: {}
        }
    },
    computed: {
        // 避免重复插入截取的数据
        uniqFilterSelectOptions() {
            let { filterOptions = [] } = this
            let optionsList = []
            return filterOptions.filter(item => {
                let { name } = item || {}
                if (optionsList.includes(name)) {
                    return false
                } else {
                    optionsList.push(name)
                    return true
                }

            })
        }
    },
    created() {
    },
    mounted() {
        // 修改回显
        if (this.value) {
            this.selected = this.value
        }
    },
    methods: {
        // 得到下拉列表的数据
        getSelectOptions(selected) {
            let { userSearch = '', options = [], filterOptions = [], maxShowStrips = 15 } = this
            if (!Array.isArray(options)) return
            let tempFilterOptions = userSearch ?
                options.filter((item) => {
                    let { name = '' } = item || {}
                    return name && name.indexOf(userSearch) !== -1;
                })
                : options
            // console.log(tempFilterOptions)
            if (tempFilterOptions.length > maxShowStrips) {
                tempFilterOptions = tempFilterOptions.slice(0, maxShowStrips)
            } else {
                tempFilterOptions = tempFilterOptions
            }
            // 判断用户是否有选择
            if (selected) {
                if (!selected) return
                // 从options中过滤出当前选中的数据
                let selectedOptions = options.filter(item => {
                    let { name } = item || {}
                    if (Array.isArray(selected) && selected.length > 0 && selected.includes(name)) {
                        return true
                    } else if (selected === name) {
                        return true
                    } else {
                        return false
                    }
                })
                selectedOptions.forEach(item => {
                    const option = _.find(filterOptions, { name: item.name })
                    if (!option || !option.name) {
                        tempFilterOptions.unshift(item)
                    }
                })
            }
            this.filterOptions = tempFilterOptions
        },
        // 滚动条滚动，无限拼接数据
        handlerScroll: _.debounce(function () {
            let { options = [], maxShowStrips = 15, filterOptions = [] } = this
            let currindex = filterOptions.length
            let allIndex = options.length
            let nextPageIndex = currindex + maxShowStrips
            let newFilterOptions = nextPageIndex > allIndex ? options.slice(currindex, allIndex) : options.slice(currindex, nextPageIndex)
            this.filterOptions = filterOptions.concat(newFilterOptions)
        }, 200),
        // 用户改变搜索条件
        handlerFilterOption(value) {
            this.userSearch = value || ''
            this.getSelectOptions()
        },
        // 用户选择
        handlerSelected() {
            if (this.userSearch) {
                this.userSearch = ''
                this.getSelectOptions(this.selected)
            }
        },
        // 向父组件通知选择的数据
        handlerChange(value) {
            let res = Object.assign({}, this.selectedItem)
            this.$emit('onchange', res)
        },
        handlerDropdown(flag) {
            if (flag) this.getSelectOptions()
        },
        // 选择
        handleSelectItem(value) {
            this.selectedItem = value
        }
    },
    filter() { },
    watch: {
        options: {
            handler() {
                this.getSelectOptions();
            },
            immediate: true,
            deep: true,
        },
    },
}
</script>
    
<style lang="less" scoped>

</style>
```

#### 36.2 使用

```html
<select-load-by-scroll :value="form.brandId" @onChange="selectHandleChange" :options="brandsList" :placeholder="'请先选择产品分类'" :width="200">
</select-load-by-scroll>
```

### 37.金额格式化

```js
numFilter(val) {
    if (!val) return '0.00'
    val = val.toFixed(2)
    var intPart = Math.trunc(val) // 获取整数部分
    var intPartFormat = intPart.toString().replace(/(\d)(?=(?:\d{3})+$)/g, '$1,') // 将整数部分逢三一断
    var floatPart = '.00' // 预定义小数部分
    var value2Array = val.split('.')
    // =2表示数据有小数位
    if (value2Array.length === 2) {
        floatPart = value2Array[1].toString() // 拿到小数部分
        if (floatPart.length === 1) {
            return intPartFormat + '.' + floatPart + '0'
        } else {
            return intPartFormat + '.' + floatPart
        }
    } else {
        return intPartFormat + floatPart
    }
},
```

### 38.获取url链接中的参数

#### 38.1 split分割

```js
var url = window.location.href;             //获取当前url
var cs = url.split('?')[1];                //获取?之后的参数字符串
var cs_arr = cs.split('&');                    //参数字符串分割为数组
var cs = {};
for (var i = 0; i < cs_arr.length; i++) {         //遍历数组，拿到json对象
    cs[cs_arr[i].split('=')[0]] = cs_arr[i].split('=')[1]
}
return cs
```

![image-20220921142151040](https://gitee.com/v876774538/my-img/raw/master/image-20220921142151040.png)

#### 38.2 正则匹配

```js
/**
 *   获取url中的参数
 * @param key  待匹配的关键字
 * @param url  被匹配查询的url
 */
export function getUrlQuery(key, url) {
    let str = url || window.location.href //默认获取浏览器地址栏中的url
    let reg = decodeURIComponent((new RegExp('[?|&|/]' + key + '=([^&;]+?)(&|#|;|$)').exec(str) || [, ''])[1].replace(/\+/g, '%20')) || null
    return reg
}
```

```js
import { getUrlQuery } from './result.js'

let reg = getUrlQuery('name', 'http://hrefs.syy3.com/merchant/#/shopAuthorization?code=ABCDEFG123456&name=hhhhhh')
console.log(reg)
```

![image-20230201154702943](https://gitee.com/v876774538/my-img/raw/master/image-20230201154702943.png)

### 39.判断是否为生产环境

```js
const isProd = process.env.NODE_ENV === 'production'
```

### 40.框架自带的接口调用脱离本地环境（测试、生产）使用mock替代

#### 41.1 报错

![image-20220923144307015](https://gitee.com/v876774538/my-img/raw/master/image-20220923144307015.png)

#### 40.2 解决

1. `src\mock\services\user.js`

   ![image-20220923144357149](https://gitee.com/v876774538/my-img/raw/master/image-20220923144357149.png)

2. `src\api\login.js`

   ![image-20220923144453765](https://gitee.com/v876774538/my-img/raw/master/image-20220923144453765.png)

   ![image-20220923144443164](https://gitee.com/v876774538/my-img/raw/master/image-20220923144443164.png)

   使用Promise类方法resolve()直接返回Promise成功对象

### 41.富文本编辑器 QuillEditor使用（vue2 antd）

> 新版本？QuillEditor 官方文档地址：[Modules | VueQuill (vueup.github.io)](https://vueup.github.io/vue-quill/guide/modules.html)适配vue3使用

#### 41.1 组件

![image-20220923144939718](https://gitee.com/v876774538/my-img/raw/master/image-20220923144939718.png)

##### 1.图片大小限制，base64转换，压缩图片

 `class="notranslate"`不允许谷歌翻译进行翻译

```vue
<template>
  <div :class="prefixCls">
    <quill-editor v-model="content" ref="myQuillEditor" class="notranslate" :options="editorOption" @blur="onEditorBlur($event)"
      @focus="onEditorFocus($event)" @ready="onEditorReady($event)" @change="onEditorChange($event)">
    </quill-editor>
  </div>
</template>

<script>
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'
import 'quill/dist/quill.bubble.css'

import { quillEditor } from 'vue-quill-editor'

const toolbarOptions = [
  ['bold', 'italic', 'underline', 'strike'], // 加粗 斜体 下划线 删除线 -----['bold', 'italic', 'underline', 'strike']
  [{ color: [] }, { background: [] }], // 字体颜色、字体背景颜色-----[{ color: [] }, { background: [] }]
  [{ align: [] }], // 对齐方式-----[{ align: [] }]
  [{ size: ['small', false, 'large', 'huge'] }], // 字体大小-----[{ size: ['small', false, 'large', 'huge'] }]
  [{ font: [] }], // 字体种类-----[{ font: [] }]
  [{ header: [1, 2, 3, 4, 5, 6, false] }], // 标题
  [{ direction: 'ltl' }], // 文本方向-----[{'direction': 'rtl'}]
  [{ direction: 'rtl' }], // 文本方向-----[{'direction': 'rtl'}]
  [{ indent: '-1' }, { indent: '+1' }], // 缩进-----[{ indent: '-1' }, { indent: '+1' }]
  [{ list: 'ordered' }, { list: 'bullet' }], // 有序、无序列表-----[{ list: 'ordered' }, { list: 'bullet' }]
  [{ script: 'sub' }, { script: 'super' }], // 上标/下标-----[{ script: 'sub' }, { script: 'super' }]
  ['blockquote', 'code-block'], // 引用  代码块-----['blockquote', 'code-block']
  ['clean'], // 清除文本格式-----['clean']
  ['link', 'image', 'video'] // 链接、图片、视频-----['link', 'image', 'video']
]

export default {
  name: 'QuillEditor',
  components: {
    quillEditor
  },
  props: {
    prefixCls: {
      type: String,
      default: 'ant-editor-quill'
    },
    // 表单校验用字段
    // eslint-disable-next-line
    value: {
      type: String
    }
  },
  data() {
    return {
      content: null,
      editorOption: {
        theme: 'snow', // 主题
        placeholder: '',
        modules: {
          toolbar: {
            container: [
              ['image'],
            ], // 自定义工具栏选项
            handlers: {
              image: () => {
                let fileInput = this.$refs['myQuillEditor'].$el.querySelector('input.ql-image[type=file]')
                if (!fileInput) {
                  fileInput = document.createElement('input')
                  fileInput.setAttribute('type', 'file')
                  fileInput.setAttribute('name', 'file')
                  fileInput.setAttribute('accept', 'image/*')
                  fileInput.classList.add('ql-image')
                  fileInput.style.display = 'none'
                  fileInput.addEventListener('change', () => {
                    const imgs = this.content && this.content.match(/<img.*?/g)
                    if (imgs && imgs.length >= 30) {
                      this.$message.info('最多上传30张图片')
                      return
                    }
                    const file = fileInput.files[0]
                    // 图片大小限制
                    const valid = this.checkPicTypeAndSize(file, { PICTURE_MAX_SIZE: 2 * 1024 * 1024, PICTURE_MAX_TIP: '2MB' })
                    if (!valid) {
                      return
                    }

                    // 1.直接file转base64
                    // this.toBase64(file, (base64) => {
                    //   const index = (this.$refs['myQuillEditor'].quill.getSelection() || {}).index || this.$refs['myQuillEditor'].quill.getLength()
                    //   this.$refs['myQuillEditor'].quill.insertEmbed(index, 'image', base64)  // 插入到光标位置
                    //   // 光标位置后移
                    //   this.$refs['myQuillEditor'].quill.setSelection(index + 1)
                    // })

                    // 2.压缩图片
                    this.compressImg(file, { quality: 0.5 }, (base64) => {
                      const index = (this.$refs['myQuillEditor'].quill.getSelection() || {}).index || this.$refs['myQuillEditor'].quill.getLength()
                      this.$refs['myQuillEditor'].quill.insertEmbed(index, 'image', base64)  // 插入到光标位置
                      // 光标位置后移
                      this.$refs['myQuillEditor'].quill.setSelection(index + 1)
                    })

                    fileInput.value = ''
                  })
                  this.$refs['myQuillEditor'].$el.appendChild(fileInput)
                }
                fileInput.click()
              }
            },
          },
        },
      }
    }
  },
  methods: {
    onEditorBlur(quill) {
      // console.log('editor blur!', quill)
    },
    onEditorFocus(quill) {
      // console.log('editor focus!', quill)
    },
    onEditorReady(quill) {
      // console.log('editor ready!', quill)
    },
    onEditorChange({ quill, html, text }) {
      console.log('editor change!', quill, html, text)
      this.$emit('change', html)
    },
    checkPicTypeAndSize(file, MAX) {
      if (file.size > MAX.PICTURE_MAX_SIZE) {
        this.$message.error('请不要上传超过' + MAX.PICTURE_MAX_TIP + '的图片！')
        return false
      }
      return true
    },
    // file转base64
    toBase64(file, callback) {
      const reader = new FileReader()
      reader.onload = function (evt) {
        if (typeof callback === 'function') {
          callback(evt.target.result)
        } else {
          console.log("base64:", evt.target.result);
        }
      }
      /* readAsDataURL 方法会读取指定的 Blob 或 File 对象
      ** 读取操作完成的时候，会触发 onload 事件
      *  result 属性将包含一个data:URL格式的字符串（base64编码）以表示所读取文件的内容。
      */
      reader.readAsDataURL(file);
    },
    // 压缩图片
    /*
    *file：文件的file
    *obj配置 {quality：0.2}压缩比例
    *callback 回调
    */
    compressImg(file, obj, callback) {
      let _this = this;
      var ready = new FileReader();
      /*开始读取指定的Blob对象或File对象中的内容. 
              当读取操作完成时,readyState属性的值会成为DONE,
              如果设置了onloadend事件处理程序,则调用之.
              同时,result属性中将包含一个data: URL格式的字符串以表示所读取文件的内容.*/
      ready.readAsDataURL(file);
      ready.onload = function () {
        var path = this.result;
        // ↓压缩
        var img = new Image();
        img.src = path;
        img.onload = function () {
          var that = this;
          // 默认按比例压缩
          var w = that.width,
            h = that.height,
            scale = w / h;
          w = obj.width || w;
          h = obj.height || w / scale;
          var quality = 0.7; // 默认图片质量为0.7
          //生成canvas
          var canvas = document.createElement("canvas");
          var ctx = canvas.getContext("2d");
          // 创建属性节点
          var anw = document.createAttribute("width");
          anw.nodeValue = w;
          var anh = document.createAttribute("height");
          anh.nodeValue = h;
          canvas.setAttributeNode(anw);
          canvas.setAttributeNode(anh);
          ctx.drawImage(that, 0, 0, w, h);
          // 图像质量
          if (obj.quality && obj.quality <= 1 && obj.quality > 0) {
            quality = obj.quality;
          }
          // quality值越小，所绘制出的图像越模糊
          var base64 = canvas.toDataURL("image/jpeg", quality);
          // // 转换为Blob数据
          // var BlobData = _this.convertBase64UrlToBlob(base64)
          // // 转换为file数据
          // let this_file = new File(
          //   [BlobData],
          //   file.name,
          // );
          console.log('base64', base64)
          // 回调函数返回file的值
          callback(base64)
          // ↑压缩
        };
      };
    },
    // 转换为Blob数据方法
    convertBase64UrlToBlob(urlData) {
      var arr = urlData.split(","),
        mime = arr[0].match(/:(.*?);/)[1],
        bstr = atob(arr[1]),
        n = bstr.length,
        u8arr = new Uint8Array(n);
      while (n--) {
        u8arr[n] = bstr.charCodeAt(n);
      }
      return new Blob([u8arr], { type: mime });
    },
  },
  watch: {
    value(val) {
      this.content = val
      return false
    }
  }
}
</script>

<style lang="less" scoped>
@import url('../index.less');

/* 覆盖 quill 默认边框圆角为 ant 默认圆角，用于统一 ant 组件风格 */
.ant-editor-quill {
  line-height: initial;

  /deep/ .ql-toolbar.ql-snow {
    border-radius: @border-radius-base @border-radius-base 0 0;
  }

  /deep/ .ql-container.ql-snow {
    border-radius: 0 0 @border-radius-base @border-radius-base;
  }
}
</style>

```

##### 2.图片大小限制，上传图片到阿里云解决图片过大过多加载慢的问题

```vue
<template>
  <div :class="prefixCls">
    <quill-editor v-model="content" ref="myQuillEditor" :options="editorOption" @blur="onEditorBlur($event)"
      @focus="onEditorFocus($event)" @ready="onEditorReady($event)" @change="onEditorChange($event)">
    </quill-editor>

  </div>
</template>

<script>
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'
import 'quill/dist/quill.bubble.css'

import { quillEditor } from 'vue-quill-editor'

const toolbarOptions = [
  ['bold', 'italic', 'underline', 'strike'], // 加粗 斜体 下划线 删除线 -----['bold', 'italic', 'underline', 'strike']
  [{ color: [] }, { background: [] }], // 字体颜色、字体背景颜色-----[{ color: [] }, { background: [] }]
  [{ align: [] }], // 对齐方式-----[{ align: [] }]
  [{ size: ['small', false, 'large', 'huge'] }], // 字体大小-----[{ size: ['small', false, 'large', 'huge'] }]
  [{ font: [] }], // 字体种类-----[{ font: [] }]
  [{ header: [1, 2, 3, 4, 5, 6, false] }], // 标题
  [{ direction: 'ltl' }], // 文本方向-----[{'direction': 'rtl'}]
  [{ direction: 'rtl' }], // 文本方向-----[{'direction': 'rtl'}]
  [{ indent: '-1' }, { indent: '+1' }], // 缩进-----[{ indent: '-1' }, { indent: '+1' }]
  [{ list: 'ordered' }, { list: 'bullet' }], // 有序、无序列表-----[{ list: 'ordered' }, { list: 'bullet' }]
  [{ script: 'sub' }, { script: 'super' }], // 上标/下标-----[{ script: 'sub' }, { script: 'super' }]
  ['blockquote', 'code-block'], // 引用  代码块-----['blockquote', 'code-block']
  ['clean'], // 清除文本格式-----['clean']
  ['link', 'image', 'video'] // 链接、图片、视频-----['link', 'image', 'video']
]

export default {
  name: 'QuillEditor',
  components: {
    quillEditor
  },
  props: {
    prefixCls: {
      type: String,
      default: 'ant-editor-quill'
    },
    // 表单校验用字段
    // eslint-disable-next-line
    value: {
      type: String,
      default: () => ''
    },
    myEditorOption: {
      type: Object,
      default: () => { }
    }
  },
  mounted() {
    // console.log('mounted')
    // console.log('value', this.value)
    this.content = this.value
  },
  data() {
    return {
      content: null,
      editorOption: this.myEditorOption ? this.myEditorOption : {
        theme: 'snow', // 主题
        placeholder: '',
        modules: {
          toolbar: {
            container: [
              ['image'],
            ], // 自定义工具栏选项
            handlers: {
              image: () => {
                let fileInput = this.$refs['myQuillEditor'].$el.querySelector('input.ql-image[type=file]')
                if (!fileInput) {
                  fileInput = document.createElement('input')
                  fileInput.setAttribute('type', 'file')
                  fileInput.setAttribute('name', 'file')
                  fileInput.setAttribute('accept', 'image/*')
                  fileInput.classList.add('ql-image')
                  fileInput.style.display = 'none'
                  fileInput.addEventListener('change', () => {
                    const imgs = this.content && this.content.match(/<img.*?/g)
                    if (imgs && imgs.length >= 30) {
                      this.$message.info('最多上传30张图片')
                      return
                    }
                    const file = fileInput.files[0]
                    // 图片大小限制
                    const valid = this.checkPicTypeAndSize(file, { PICTURE_MAX_SIZE: 2 * 1024 * 1024, PICTURE_MAX_TIP: '2MB' })
                    if (!valid) {
                      return
                    }
                    // 上传图片
                    this.uploadImage(file, (data) => {
                      const index = (this.$refs['myQuillEditor'].quill.getSelection() || {}).index || this.$refs['myQuillEditor'].quill.getLength()
                      this.$refs['myQuillEditor'].quill.insertEmbed(index, 'image', data)  // 插入到光标位置
                      // 光标位置后移
                      this.$refs['myQuillEditor'].quill.setSelection(index + 1)
                    })

                    fileInput.value = ''
                  })
                  this.$refs['myQuillEditor'].$el.appendChild(fileInput)
                }
                fileInput.click()
              }
            },
          },
        },
      }
    }
  },
  methods: {
    onEditorBlur(quill) {
      // console.log('editor blur!', quill)
    },
    onEditorFocus(quill) {
      // console.log('editor focus!', quill)
    },
    onEditorReady(quill) {
      // console.log('editor ready!', quill)
    },
    onEditorChange({ quill, html, text }) {
      console.log('editor change!', quill, html, text)
      this.$emit('change', html)
    },
    checkPicTypeAndSize(file, MAX) {
      console.log('file', file)
      if (file.size > MAX.PICTURE_MAX_SIZE) {
        this.$message.error('请不要上传超过' + MAX.PICTURE_MAX_TIP + '的图片！')
        return false
      }
      return true
    },
    // 上传图片
    uploadImage(file, callback) {
      this.$message.loading({ content: '上传中，请稍后……', key: 'message', duration: 0 })
      const formData = new FormData()
      formData.append('file', file)
      this.$httpUpload(this.APIURL.ossUploadFile, formData).then((res) => {
        if (!res.success) {
          this.$message.error({ content: res.message, key: 'message' })
          return false
        }
        callback(res.data)
        this.$message.success({ content: '上传完成！', key: 'message' })
      }).catch((err) => {
        this.$message.error({ content: err.message, key: 'message' })
      })
    }
  },
  // watch: {
  //   value(val) {
  //     this.content = val
  //   }
  // }
}
</script>

<style lang="less" scoped>
@import url('../index.less');

/* 覆盖 quill 默认边框圆角为 ant 默认圆角，用于统一 ant 组件风格 */
.ant-editor-quill {
  line-height: initial;

  /deep/ .ql-toolbar.ql-snow {
    border-radius: @border-radius-base @border-radius-base 0 0;
  }

  /deep/ .ql-container.ql-snow {
    border-radius: 0 0 @border-radius-base @border-radius-base;
  }
}
</style>

```

##### 3.自定义工具

```vue
<template>
  <div :class="prefixCls">
    <quill-editor v-model="content" ref="myQuillEditor" :options="editorOption" @blur="onEditorBlur($event)"
      @focus="onEditorFocus($event)" @ready="onEditorReady($event)" @change="onEditorChange($event)">
    </quill-editor>
    <!-- 上传网络图片 -->
    <a-modal v-model="showOnlinePictureModal" title="从网络地址(URL)选择图片" @ok="handleUploadOnlineImage"
      @cancel="form.picUrls = ''; showOnlinePictureModal = false;">
      <a-textarea v-model="form.picUrls" :rows="5" placeholder="请填写URL地址，多个地址用回车换行"></a-textarea>
    </a-modal>
    <!-- 引用采集图片 -->
    <a-modal v-if="showQuoteCollectImageModal" v-model="showQuoteCollectImageModal" title="引用采集图片"
      @ok="handleQuoteCollectImageOk" @cancel="handleQuoteCollectImageCancel" class="quoteCollectImage_modal"
      :width="600">
      <div class="content">
        <div class="productImageBox" v-for="(item, index) in form.quoteList">
          <img :src="item.url" alt="" class="image">
          <a-checkbox :value="index" class="checkbox" @change="handleQuoteCollectImageCheck($event, item)">
          </a-checkbox>
        </div>
      </div>
    </a-modal>
    <!-- 引用产品图片 -->
    <a-modal v-if="showQuoteProductImageModal" v-model="showQuoteProductImageModal" title="引用产品图片"
      @ok="handleQuoteProductImageOk" @cancel="handleQuoteProductImageCancel" class="quoteCollectImage_modal"
      :width="600">
      <div class="content">
        <div class="productImageBox" v-for="(item, index) in form.quoteList">
          <img :src="item.url" alt="" class="image">
          <a-checkbox :value="index" class="checkbox" @change="handleQuoteCollectImageCheck($event, item)">
          </a-checkbox>
        </div>
      </div>
    </a-modal>
  </div>
</template>

<script>
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'
import 'quill/dist/quill.bubble.css'

import { quillEditor } from 'vue-quill-editor'
import { isNone } from '@/utils/util';

const toolbarOptions = [
  ['bold', 'italic', 'underline', 'strike'], // 加粗 斜体 下划线 删除线 -----['bold', 'italic', 'underline', 'strike']
  [{ color: [] }, { background: [] }], // 字体颜色、字体背景颜色-----[{ color: [] }, { background: [] }]
  [{ align: [] }], // 对齐方式-----[{ align: [] }]
  [{ size: ['small', false, 'large', 'huge'] }], // 字体大小-----[{ size: ['small', false, 'large', 'huge'] }]
  [{ font: [] }], // 字体种类-----[{ font: [] }]
  [{ header: [1, 2, 3, 4, 5, 6, false] }], // 标题
  [{ direction: 'ltl' }], // 文本方向-----[{'direction': 'rtl'}]
  [{ direction: 'rtl' }], // 文本方向-----[{'direction': 'rtl'}]
  [{ indent: '-1' }, { indent: '+1' }], // 缩进-----[{ indent: '-1' }, { indent: '+1' }]
  [{ list: 'ordered' }, { list: 'bullet' }], // 有序、无序列表-----[{ list: 'ordered' }, { list: 'bullet' }]
  [{ script: 'sub' }, { script: 'super' }], // 上标/下标-----[{ script: 'sub' }, { script: 'super' }]
  ['blockquote', 'code-block'], // 引用  代码块-----['blockquote', 'code-block']
  ['clean'], // 清除文本格式-----['clean']
  // ['link', 'image', 'video', 'upload'], // 链接、图片、视频-----['link', 'image', 'video']
  ['link', 'video', 'upload'], // 链接、图片、视频-----['link', 'image', 'video']
]

export default {
  name: 'QuillEditor',
  components: {
    quillEditor
  },
  props: {
    prefixCls: {
      type: String,
      default: 'ant-editor-quill'
    },
    // 表单校验用字段
    // eslint-disable-next-line
    value: {
      type: String,
      default: () => ''
    },
    form: {
      type: Object,
      default: () => { }
    }
  },
  created() {
  },
  mounted() {
    // this.content = this.value
    // console.log(this.content)
    this.$nextTick(() => {
      this.initButton()
    })
  },
  data() {
    return {
      content: null,
      editorOption: {
        theme: 'snow', // 主题
        placeholder: '',
        modules: {
          toolbar: {
            container: toolbarOptions, // 自定义工具栏选项
            handlers: {
            
            },
          },
        },
      },
      // 弹窗
      showOnlinePictureModal: false,  // 上传网络图片
      showQuoteCollectImageModal: false,  // 引用采集图片
      showQuoteProductImageModal: false,  // 引用产品图片
    }
  },
  methods: {
    // 初始化自定义工具按钮  
    initButton() {
      const editorButton = document.querySelector('.ql-upload');
      editorButton.style.cssText = 'width: 80px;'
      // 自定义下拉菜单
      // html给elect添加placeholder技巧：disabled selected style='display: none'
      editorButton.innerHTML = "<select class='upload-select'><option value='' disabled selected style='display: none'>上传图片</option><option value='1'>本地图片</option><option value='2'>网络图片</option><option value='3'>引用采集图片</option><option value='4'>引用产品图片</option></select>"
      const select = document.querySelector('.my-select')
      // 绑定点击事件、、事件、、
      select.addEventListener('change', (e) => {
        let index = select.selectedIndex
        select.selectedIndex = 0
        // 本地图片
        if (index == 1) {
          let fileInput = this.$refs['myQuillEditor'].$el.querySelector('input.ql-image[type=file]')
          if (!fileInput) {
            fileInput = document.createElement('input')
            fileInput.setAttribute('type', 'file')
            fileInput.setAttribute('name', 'file')
            fileInput.setAttribute('accept', 'image/*')
            fileInput.classList.add('ql-image')
            fileInput.style.display = 'none'
            fileInput.addEventListener('change', () => {
              const imgs = this.content && this.content.match(/<img.*?/g)
              if (imgs && imgs.length >= 30) {
                this.$message.info('最多上传30张图片')
                return
              }
              const file = fileInput.files[0]
              // 图片大小限制
              const valid = this.checkPicTypeAndSize(file, { PICTURE_MAX_SIZE: 2 * 1024 * 1024, PICTURE_MAX_TIP: '2MB' })
              if (!valid) {
                return
              }
              // 上传图片
              this.uploadImage(file, (data) => {
                const index = (this.$refs['myQuillEditor'].quill.getSelection() || {}).index || this.$refs['myQuillEditor'].quill.getLength()
                this.$refs['myQuillEditor'].quill.insertEmbed(index, 'image', data)  // 插入到光标位置
                // 光标位置后移
                this.$refs['myQuillEditor'].quill.setSelection(index + 1)
              })
              fileInput.value = ''
            })
            this.$refs['myQuillEditor'].$el.appendChild(fileInput)
          }
          fileInput.click()
        }
        // 网络图片
        else if (index == 2) {
          this.showOnlinePictureModal = true
        }
        // 引用采集图片
        else if (index == 3) {
          this.handleQuoteCollectImage()
        }
        // 引用产品图片
        else if (index == 4) {
          this.handleQuoteProductImage()
        }
      })
    },
    // 上传网络图片
    handleUploadOnlineImage() {
      if (isNone(this.form.picUrls)) {
        this.$message.info('请填写图片URL地址')
        return false
      }
      this.form.picUrls.split('\n').forEach((item) => {
        if (item) {
          const index = (this.$refs['myQuillEditor'].quill.getSelection() || {}).index || this.$refs['myQuillEditor'].quill.getLength()
          this.$refs['myQuillEditor'].quill.insertEmbed(index, 'image', item)  // 插入到光标位置
          // 光标位置后移
          this.$refs['myQuillEditor'].quill.setSelection(index + 1)
        }
      })
      this.showOnlinePictureModal = false
      this.form.picUrls = ''
    },
    // 引用采集图片
    handleQuoteCollectImage() {
      this.form.quoteList = []
      if (this.form.collectImages) {
        this.form.collectImages.forEach((item) => {
          this.form.quoteList.push({
            url: item,
            width: '',
            height: '',
            checked: false,
          })
        })
      }
      this.showQuoteCollectImageModal = true
    },
    handleQuoteCollectImageOk() {
      if (this.form.quoteList && this.form.quoteList.length != 0) {
        this.form.quoteList.forEach((item) => {
          if (item.checked) {
            console.log(item.url)
            const index = (this.$refs['myQuillEditor'].quill.getSelection() || {}).index || this.$refs['myQuillEditor'].quill.getLength()
            this.$refs['myQuillEditor'].quill.insertEmbed(index, 'image', item.url)  // 插入到光标位置
            // 光标位置后移
            this.$refs['myQuillEditor'].quill.setSelection(index + 1)
          }
        })
        this.showQuoteCollectImageModal = false
      }
      else {
        this.showQuoteCollectImageModal = false
      }
    },
    handleQuoteCollectImageCancel() {
      this.form.quoteList = []
      this.showQuoteCollectImageModal = false
    },
    handleQuoteCollectImageCheck(e, item) {
      item.checked = e.target.checked
    },
    // 引用产品图片
    handleQuoteProductImage() {
      this.form.quoteList = []
      if (this.form.productImageList) {
        this.form.productImageList.forEach((item) => {
          this.form.quoteList.push({
            url: item.url,
            width: item.width,
            height: item.height,
            checked: false,
          })
        })
      }
      this.showQuoteProductImageModal = true
    },
    handleQuoteProductImageOk() {
      if (this.form.quoteList && this.form.quoteList.length != 0) {
        this.form.quoteList.forEach((item) => {
          if (item.checked) {
            const index = (this.$refs['myQuillEditor'].quill.getSelection() || {}).index || this.$refs['myQuillEditor'].quill.getLength()
            this.$refs['myQuillEditor'].quill.insertEmbed(index, 'image', item.url)  // 插入到光标位置
            // 光标位置后移
            this.$refs['myQuillEditor'].quill.setSelection(index + 1)
          }
        })
        this.showQuoteProductImageModal = false
      }
      else {
        this.showQuoteProductImageModal = false
      }
    },
    handleQuoteProductImageCancel() {
      this.form.quoteList = []
      this.showQuoteProductImageModal = false
    },
    handleQuoteProductImageCheck(e, item) {
      item.checked = e.target.checked
    },
    onEditorBlur(quill) {
      // console.log('editor blur!', quill)
    },
    onEditorFocus(quill) {
      // console.log('editor focus!', quill)
    },
    onEditorReady(quill) {
      // console.log('editor ready!', quill)
    },
    onEditorChange({ quill, html, text }) {
      // console.log('editor change!', quill, html, text)
      console.log('editor change!', html)
      this.$emit('change', html)
    },
    checkPicTypeAndSize(file, MAX) {
      console.log('file', file)
      if (file.size > MAX.PICTURE_MAX_SIZE) {
        this.$message.error('请不要上传超过' + MAX.PICTURE_MAX_TIP + '的图片！')
        return false
      }
      return true
    },
    // 上传图片
    uploadImage(file, callback) {
      this.$message.loading({ content: '上传中，请稍后……', key: 'message', duration: 0 })
      const formData = new FormData()
      formData.append('file', file)
      this.$httpUpload(this.APIURL.ossUploadFile, formData).then((res) => {
        if (!res.success) {
          this.$message.error({ content: res.message, key: 'message' })
          return false
        }
        callback(res.data)
        this.$message.success({ content: '上传完成！', key: 'message' })
      }).catch((err) => {
        this.$message.error({ content: err.message, key: 'message' })
      })
    }
  },
  watch: {
    value(val) {
      this.content = val
    }
  }
}
</script>

<style lang="less" scoped>
@import url('../index.less');

/* 覆盖 quill 默认边框圆角为 ant 默认圆角，用于统一 ant 组件风格 */
.ant-editor-quill {
  line-height: initial;

  /deep/ .ql-toolbar.ql-snow {
    border-radius: @border-radius-base @border-radius-base 0 0;
  }

  /deep/ .ql-container.ql-snow {
    border-radius: 0 0 @border-radius-base @border-radius-base;
  }
}

/deep/.select {
  padding: 0 5px;
}

.quoteCollectImage_modal {
  .content {
    display: flex;
    flex-wrap: wrap;

    .productImageBox {
      position: relative;
      border: 1px solid #e8e8e8;
      // width: 120px;
      // height: 147px;
      // overflow: hidden;
      margin-right: 10px;
      margin-bottom: 10px;
      cursor: pointer;

      .image {
        width: 100px;
        height: 100px;
        overflow: hidden;
        position: relative;

        img {
          width: 100%;
          height: 100%;
        }

      }

      .checkbox {
        position: absolute;
        top: 2px;
        left: 5px;
      }
    }

    .productImageBox:nth-child(5n) {
      margin-right: 0;
    }
  }
}
</style>

```



#### 41.2 使用

```js
import QuillEditor from '@/components/Editor/QuillEditor.vue'	// 单页面引入

// 组件注册
components: {
	QuillEditor,
},
```

```html
<quill-editor ref="quillEditor" class="quillEditor" :value="form.content" @change="onEditorChange"></quill-editor>
```

```js
onEditorChange(res) {
  this.form.content = res
},
```



```html
<quill-editor class="quillEditor" :myEditorOption="{
  theme: 'snow', // 主题
  placeholder: '',
  modules: {
    toolbar: {
      container: [
        ['image'],
      ], // 自定义工具栏选项
    },
  },
}" @change="onEditorChange"></quill-editor>

// 传myEditorOption给子组件
props: {
    prefixCls: {
      type: String,
      default: 'ant-editor-quill'
    },
    // 表单校验用字段
    // eslint-disable-next-line
    value: {
      type: String,
      default: () => ''
    },
    myEditorOption: {
      type: Object,
      default: () => { }
    }
},

// 组件配置
data() {
    return {
      content: null,
      editorOption: this.myEditorOption ? this.myEditorOption : {
		...
    }
},
```

### 42.设置网页title

```js
document.title = '标题名称';
```

![image-20220928140501903](https://gitee.com/v876774538/my-img/raw/master/image-20220928140501903.png)

![image-20220928140624237](https://gitee.com/v876774538/my-img/raw/master/image-20220928140624237.png)

![image-20220928140632335](https://gitee.com/v876774538/my-img/raw/master/image-20220928140632335.png)

### 43.监听路由$route.query变化

#### 43.1 监听

```js
watch: {
    '$route.query': {
        immediate: true,    // 一旦监听到路由变化立即执行
        handler(newVal, oldVal) {
            // console.log(newVal, oldVal)
            // query改变 重新获取数据
            if (this.$route.query.status) {
                // 赋值
                let query = this.$route.query
                this.status = query.status * 1
                this.queryParams.platformOrderSn = query.platformOrderSn
                this.handleSearch() // 查询
            }
            if (!isNone(newVal)) {
                this.$router.push({ query: {} })	// 清空query参数
            }
        },
        deep: true
    }
},
```

#### 43.2 跳转

```js
this.$router.push({
    path: '/order/index',
    query: query,
})
```

### 44.解决表格带额外展开行需要全部展开的问题

`:rowKey="(record) => record.id" :expandedRowKeys="dataSource.map(item => item.id)"`

```html
<a-table :columns="columns" :data-source="dataSource" :rowKey="(record) => record.id" :expandedRowKeys="dataSource.map(item => item.id)"
    :pagination="pagination" :loading="loading" :row-selection="rowSelection"
    @change="onPageChange" class="table">
	...
    <!-- 自定义展开图标 -->
    <!-- <div slot="expandIcon" slot-scope="text, record">

    </div> -->
    <div slot="expandedRowRender" slot-scope="record">
        <table class="expandTable">
            ...
        </table>
    </div>
</a-table>
```

```js
// 表格
columns: [
    ...
],    // 表头
dataSource: [], // 表格资源
loading: false, // 加载状态
pagination: {
    pageSize: 10,
    total: 0,
    current: 1,
    showQuickJumper: true,
    showTotal: (total) => `共${this.pagination.total}条`,
    showSizeChanger: true,
    pageSizeOptions: ['10', '15', '20', '30'],
    onShowSizeChange: (current, pageSize) => (this.pagination.pageSize = pageSize),
    // hideOnSinglePage: true,	// 单页隐藏
},
selectedRows: [],	// 选中的行
selectedRowKeys: [],    // 选中的行的key
// 表格选择
rowSelection: {
    onChange: (selectedRowKeys, selectedRows) => {
        this.selectedRows = selectedRows
        this.selectedRowKeys = selectedRowKeys
    },
},
```

```js
// 翻页
onPageChange(e) {
    this.pagination.current = e.current
    // 重新加载
	...
},
```

**但是因为写死所以，不能合上了，还需要改进**

### 45.uni-app 获取当前时间

#### 45.1 getDateTime.js

```js
function dateTimeStr(str){
	var date = new Date(),
	year = date.getFullYear(), //年
	month = date.getMonth() + 1, //月
	day = date.getDate(), //日
	hour = date.getHours() < 10 ? "0" + date.getHours() : date.getHours(), //时
	minute = date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes(), //分
	second = date.getSeconds() < 10 ? "0" + date.getSeconds() : date.getSeconds(); //秒
	month >= 1 && month <= 9 ? (month = "0" + month) : "";
	day >= 0 && day <= 9 ? (day = "0" + day) : "";
	if(str.indexOf('y') != -1){
		str = str.replace('y', year)
	}
	if(str.indexOf('m') != -1){
		str = str.replace('m', month)
	}
	if(str.indexOf('d') != -1){
		str = str.replace('d', day)
	}
	if(str.indexOf('h') != -1){
		str = str.replace('h', hour)
	}
	if(str.indexOf('i') != -1){
		str = str.replace('i', minute)
	}
	if(str.indexOf('s') != -1){
		str = str.replace('s', second)
	}
	return str;
}
 
module.exports = {
	dateTimeStr: dateTimeStr,
}
```

#### 45.2 使用

```js
import getDateTime from '@/common/getDateTime.js';	// 引入
```

```js
onLoad() {
    // 获取当前时间
    this.nowTime = getDateTime.dateTimeStr('y-m-d h:i:s'); // y:年 m:月 d:日 h:时 i:分 s:秒 中间的分割符号可更改
    console.log(this.nowTime)
},
```

### 46.uni-app 判断是否当天

```js
// 是否当天
isSameDate(startTime, endTime) {
    const startTimeMs = new Date(startTime).setHours(0, 0, 0, 0);	// 设置为0点0分0秒0毫秒
    const endTimeMs = new Date(endTime).setHours(0, 0, 0, 0);
    return startTimeMs === endTimeMs ? true : false
},
```

### 47.antd modal 提示信息内容展示后端返回的带换行符的信息

```js
this.$success({
    title: res.message,
    content: (
        <p ref="message" style="white-space:pre-wrap"></p>
    )
})
this.$nextTick(() => {
    this.$refs.message.innerHTML = res.data.replace(/\r\n/g, '<br/>')
})
```

![image-20221014135218801](https://gitee.com/v876774538/my-img/raw/master/image-20221014135218801.png)

**white-space属性值**

`normal`：忽略多余的空白，只保留一个空白（默认）；
`pre`：保留空白(行为方式类似于html中的pre标签)；
`nowrap`：只保留一个空白，文本不会换行，会在在同一行上继续，直到遇到br标签为止。
`pre-wrap`：保留空白符序列，正常地进行换行；
`pre-line`：合并空白符序列，保留换行符；
`inherit`：从父元素继承white-space属性的值。

### 48.获取某个日期区间的日期数组

```js
// 获取日期数组
getAllDateCN(startTime, endTime) {
    var date_all = []
    startTime = startTime.setHours(0, 0, 0, 0)
    endTime = endTime.setHours(0, 0, 0, 0)	// 时间戳
    while (startTime <= endTime) {
        var date = new Date(startTime)
        var year = date.getFullYear()
        var month = date.getMonth() + 1
        var day = date.getDate()
        month = String(month).length <= 1 ? '0' + month : month
        day = String(day).length <= 1 ? '0' + day : day
        date_all.push(year + '-' + month + '-' + day)
        startTime += (24 * 60 * 60 * 1000)	// +1天
    }
    return date_all
},
```

```js
var date = new Date();
// ts = ... 时间戳
var preDate = new Date(ts * 1000);
var all = this.getAllDateCN(preDate, date)
```

### 49.为数组中每个对象添加属性

```js
// 添加showBit属性
this.dataSource.forEach((item) => {
    Object.assign(item, {
        showBit: false
    })
})
```

### 50.CSS实现带箭头的横向任务流程图

#### 50.1 效果

![image-20221018161534902](https://gitee.com/v876774538/my-img/raw/master/image-20221018161534902.png)

#### 50.2 实现

```html
<a-card :bordered="false" class="flow_card">
    <div class="title">
        <div class="line"></div>数据搬家任务流程图
    </div>
    <div class="flow">
        <div class="flowItem active">同步产品</div>
        <div class="flowItem">认领产品</div>
        <div class="flowItem">选择店铺</div>
        <div class="flowItem">进入采集箱</div>
    </div>
</a-card>
```

```css
.flow_card {
    // 标题
    .title {
        font-size: 15px;
        font-weight: 600;
        display: flex;
        align-items: center;
        margin-bottom: 20px;

        .line {
            width: 3px;
            height: 13px;
            display: block;
            background-color: #3AA5FF;
            border-radius: 10px;
            margin-right: 5px;
        }
    }
	//流程图
    .flow {
        display: flex;
        flex-direction: row;

        .flowItem {
            width: 40%;
            height: 40px;
            line-height: 40px;
            background-color: #E4E4E4;
            text-align: center;
            position: relative;
            margin-right: 10px;
        }

        .active {
            background-color: #1890FF;
            color: #fff;
        }

        .flowItem:after,
        .flowItem:before,
        .active:after,
        .active:before {
            content: '';
            display: block;
            position: absolute;
            top: 0;
        }

        .flowItem:after {
            border-top: 20px solid transparent;
            border-bottom: 20px solid transparent;
            border-left: 20px solid #E4E4E4;
            right: -20px;
            z-index: 9;
        }

        .flowItem:before {
            border-top: 20px solid #E4E4E4;
            border-bottom: 20px solid #E4E4E4;
            border-left: 20px solid #fff;
            left: 0;
        }
        .active:after {
            border-top: 20px solid transparent;
            border-bottom: 20px solid transparent;
            border-left: 20px solid #1890FF;
            right: -20px;
        }

        .active:before {
            border-top: 20px solid transparent;
            border-bottom: 20px solid transparent;
            border-left: 20px solid #FFFFFF;
            left: 0;
        }

    }
}
```

### 51.三级checkbox（1.的优化版本）

#### 51.1 效果

![image-20221019155326703](https://gitee.com/v876774538/my-img/raw/master/image-20221019155326703.png)

#### 51.2 思路

全选/取消全选通过递归来完成，再通过后序遍历来判断父的选中状态。

**后序遍历**：左右根，下图数据输出为`10,4,5,1,6,11,7,2,8,12,9,3,0`

![在这里插入图片描述](https://img-blog.csdnimg.cn/4c741614659745cdb9e80f49a3a1b3c5.png)

```js
function nextOrderTraverse(rnode){
    if(rnode.children){
        for(let v of rnode.children){
             nextOrderTraverse(v)
        }
    }
    console.log(rnode.id)
}

nextOrderTraverse(Tree)

```

附js实现先序、中序、后序、层序遍历：https://blog.csdn.net/qq_61233877/article/details/124881491

#### 51.3 代码

```vue
<template>
    <div class="index">
        <a-card :bordered="false" title="选择批量编辑的信息">
            <tr v-for="(item1, index1) in checkModule" :key="item1.id">
                <td>
                    <a-checkbox v-model:checked="item1.checked" @change="onCheckboxChange($event, item1, index1, 1)">
                        {{item1.label}}</a-checkbox>
                </td>
                <td v-for="(item2, index2) in item1.children" :key="item2.id">
            <tr>
                <td>
                    <a-checkbox v-model:checked="item2.checked" @change="onCheckboxChange($event, item2, index2, 2)">{{
                    item2.label }}</a-checkbox>
                </td>
            </tr>
            <tr v-for="(item3, index3) in item2.children" :key="item3.id">
                <td>
                    <a-checkbox v-model:checked="item3.checked" @change="onCheckboxChange($event, item3, index3, 3)">{{
                    item3.label }}</a-checkbox>
                </td>
            </tr>
            </td>
            </tr>
        </a-card>
    </div>
</template>

<script>
export default {
    name: 'PutGoodsOnSale',
    data() {
        return {
            checkModule: [
                {
                    parentId: null,
                    id: 0,
                    label: '全部',
                    checked: false,
                    children: [
                        {
                            parentId: 0,
                            id: 100,
                            label: '变种信息',
                            checked: false,
                            children: [
                                {
                                    parentId: 100,
                                    id: 101,
                                    label: '变种主题',
                                    checked: false,
                                    children: null
                                },
                                {
                                    parentId: 100,
                                    id: 102,
                                    label: '变种图',
                                    checked: false,
                                    children: null
                                },
                                {
                                    parentId: 100,
                                    id: 103,
                                    label: '价格',
                                    checked: true,
                                    children: null
                                },
                                {
                                    parentId: 100,
                                    id: 104,
                                    label: '库存',
                                    checked: true,
                                    children: null
                                }
                            ]
                        },
                        {
                            parentId: 0,
                            id: 200,
                            label: '物流和保障',
                            checked: false,
                            children: [
                                {
                                    parentId: 200,
                                    id: 201,
                                    label: '重量',
                                    checked: true,
                                    children: null
                                },
                                {
                                    parentId: 200,
                                    id: 202,
                                    label: '尺寸',
                                    checked: true,
                                    children: null
                                },
                                {
                                    parentId: 200,
                                    id: 203,
                                    label: '服务期限',
                                    checked: false,
                                    children: null
                                },
                                {
                                    parentId: 200,
                                    id: 204,
                                    label: '服务条款',
                                    checked: false,
                                    children: null
                                }
                            ]
                        }
                    ]
                },
            ],
        }
    },
    methods: {
        onCheckboxChange(e, item, index, level) {
            let isChecked = e.target.checked
            // 根节点
            if (level == 1) {
                // 全选及取消全选
                this.getTreeList(this.checkModule, isChecked)
            }
            else if (level == 2) {
                // 全选及取消全选
                this.getTreeList(item.children, isChecked)
            }
            
            // 后序遍历 判断全选状态
            this.nextOrderTransversal(this.checkModule[0])
        },
        // 递归树状数据 修改选中状态
        getTreeList(treeList, isChecked) {
            treeList.forEach((item) => {
                item.checked = isChecked
                if (item.children && item.children.length > 0) {
                    this.getTreeList(item.children, isChecked)
                }
            })
        },
        // 后序遍历
        nextOrderTransversal(rnode) {
            if (rnode.children) {
                for (let v of rnode.children) {
                    this.nextOrderTransversal(v)
                }
                rnode.checked = this.judgeIsAllChecked(rnode)
            }
        },
        // 判断是否全选
        judgeIsAllChecked(treeList) {
            let flag = true
            if (treeList.children && treeList.children.length > 0) {
                treeList.children.forEach((item) => {
                    if (item.checked == false) {
                        flag = false
                    }
                })
            }
            return flag
        }
    },
}
</script>

<style lang="less" scoped>

</style>
```

### 52.antd 侧边栏默认固定

![image-20221020140517918](https://gitee.com/v876774538/my-img/raw/master/image-20221020140517918.png)

![image-20221020140540026](https://gitee.com/v876774538/my-img/raw/master/image-20221020140540026.png)

```js
  fixedHeader: true, // sticky header
  fixSiderbar: true, // sticky siderbar
```

### 53.antd 表格动态表头

#### 53.1 效果

![image-20221020165219853](https://gitee.com/v876774538/my-img/raw/master/image-20221020165219853.png)

需求：根据上方三级checkbox选择模块，动态添加/删除表头

#### 53.2 思路

1. 创建checkModule数组对象（树形结构），用于同时控制上方选择与下方表头

   **checked属性标志上方被选中的模块以及下方需要显示的模块**

   **hidden属性控制个别固定的，不通过checkbox控制添加或删除的表头**

   ```js
   checkModule: [
       {
           parentId: null,
           id: 0,
           title: '全部',
           checked: false,
           hidden: false,
           children: [
               {
                   parentId: 0,
                   id: 100,
                   title: '产品信息',
                   checked: true,
                   hidden: true,
                   children: [
                       {
                           parentId: 100,
                           id: 101,
                           title: '产品图片',
                           dataIndex: 'productImage',
                           key: 'productImage',
                           align: 'center',
                           checked: true,
                           hidden: false,
                           children: null
                       },
                       {
                           parentId: 100,
                           id: 102,
                           title: '产品标题',
                           dataIndex: 'productTitle',
                           key: 'title',
                           align: 'center',
                           checked: true,
                           hidden: false,
                           children: null
                       },
                   ]
               },
               {
                   parentId: 0,
                   id: 200,
                   title: '变种信息',
                   checked: false,
                   hidden: false,
                   children: [
                       {
                           parentId: 200,
                           id: 201,
                           title: '变种主题',
                           dataIndex: 'variantTheme',
                           key: 'variantTheme',
                           align: 'center',
                           checked: false,
                           hidden: false,
                           children: null,
                       },
                       {
                           parentId: 200,
                           id: 202,
                           title: '变种图',
                           dataIndex: 'variantImage',
                           key: 'variantImage',
                           align: 'center',
                           checked: false,
                           hidden: false,
                           children: null,
                       },
                       {
                           parentId: 200,
                           id: 203,
                           title: '变种名称',
                           dataIndex: 'variantName',
                           key: 'variantName',
                           align: 'center',
                           checked: true,
                           hidden: true,
                           children: null,
                       },
                       {
                           parentId: 200,
                           id: 204,
                           title: '变种SKU',
                           dataIndex: 'variantSku',
                           key: 'variantSku',
                           align: 'center',
                           checked: true,
                           hidden: true,
                           children: null,
                       },
                       {
                           parentId: 200,
                           id: 205,
                           title: '识别码',
                           dataIndex: 'identificationCode',
                           key: 'identificationCode',
                           align: 'center',
                           checked: true,
                           hidden: true,
                           children: null,
                       },
                       {
                           parentId: 200,
                           id: 206,
                           title: '价格',
                           dataIndex: 'price',
                           key: 'price',
                           align: 'center',
                           checked: true,
                           hidden: false,
                           children: null,
                       },
                       {
                           parentId: 200,
                           id: 207,
                           title: '库存',
                           dataIndex: 'stock',
                           key: 'stock',
                           align: 'center',
                           checked: true,
                           hidden: false,
                           children: null,
                       }
                   ]
               },
               {
                   parentId: 0,
                   id: 300,
                   title: '物流和保障',
                   checked: false,
                   hidden: false,
                   children: [
                       {
                           parentId: 300,
                           id: 301,
                           title: '重量',
                           dataIndex: 'weight',
                           key: 'weight',
                           align: 'center',
                           checked: true,
                           hidden: false,
                           children: null,
                       },
                       {
                           parentId: 300,
                           id: 302,
                           title: '尺寸',
                           dataIndex: 'size',
                           key: 'size',
                           align: 'center',
                           checked: true,
                           hidden: false,
                           children: null,
                       },
                       {
                           parentId: 300,
                           id: 303,
                           title: '服务期限',
                           dataIndex: 'serviceDeadline',
                           key: 'serviceDeadline',
                           align: 'center',
                           checked: false,
                           hidden: false,
                           children: null,
                       },
                       {
                           parentId: 300,
                           id: 304,
                           title: '服务条款',
                           dataIndex: 'serviceTerm',
                           key: 'serviceTerm',
                           align: 'center',
                           checked: false,
                           hidden: false,
                           children: null,
                       }
                   ]
               },
               {
                   parentId: 0,
                   id: 400,
                   title: '',
                   checked: true,
                   hidden: true,
                   children: [
                       {
                           parentId: 400,
                           id: 401,
                           title: '操作',
                           dataIndex: 'action',
                           key: 'action',
                           scopedSlots: { customRender: 'action' },
                           align: 'center',
                           checked: true,
                           hidden: true,
                           children: null
                       }
                   ]
   
               }
           ]
       },
   ],
   ```

2. 创建表头（这里写死的可能有点笨，可以优化一下）

   ```js
   createColumns() {
       // 第一层
       this.tempColumns = JSON.parse(JSON.stringify(this.checkModule[0].children))	// 深度拷贝，防止后续改动影响checkbox组
       this.filterColumns = this.tempColumns.filter((item) => {
           return item.checked || item.hidden || (item.children && item.children.length > 0 && item.children.some((child) => child.checked))
       // 过滤出被选中/隐藏固定显示/存在子级有被选中模块的 赋值给filterColumns
       })
       // 第二层
       this.filterColumns.forEach((item) => {
           if (item.children && item.children.length > 0) {
               item.children = item.children.filter((child) => {
                   return child.checked || item.hidden
               })
           }
       })
       // 过滤出被选中/隐藏固定显示的赋值给filterColumns.children
   },
   ```

3. checkbox变化时修改checkModule中的数据，同时调用创建表头函数重新进行渲染

   ```js
   // 三级多选
   onCheckboxChange(e, item, index, level) {
       let isChecked = e.target.checked
       // 根节点
       if (level == 1) {
           // 全选及取消全选
           this.getTreeList(this.checkModule, isChecked)
       }
       else if (level == 2) {
           // 全选及取消全选
           this.getTreeList(item.children, isChecked)
       }
   
       // 后序遍历
       this.nextOrderTransversal(this.checkModule[0])
       // 创建表头
       this.createColumns()
   },
   ```

#### 53.3 代码

```vue
<template>
    <div class="index">
        <div class="toolBar">
            <a-breadcrumb>
                <a-breadcrumb-item>产品采集箱</a-breadcrumb-item>
                <a-breadcrumb-item><a href="/productCollectionBox/siteProductCollectionBox">站点产品采集箱</a>
                </a-breadcrumb-item>
                <!-- <a-breadcrumb-item><a href="">全球产品采集箱</a></a-breadcrumb-item> -->
                <a-breadcrumb-item>批量编辑</a-breadcrumb-item>
            </a-breadcrumb>
            <a-space>
                <a-button type="default" class="btnGroup">一键翻译</a-button>
                <a-button type="primary" class="btnGroup">保存</a-button>
            </a-space>
        </div>
        <a-card :bordered="false" title="选择批量编辑的信息" class="checkModule_card">
            <tr v-for="(item1, index1) in checkModule" :key="item1.id" v-if="!item1.hidden">
                <td class="em">
                    <a-checkbox v-model:checked="item1.checked" @change="onCheckboxChange($event, item1, index1, 1)">
                        {{item1.title}}</a-checkbox>
                </td>
                <td v-for="(item2, index2) in item1.children" :key="item2.id" v-if="!item2.hidden">
            <tr>
                <td class="em" style="padding-bottom: 5px">
                    <a-checkbox v-model:checked="item2.checked" @change="onCheckboxChange($event, item2, index2, 2)">{{
                    item2.title }}</a-checkbox>
                </td>
            </tr>
            <tr v-for="(item3, index3) in item2.children" :key="item3.id" v-if="!item3.hidden">
                <td>
                    <a-checkbox v-model:checked="item3.checked" @change="onCheckboxChange($event, item3, index3, 3)">{{
                    item3.title }}</a-checkbox>
                </td>
            </tr>
            </td>
            </tr>
        </a-card>
        <a-table :columns="filterColumns" :data-source="dataSource" :pagination="pagination" :loading="loading"
            :rowKey="(record) => record.id" @change="onPageChange" class="table">

        </a-table>
    </div>
</template>

<script>
export default {
    name: 'PutGoodsOnSale',
    data() {
        return {
            checkModule: [
                {
                    parentId: null,
                    id: 0,
                    title: '全部',
                    checked: false,
                    hidden: false,
                    children: [
                        {
                            parentId: 0,
                            id: 100,
                            title: '产品信息',
                            checked: true,
                            hidden: true,
                            children: [
                                {
                                    parentId: 100,
                                    id: 101,
                                    title: '产品图片',
                                    dataIndex: 'productImage',
                                    key: 'productImage',
                                    align: 'center',
                                    checked: true,
                                    hidden: false,
                                    children: null
                                },
                                {
                                    parentId: 100,
                                    id: 102,
                                    title: '产品标题',
                                    dataIndex: 'productTitle',
                                    key: 'title',
                                    align: 'center',
                                    checked: true,
                                    hidden: false,
                                    children: null
                                },
                            ]
                        },
                        {
                            parentId: 0,
                            id: 200,
                            title: '变种信息',
                            checked: false,
                            hidden: false,
                            children: [
                                {
                                    parentId: 200,
                                    id: 201,
                                    title: '变种主题',
                                    dataIndex: 'variantTheme',
                                    key: 'variantTheme',
                                    align: 'center',
                                    checked: false,
                                    hidden: false,
                                    children: null,
                                },
                                {
                                    parentId: 200,
                                    id: 202,
                                    title: '变种图',
                                    dataIndex: 'variantImage',
                                    key: 'variantImage',
                                    align: 'center',
                                    checked: false,
                                    hidden: false,
                                    children: null,
                                },
                                {
                                    parentId: 200,
                                    id: 203,
                                    title: '变种名称',
                                    dataIndex: 'variantName',
                                    key: 'variantName',
                                    align: 'center',
                                    checked: true,
                                    hidden: true,
                                    children: null,
                                },
                                {
                                    parentId: 200,
                                    id: 204,
                                    title: '变种SKU',
                                    dataIndex: 'variantSku',
                                    key: 'variantSku',
                                    align: 'center',
                                    checked: true,
                                    hidden: true,
                                    children: null,
                                },
                                {
                                    parentId: 200,
                                    id: 205,
                                    title: '识别码',
                                    dataIndex: 'identificationCode',
                                    key: 'identificationCode',
                                    align: 'center',
                                    checked: true,
                                    hidden: true,
                                    children: null,
                                },
                                {
                                    parentId: 200,
                                    id: 206,
                                    title: '价格',
                                    dataIndex: 'price',
                                    key: 'price',
                                    align: 'center',
                                    checked: true,
                                    hidden: false,
                                    children: null,
                                },
                                {
                                    parentId: 200,
                                    id: 207,
                                    title: '库存',
                                    dataIndex: 'stock',
                                    key: 'stock',
                                    align: 'center',
                                    checked: true,
                                    hidden: false,
                                    children: null,
                                }
                            ]
                        },
                        {
                            parentId: 0,
                            id: 300,
                            title: '物流和保障',
                            checked: false,
                            hidden: false,
                            children: [
                                {
                                    parentId: 300,
                                    id: 301,
                                    title: '重量',
                                    dataIndex: 'weight',
                                    key: 'weight',
                                    align: 'center',
                                    checked: true,
                                    hidden: false,
                                    children: null,
                                },
                                {
                                    parentId: 300,
                                    id: 302,
                                    title: '尺寸',
                                    dataIndex: 'size',
                                    key: 'size',
                                    align: 'center',
                                    checked: true,
                                    hidden: false,
                                    children: null,
                                },
                                {
                                    parentId: 300,
                                    id: 303,
                                    title: '服务期限',
                                    dataIndex: 'serviceDeadline',
                                    key: 'serviceDeadline',
                                    align: 'center',
                                    checked: false,
                                    hidden: false,
                                    children: null,
                                },
                                {
                                    parentId: 300,
                                    id: 304,
                                    title: '服务条款',
                                    dataIndex: 'serviceTerm',
                                    key: 'serviceTerm',
                                    align: 'center',
                                    checked: false,
                                    hidden: false,
                                    children: null,
                                }
                            ]
                        },
                        {
                            parentId: 0,
                            id: 400,
                            title: '',
                            checked: true,
                            hidden: true,
                            children: [
                                {
                                    parentId: 400,
                                    id: 401,
                                    title: '操作',
                                    dataIndex: 'action',
                                    key: 'action',
                                    scopedSlots: { customRender: 'action' },
                                    align: 'center',
                                    checked: true,
                                    hidden: true,
                                    children: null
                                }
                            ]

                        }
                    ]
                },
            ],
            labelCol: { style: { width: '100px' } },
            form: {},

            filterColumns: [],  // 过滤后的表头
            tempColumns: [],    // 临时表头
            dataSource: [], // 表格资源
            loading: false, // 加载状态
            pagination: {
                pageSize: 10,
                total: 0,
                current: 1,
                showQuickJumper: true,
                showTotal: (total) => `共${this.pagination.total}条`,
                showSizeChanger: true,
                pageSizeOptions: ['10', '15', '20', '30'],
                onShowSizeChange: (current, pageSize) => (this.pagination.pageSize = pageSize),
                // hideOnSinglePage: true,	// 单页隐藏
            },

        }
    },
    computed: {
    },
    mounted() {
        this.createColumns()
    },
    methods: {
        // 三级多选
        onCheckboxChange(e, item, index, level) {
            let isChecked = e.target.checked
            // 根节点
            if (level == 1) {
                // 全选及取消全选
                this.getTreeList(this.checkModule, isChecked)
            }
            else if (level == 2) {
                // 全选及取消全选
                this.getTreeList(item.children, isChecked)
            }

            // 后序遍历
            this.nextOrderTransversal(this.checkModule[0])
            // 创建表头
            this.createColumns()
        },
        // 递归树状数据 修改选中状态
        getTreeList(treeList, isChecked) {
            treeList.forEach((item) => {
                if (!item.hidden) {
                    item.checked = isChecked
                }
                if (item.children && item.children.length > 0) {
                    this.getTreeList(item.children, isChecked)
                }
            })
        },
        // 后序遍历
        nextOrderTransversal(rnode) {
            if (rnode.children) {
                for (let v of rnode.children) {
                    this.nextOrderTransversal(v)
                }
                rnode.checked = this.judgeIsAllChecked(rnode)
            }
        },
        // 判断是否全选
        judgeIsAllChecked(treeList) {
            let flag = true
            if (treeList.children && treeList.children.length > 0) {
                treeList.children.forEach((item) => {
                    if (item.checked == false) {
                        flag = false
                    }
                })
            }
            return flag
        },
        // 创建表头
        createColumns() {
            // 第一层
            this.tempColumns = JSON.parse(JSON.stringify(this.checkModule[0].children))
            this.filterColumns = this.tempColumns.filter((item) => {
                return item.checked || item.hidden || (item.children && item.children.length > 0 && item.children.some((child) => child.checked))
            })
            // 第二层
            this.filterColumns.forEach((item) => {
                if (item.children && item.children.length > 0) {
                    item.children = item.children.filter((child) => {
                        return child.checked || item.hidden
                    })
                }
            })
        },
        // 表格
        // 翻页
        onPageChange(e) {
            this.pagination.current = e.current
            // 重新加载
        },
        // 清除批量勾选
        clearSelectRows() {
            this.selectedRowKeys = []
        },
    },
}
</script>

<style lang="less" scoped>
.em {
    font-weight: 600;
}

.index {
    .btnGroup {
        border-radius: 5px;
        width: 88px;
    }

    .toolBar {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 10px;
    }

    .main {
        /deep/.ant-card-body {
            display: flex;

        }

        .input {
            width: 250px;
        }
    }

    .checkModule_card {
        td {
            padding: 0px 10px;
        }
    }

    .table {
        margin-top: 20px;
    }
}
</style>
```

### 54.vue 拖拽插件 可拖放排序

#### 54.1 安装依赖插件npm

```
npm i -S vuedraggable
```

#### 54.2 使用组件

html

```html
<draggable v-model="myArray" class="drag">
  <transition-group>
    <div v-for="element in myArray" :key="element.id">{{element.name}}</div>
  </transition-group>
</draggable>
```

js

```js
import draggable from "vuedraggable";
export default {
    components: { draggable },
    data() {
      myArray: [
        { name: 1234567890, id: 1 },
        { name: 23467890, id: 2 },
        { name: 1234589, id: 3 },
        { name: 123678, id: 4 },
        { name: 134567890, id: 5 },
        { name: 1234567890, id: 6 },
        { name: 23467890, id: 7 },
        { name: 1234589, id: 8 },
        { name: 123678, id: 9 },
        { name: 134567890, id: 10 }
      ]
    };
}
```

css

```css
.drag {
  width: 300px;
  height: 500px;
  overflow: hidden;
  background: #42b983;
}
.drag div {
  font-size: 20px;
  padding: 20px;
  margin: 2px;
  border: 2px dashed red;
}
```

### 55.$router 路由跳转 打开新页面

```js
// 路由跳转
goPath(path, query) {
    this.$router.push({
        path: path,
        query: query,
    })
},

// 打开新页面
openPath(path, query) {
    let routeUrl = this.$router.resolve({
        path: path,
        query: query
    });
    window.open(routeUrl.href, '_blank');
}
```

### 56.溢出省略

#### 56.1 单行省略

```css
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;
```

#### 56.2 多行省略

```css
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3;
overflow: hidden;
```

### 57.数组对象根据某个属性值进行分组

#### 57.1 分组前

```json
[
    {
        "attributeId": "1",
        "attributeName": "Scent",
        "customValue": "135x85x76cm",
        "skuImg": {
            "id": "12321321321"
        }
    },
    {
        "attributeId": "2",
        "attributeName": "Specification",
        "customValue": "【岩板6mm】1桌8木椅"
    },
    {
        "attributeId": "1",
        "attributeName": "Scent",
        "customValue": "135x85x77cm",
        "skuImg": {
            "id": "111111"
        }
    }
]
```

#### 57.2 分组后

```json
[
    {
        "name": "Scent",
        "values": [
            {
                "attributeId": "1",
                "attributeName": "Scent",
                "customValue": "135x85x76cm",
                "skuImg": {
                    "id": "12321321321"
                }
            },
            {
                "attributeId": "1",
                "attributeName": "Scent",
                "customValue": "135x85x77cm",
                "skuImg": {
                    "id": "111111"
                }
            }
        ]
    },
    {
        "name": "Specification",
        "values": [
            {
                "attributeId": "2",
                "attributeName": "Specification",
                "customValue": "【岩板6mm】1桌8木椅"
            }
        ]
    }
]
```

#### 57.3 实现

```js
handleGrouping(sortData) {
    let tempArr = []	// 用于判断属性值的数组
    var newArr = []	// 构建的新数组
    sortData.forEach((item) => {
        // 判断item的属性值是否存在
        if (tempArr.indexOf(item.attributeName) === -1) {	// 不存在
            // push一个新的对象
            newArr.push({
                name: item.attributeName,
                values: [item]
            })
            tempArr.push(item.attributeName)
        }
        else {	// 存在
           	// 往已有的对象中push
            newArr[tempArr.indexOf(item.attributeName)].values.push(item)
        }
    })
    return newArr
},
```

### 58.js获取图片尺寸

```js
// 获取图片的宽高
getImageSize(url) {
  return new Promise((resolve, reject) => {
    var img = document.createElement("img");
    img.src = url;
    img.onload = () => {
      resolve({ width: img.naturalWidth, height: img.naturalHeight });
    };
    img.onerror = () => {
      reject({ width: undefined, height: undefined })
    }
  });
},
```

```js
this.form.picUrls.split('\n').forEach((item) => {
    if (item) {
      this.getImageSize(item).then((res) => {
        this.form.productImageList.push({
          url: item,
          width: res.width,
          height: res.height,
          checked: true
        })
        this.showOnlinePictureModal = false
      }).catch((err) => {
        this.form.productImageList.push({
          url: item,
          width: err.width,
          height: err.height,
          checked: true
        })
        this.showOnlinePictureModal = false
      })
    }
})
```

### 59.css文字平均铺满容器

```html
<view class="row">
    <view class="label">
        券码信息
    </view>
    <view class="val">
        ：宁乡木桶饭套餐
    </view>
</view>
```

```css
.label {
    min-width: 112rpx;
    text-align-last: justify;
    text-align: justify;
}
```

![image-20221130104118171](https://gitee.com/v876774538/my-img/raw/master/image-20221130104118171.png)

### 60.上传图片添加遮罩

```html
<a-upload v-if="!queryParam.logoUrls || queryParam.logoUrls == ''" accept=".jpg,.jpeg,.png,.JPG,.JPEG,.gif"
:customRequest="LogoImg" :showUploadList="false">
	<a-button class="selectBtn" style="width:100px;height:100px;">上传图片</a-button>
	</a-upload>
<div v-else class="image" style="width:100px; height:100px;" @click="handleImageDelete('logo')">
	<img :src="queryParam.logoUrls" alt="" style="width:100px; height:100px;" />
	<div class="mask"></div>
	<a-icon type="delete" class="delete" />
</div>
```

```css
.image {
  position: relative;
  cursor: pointer;

  .mask {
    position: absolute;
    top: 0;
    left: 0;
    background: #000;
    width: 100%;
    height: 100%;
    opacity: 0;
  }

  .delete {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-left: -10px;
    margin-top: -10px;
    font-size: 20px;
    // color: #f3f3f3;
    color: #fff;
    display: none;
  }
}

.image:hover {
  .mask {
    opacity: 0.3;
  }

  .delete {
    display: block;
  }
}
```

### 61.网页黑白过滤

```css
<style>
    html {
    filter:grayscale(100%);
    -webkit-filter:grayscale(100%);
    -moz-filter:grayscale(100%);
    -ms-filter:grayscale(100%);
    -o-filter:grayscale(100%);
    -webkit-filter:grayscale(1);
    }
</style>
```

### 62.CSS控制整个盒子占满屏幕

1. 给最外层的盒子设置绝对定位

   ```css
   div{
       position:absolute;
       top:0;
       left:0;
       right:0;
       bottom:0;
   }
   ```

2. 给html,body，div设置高度100%(在vue文件中，在index.html文件中设置该样式命令)

   ```css
   html,body,div{
       height:100%;
       box-sizing:border-box;
       padding: 0;
       margin: 0;
   }
   ```

3. 让一个盒子自适应填满剩下的高度，在该div加min-height：100vh即可

   ```css
   div{
       min-height:100vh
   }
   ```


### 63.监听localStorage 实现跨页面监听

#### 63.1 触发

```js
localStorage.setItem('imgUrl', data)
```

#### 63.2 监听localStorage

```js
created() {
// 监听
window.addEventListener('storage', (event) => {
  if (event.key == 'imgUrl' && this.editImg.url != event.newValue) {
	....
  }
})
},
```

### 64.上传图片 blob转file 添加name

```js
  let blob = new Blob([u8arr], { type: mime });
  let file = new File([blob], new Date().getTime() + '.png');
```

```js
editor.onSave(({
  files,
  workId,
  type,
  title
}) => {
  // 直接关闭编辑器
  editor.close();

  // 对结果进行下载
  const file = files[0];
  const url = URL.createObjectURL(file);
  const a = document.createElement('a');
  a.href = url;
  a.download = `${title}.${type}`
  //   a.click();
  let newFile = new File([file], title + '.' + type)  // 转file 添加name
  // console.log('file', file, title, type)
  console.log(newFile)
  iframeSendMsg(newFile)
})
```

### 65.解决message提示重复弹出的问题

先销毁上一个，再提示下一个

```js
this.$message.destroy()
this.$message.success('图片编辑成功！')
```

### 66.iframe内嵌html iframe通信

#### 66.1 使用iframe潜入HTML页面

```vue
<!-- 图片美化 -->
<template>
    <div class="wrap">
        <iframe ref="iframe" :src="htmlSrc" width="100%" height="50%" frameborder="0">
        </iframe>
    </div>
</template>

<script>
export default {
    name: 'ImageEditor',
    data() {
        return {
            htmlSrc: '',	// html地址
            imgUrl: ''
        }
    },
    computed: {
    },
    mounted() {
        // 获取url参数
        if (this.$route.query) {
            this.query = this.$route.query
            this.imgUrl = this.query.url
        }
        this.htmlSrc = window.location.origin + '/imageEditor/index.html?url=' + this.imgUrl
        // 接收返回的图片
        window.addEventListener('message', this.getIframeMsg)
    },
    methods: {
    },
}
</script>

<style lang="less" scoped>
// 占满整个页面
.wrap {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
}

html,
body,
div,
iframe {
    height: 100%;
    box-sizing: border-box;
    padding: 0;
    margin: 0;
}

iframe {
    min-height: 100vh
}
</style>
```

#### 66.2 相互通信

**vue文件完整代码**

```vue
<!-- 图片美化 -->
<template>
    <div class="wrap">
        <iframe ref="iframe" :src="htmlSrc" width="100%" height="50%" frameborder="0">
        </iframe>
    </div>
</template>

<script>
export default {
    name: 'ImageEditor',
    data() {
        return {
            htmlSrc: '',
            imgUrl: ''
        }
    },
    computed: {
    },
    mounted() {
        // 获取url参数
        if (this.$route.query) {
            this.query = this.$route.query
            this.imgUrl = this.query.url
        }
        this.htmlSrc = window.location.origin + '/imageEditor/index.html?url=' + this.imgUrl
        // 接收返回的图片
        window.addEventListener('message', this.getIframeMsg)
    },
    methods: {
        // vue获取iframe传递过来的信息
        getIframeMsg(event) {
            const res = event.data;
            console.log('iframe接收到', res)
            this.uploadImage(res, (data) => {
                localStorage.setItem('imgUrl', data)
                window.close()
            })
        },
        // 上传图片
        uploadImage(file, callback) {
            this.$message.loading({ content: '上传中，请稍后……', key: 'message', duration: 0 })
            const formData = new FormData()
            formData.append('file', file)
            this.$httpUpload(this.APIURL.ossUploadFile, formData).then((res) => {
                if (!res.success) {
                    this.$message.error({ content: res.message, key: 'message' })
                    return false
                }
                this.$message.success({ content: '上传完成！', key: 'message' })
                console.log('res.data', res.data)
                callback(res.data)
            }).catch((err) => {
                // this.$message.error({ content: err.message, key: 'message' })
            })
        }
    },
}
</script>

<style lang="less" scoped>
.wrap {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
}

html,
body,
div,
iframe {
    height: 100%;
    box-sizing: border-box;
    padding: 0;
    margin: 0;
}

iframe {
    min-height: 100vh
}
</style>
```

**html文件完整代码**

```html
<!DOCTYPE html>
<html>

<head>
  <script src="https://open.gaoding.com/assets/editor-sdk-v2.js"></script>
</head>

<body>
  <div id="app"></div>
  <script type="text/javascript">
    const editor = window.gaoding.createImageEditor({
      appId: 'AETSPW728866',
      container: '#app'
    });

    // 获取url链接中的参数
    function getQuery() {
      var url = window.location.href; //获取当前url
      console.log('url', url)
      var cs = url.split('?')[1]; //获取?之后的参数字符串
      var cs_arr = cs.split('&'); //参数字符串分割为数组
      var cs = {};
      for (var i = 0; i < cs_arr.length; i++) { //遍历数组，拿到json对象
        cs[cs_arr[i].split('=')[0]] = cs_arr[i].split('=')[1]
      }
      return cs;
    }

    function create() {
      // 获取图片
      var query = getQuery()
      editor.importImage(query.url);
    }

    // iframe向vue传递信息
    function iframeSendMsg(file) {
      window.parent.postMessage(file, '*');
    };


    create() // 创建
    // 保存
    editor.onSave(({
      files,
      workId,
      type,
      title
    }) => {
      // 直接关闭编辑器
      editor.close();

      // 对结果进行下载
      const file = files[0];
      const url = URL.createObjectURL(file);
      const a = document.createElement('a');
      a.href = url;
      a.download = `${title}.${type}`
      //   a.click();
      let newFile = new File([file], title + '.' + type)  // 转file 添加name
      // console.log('file', file, title, type)
      console.log(newFile)
      iframeSendMsg(newFile)
    })
  </script>
</body>

</html>
<style>
  .design-editor-page {
    position: absolute;
    top: 0;
    left: 0;
  }

  html,
  body,
  div {
    height: 100%;
    box-sizing: border-box;
    padding: 0;
    margin: 0;
  }

  div {
    min-height: 100vh
  }
</style>
```

### 67.git规范

![image-20221212165735498](https://gitee.com/v876774538/my-img/raw/master/image-20221212165735498.png)

#### 67.1 VScode git使用

##### 1.提交代码

1）打开下面视图，添加一行文字：

![img](https://pic3.zhimg.com/80/v2-5a76e90a9c7dca54234a5481b88c3462_720w.webp)

2）点击 + ；相当于`git add .`

![img](https://pic2.zhimg.com/80/v2-378ba2b1183a95d2851bf49228cb209d_720w.webp)

3）点击对号；等于`git commit -m "备注信息"`；右边的箭头输入需要备注的信息。然后按 Enter 确定：

![img](https://pic3.zhimg.com/80/v2-e3ddb9a972780427c6349f941aee259e_720w.webp)

回车之后，然后我们可以看到。所有的修改的文件，均已经提交到缓存区。1变成了0：

![img](https://pic1.zhimg.com/80/v2-d21cd824b5db226216011dd64ec0e860_720w.webp)

4）提交到远程仓库；**推送**：

![img](https://pic1.zhimg.com/80/v2-20e1a4a61484794189de3dcfa33b2870_720w.webp) 

##### 2.获取最新分支（命令行）

1. 查看本地所有分支

   ```
   git branch -a
   ```

2. 同步获取所有分支

   ```
   git fetch
   ```

3. 切换到远程同事的分支

   ```
   git checkout origin/XXX
   ```

   ![image-20230103094559832](https://gitee.com/v876774538/my-img/raw/master/image-20230103094559832.png)

### 68.模拟进度条  提示

#### 68.1 组件

```vue
<!-- 进度条 -->
<template>
    <a-modal :title="title" centered :visible="visible" @cancel="handleCancel">
        <template slot="footer">
            <div>
                <a-space>
                    <a-button type="primary" @click="handleOk" :loading="btnLoading">确定</a-button>
                </a-space>
            </div>
        </template>
        <div class="progress">
            <a-progress :percent="percent" :status="status"></a-progress>
        </div>
        <div class="tip" v-html="message ? message : '请求中，请稍后……'"></div>
    </a-modal>
</template>

<script>
export default {
    name: 'ProgressModal',
    props: {
        title: {
            type: String,
            required: true
        },
        visible: {
            type: Boolean,
            required: true
        },
        btnLoading: {
            type: Boolean,
            default: () => false
        },
        message: {
            type: String,
            default: () => '',
        },
        percent: {
            type: Number,
            required: true
        },
        status: {
            type: String,
            default: 'active',
        }
    },
    data() {
        return {
        }
    },
    methods: {
        handleOk() {
            this.$emit('ok')
        },
        handleCancel() {
            this.$emit('cancel')
        }
    },
}
</script>

<style lang="less" scoped>
.ant-modal-body {
    padding: 20px;
    box-sizing: border-box;
}
.tip {
    margin-top: 20px;
}
</style>
```

#### 68.2 使用

```html
<progress-modal v-if="showProgressModal" :visible="showProgressModal" :title="'同步产品'" :btnLoading="btnLoading"
    :message="message" :percent="percent" :status="status" @ok="showProgressModal = false"
    @cancel="showProgressModal = false"></progress-modal>
```

#### 68.3 模拟进度函数

```js
// 模拟进度
simulateUpdate() {
    this.status = 'active'
    this.percent = 0
    let that = this
    let timer = setInterval(function () {
        if (that.percent < 99) {
            that.percent++
        }
        else if (that.percent == 100) {
            clearInterval(timer)
        }
    }, 10)
},
```

#### 68.4 发起请求

```js
// 同步产品
handleSyncProduct() {
    this.btnLoading = true
    this.showProgressModal = true
    this.simulateUpdate()
    this.$httpGet(this.APIURL.dataMovingSyncProduct, {
        shopType: '1',  // 全球
        shopId: this.queryParams.shopId
    }).then((res) => {
        if (!res.success) {
            this.status = 'exception'
            this.percent = 100
            this.message = res.data
            setTimeout(() => {
                this.btnLoading = false
            }, 200)
            return false
        }
        this.status = 'success'
        this.percent = 100
        this.message = res.data
        this.btnLoading = false
        this.getDataMovingPage()
    }).catch((err) => {
        this.status = 'exception'
        this.percent = 100
        this.message = err.data
        setTimeout(() => {
            this.btnLoading = false
        }, 200)
    })
},
```

### 69.a-select同时支持下拉选项与手动输入

```html
<a-select show-search option-filter-prop="children" class="input2" :filter-option="filterOption"
    :autoClearSearchValue="false" @search="fetchUpdate" v-model="option.update">
    <span slot="suffixIcon">px</span>
    <a-select-option v-for="(item, index) in updateList" :key="index" :value="item">{{ item
    }}</a-select-option>
</a-select>
```

```js
filterOption(input, option) {
    return (
        option.componentOptions.children[0].text.toLowerCase().indexOf(input.toLowerCase()) >= 0
    );
},
fetchUpdate(value) {
    if (value) {
        this.option.update = Number(value)
        this.$forceUpdate()	// 必须 否则会被清空
    }
},
```

![image-20221214144554489](https://gitee.com/v876774538/my-img/raw/master/image-20221214144554489.png)

![image-20221214144614204](https://gitee.com/v876774538/my-img/raw/master/image-20221214144614204.png)

### 70.匹配、替换富文本中的图片

#### 70.1 匹配富文本图片 将图片放入数组

```js
let imgs = this.form.description && this.form.description.match(/<img\b.*?(?:\>|\/>)/gi)
if (imgs && imgs.length != 0) {
    var srcReg = /src=[\'\"]?([^\'\"]*)[\'\"]?/i
    var srcs = []
    imgs.forEach((item) => {
        srcs.push(item.match(srcReg)[1])
    })
    srcs.forEach((item) => {
        this.getImageSize(item).then((res) => {
            this.imageList.push({
                url: item,
                width: res.width,
                height: res.height,
                checked: true,
            })
        }).catch((err) => {
            this.imageList.push({
                url: item,
                width: err.width,
                height: err.height,
                checked: true,
            })
        })
    })
}
```

```js
// 获取图片的宽高
getImageSize(url) {
    return new Promise((resolve, reject) => {
        var img = document.createElement("img");
        img.src = url;
        img.onload = () => {
            resolve({ width: img.naturalWidth, height: img.naturalHeight });
        };
        img.onerror = () => {
            reject({ width: undefined, height: undefined })
        }
    });
},
```

![image-20221215151556703](https://gitee.com/v876774538/my-img/raw/master/image-20221215151556703.png)

#### 70.2 替换富文本图片

```js
    this.form.description = this.replaceImg(this.form.description, res)
```

```js
// 替换富文本图片
replaceImg(a, imageList) {
  let n = 0
  a = a.replace(/src=['"]([^'"]+)[^>]*>/gi, function (match, capture) {
    return 'src="' + imageList[n++].url + '"' + '>'
  });
  return a
},
```

### 71.修改图片尺寸

#### 71.1 两种调整方式

点击生成图片 → 修改图片尺寸 上传到阿里云 → 修改图片列表信息 → 点击确定 → 将图片列表传给父组件 → 父组件再修改对应的图片信息

![image-20221215151841536](https://gitee.com/v876774538/my-img/raw/master/image-20221215151841536.png)

![image-20221215151851215](https://gitee.com/v876774538/my-img/raw/master/image-20221215151851215.png)

#### 71.2 实现

一、获取生成图片宽高

1.等比例调整

参考边变化到设置长度，另一边按照图片原宽高比例调整

```js
this.imageList.filter((v) => v.checked).forEach((item, index) => {
    if (index == this.imageList.filter((v) => v.checked).length - 1) {
        isEnd = true
    }
    let newWidth = 0
    let newHeight = 0
    // 图片小边
    if (this.option.refer == '1') {
        if (item.width < item.height) {
            newWidth = this.option.update
            newHeight = (item.height * (newWidth / item.width)).toFixed(0) * 1
        }
        else {
            newHeight = this.option.update
            newWidth = (item.width * (newHeight / item.height)).toFixed(0) * 1
        }
    }
    // 图片大边
    else if (this.option.refer == '2') {
        if (item.width > item.height) {
            newWidth = this.option.update
            newHeight = (item.height * (newWidth / item.width)).toFixed(0) * 1
        }
        else {
            newHeight = this.option.update
            newWidth = (item.width * (newHeight / item.height)).toFixed(0) * 1
        }
    }
    this.resizeImage(item, newWidth, newHeight, isEnd)
})
```

2.自定义比例调整

同理，参考边变化到设置长度，另一边按照图片原宽高比例调整，设为画布的宽高

```js
this.imageList.filter((v) => v.checked).forEach((item, index) => {
    if (index == this.imageList.filter((v) => v.checked).length - 1) {
        isEnd = true
    }
    let newWidth = 0
    let newHeight = 0
    // 图片宽
    if (this.option.refer == '1') {
        newWidth = this.option.update
        // 比例换算
        let proportion = this.getProportion(item)
        newHeight = ((newWidth * (proportion[1] * 1)) / (proportion[0] * 1)).toFixed(0) * 1
    }
    // 图片高
    else if (this.option.refer == '2') {
        newHeight = this.option.update
        // 比例换算
        let proportion = this.getProportion(item)
        newWidth = ((newHeight * (proportion[0] * 1)) / (proportion[1] * 1)).toFixed(0) * 1
    }
    this.resizeImage(item, newWidth, newHeight, isEnd)
})
```

二、调整图片大小

1.等比例调整

图片根据设置好的宽高缩放即可

```js
let img = new Image()
img.src = item.url
img.width = newWidth
img.height = newHeight
img.setAttribute('crossOrigin', 'anonymous')
let canvas = document.createElement("canvas")
let context = canvas.getContext("2d")
canvas.width = newWidth
canvas.height = newHeight
img.onload = () => {
    context.drawImage(img, 0, 0, canvas.width, canvas.height)
    let image = canvas.toDataURL('image/jpg')
    let file = this.dataURLtoFile(image, '.jpg')
    // 上传
    this.uploadImage(file, (res) => {
        item.url = res
        item.width = newWidth
        item.height = newHeight
        this.$forceUpdate()
        if (isEnd) {
            this.status = 'success'
            this.percent = 100
            this.message = '尺寸调整完成！'
            this.btnLoading = false
        }
    })
}
```

2.自定义比例调整

画布宽高固定，将原图缩放后居中塞入画布（在两边补白）

```js
let img = new Image()
img.src = item.url
// 图片宽高
if (item.width > item.height) {
    img.width = newWidth
    img.height = ((newWidth / item.width) * item.height).toFixed(0) * 1
    if (img.height > newHeight) {
        img.height = newHeight
        img.width = ((newHeight / item.height) * item.width).toFixed(0) * 1
    }
}
else if (item.width == item.height) {
    if (newWidth < newHeight) {
        item.width = newWidth
        item.height = newWidth
    }
    else {
        item.width = newHeight
        item.height = newHeight
    }
}
else {
    img.height = newHeight
    img.width = ((newHeight / item.height) * item.width).toFixed(0) * 1
    if (img.width > newWidth) {
        img.width = newWidth
        img.height = ((newWidth / item.width) * item.height).toFixed(0) * 1
    }
}
img.setAttribute('crossOrigin', 'anonymous')
let canvas = document.createElement("canvas")
canvas.width = newWidth
canvas.height = newHeight
let context = canvas.getContext("2d")
// 转换为白底
const imageData = context.getImageData(0, 0, canvas.width, canvas.height)
for (let i = 0; i < imageData.data.length; i += 4) {
    // 当该像素是透明的，则设置成白色
    if (imageData.data[i + 3] === 0) {
        imageData.data[i] = 255;
        imageData.data[i + 1] = 255;
        imageData.data[i + 2] = 255;
        imageData.data[i + 3] = 255;
    }
}
context.putImageData(imageData, 0, 0)
img.onload = () => {
    let x = 0
    let y = 0
    // 计算坐标
    if (img.width < newWidth) {
        x = ((newWidth - img.width) / 2).toFixed(0) * 1
    }
    else {
        x = 0
    }
    if (img.height < newHeight) {
        y = ((newHeight - img.height) / 2).toFixed(0) * 1
    }
    else {
        y = 0
    }
    context.drawImage(img, x, y, img.width, img.height)
    let image = canvas.toDataURL('image/jpg')
    let file = this.dataURLtoFile(image, '.jpg')
    // 上传
    this.uploadImage(file, (res) => {
        item.url = res
        item.width = newWidth
        item.height = newHeight
        this.$forceUpdate()
        if (isEnd) {
            this.status = 'success'
            this.percent = 100
            this.message = '尺寸调整完成！'
            this.btnLoading = false
        }
    })
}

```

#### 71.3 完整组件代码

```vue
<!-- 调整图片尺寸设置 -->
<template>
    <a-modal title="调整尺寸设置" :visible="visible" @cancel="$emit('cancel')" :width="825">
        <template slot="footer">
            <a-space>
                <a-button type="default" @click="handleCancel">取消</a-button>
                <a-button type="primary" @click="handleOk">确定</a-button>
            </a-space>
        </template>
        <a-space>
            <a-select v-model="option.model" class="input1">
                <a-select-option value="1">等比例调整</a-select-option>
                <a-select-option value="2">自定义比例调整</a-select-option>
            </a-select>
            <!-- 等比例调整 -->
            <template v-if="option.model == '1'">
                <a-space>
                    <a-select v-model="option.refer" class="input2">
                        <a-select-option value="1">图片小边</a-select-option>
                        <a-select-option value="2">图片大边</a-select-option>
                    </a-select>
                    变化至
                    <a-select show-search option-filter-prop="children" class="input2" :filter-option="filterOption"
                        :autoClearSearchValue="false" @search="fetchUpdate" v-model="option.update">
                        <span slot="suffixIcon">px</span>
                        <a-select-option v-for="(item, index) in updateList" :key="index" :value="item">{{ item
                        }}</a-select-option>
                    </a-select>
                </a-space>
            </template>
            <!-- 自定义比例调整 -->
            <template v-else-if="option.model == '2'">
                <a-space>
                    <a-select v-model="option.refer" class="input2">
                        <a-select-option value="1">图片宽</a-select-option>
                        <a-select-option value="2">图片高</a-select-option>
                    </a-select>
                    变化至
                    <a-select show-search option-filter-prop="children" class="input2" :filter-option="filterOption"
                        :autoClearSearchValue="false" @search="fetchUpdate" v-model="option.update">
                        <span slot="suffixIcon">px</span>
                        <a-select-option v-for="(item, index) in updateList" :key="index" :value="item">{{ item
                        }}</a-select-option>
                    </a-select>
                    <a-select v-model="option.proportion" class="input1">
                        <a-select-option value="default">保持原图比例</a-select-option>
                        <a-select-option value="1:1">1:1</a-select-option>
                        <a-select-option value="3:4">3:4</a-select-option>
                        <a-select-option value="4:3">4:3</a-select-option>
                        <a-select-option value="9:16">9:16</a-select-option>
                        <a-select-option value="16:9">16:9</a-select-option>
                    </a-select>
                </a-space>
            </template>
            <a-button type="primary" @click="handleUpdate">生成图片</a-button>
        </a-space>
        <div class="content">
            <div class="productImageBox" v-for="(item, index) in imageList" v-if="item.url">
                <img :src="item.url" alt="" class="image">
                <a-checkbox :value="index" class="checkbox" :checked="item.checked"
                    @change="handleImageCheck($event, item)">
                </a-checkbox>
                <div class="line">{{ item.width }} × {{ item.height }}</div>
            </div>
        </div>
        <div class="tip" v-if="option.model == '2'">
            <a-space>
                <a-icon type="info-circle" theme="twoTone" />
                为保证图片内容不丢失，自定义比例调整会将图片设置比例放大/缩小后，再用白底填充另外两边
            </a-space>
        </div>
        <!-- 弹窗 -->
        <progress-modal v-if="showProgressModal" :visible="showProgressModal" :title="title" :btnLoading="btnLoading"
            :message="message" :percent="percent" :status="status" @ok="showProgressModal = false"
            @cancel="showProgressModal = false"></progress-modal>
    </a-modal>
</template>

<script>
import { isNone } from '@/utils/util';
import ProgressModal from '../../modules/ProgressModal.vue';

export default {
    name: 'ImageResizeModal',
    components: {
        ProgressModal,
    },
    props: {
        visible: {
            type: Boolean,
            required: true
        },
        form: {
            type: Object,
            default: () => { }
        },
        dataIndex: {
            type: String,
            default: () => ''
        }
    },
    data() {
        return {
            option: {
                model: '1', // 等比例调整
                refer: '1', // 图片小边/图片宽
                proportion: 'default',  // 图片比例
            },
            updateList: [600, 800],
            imageList: [],  // 图片列表

            // 进度条
            title: '',  // 标题
            message: '',    // 提示
            percent: 0, // 进度
            status: 'active',   // 状态
            btnLoading: false,  // 按钮加载状态
            showProgressModal: false,   // 进度条提示

        }
    },
    mounted() {
        // 获取图片列表
        if (this.dataIndex == 'productImage') {
            this.imageList = JSON.parse(JSON.stringify(this.form.productImageList))
        }
        else if (this.dataIndex == 'variantImage') {
            this.form.skus[0].salesAttributes.forEach((item => {
                if (item)
                    this.imageList.push({
                        url: item.skusImg.url,
                        width: item.skusImg.width,
                        height: item.skusImg.height,
                        checked: item.skusImg.url != '' ? true : false
                    })
            }))
        }
        else if (this.dataIndex == 'description') {
            let imgs = this.form.description && this.form.description.match(/<img\b.*?(?:\>|\/>)/gi)
            if (imgs && imgs.length != 0) {
                var srcReg = /src=[\'\"]?([^\'\"]*)[\'\"]?/i
                var srcs = []
                imgs.forEach((item) => {
                    srcs.push(item.match(srcReg)[1])
                })
                srcs.forEach((item) => {
                    this.getImageSize(item).then((res) => {
                        this.imageList.push({
                            url: item,
                            width: res.width,
                            height: res.height,
                            checked: true,
                        })
                    }).catch((err) => {
                        this.imageList.push({
                            url: item,
                            width: err.width,
                            height: err.height,
                            checked: true,
                        })
                    })
                })
            }
        }
    },
    methods: {
        // 模拟进度
        simulateUpdate() {
            this.status = 'active'
            this.percent = 0
            let that = this
            let timer = setInterval(function () {
                if (that.percent < 99) {
                    that.percent++
                }
                else if (that.percent == 100) {
                    clearInterval(timer)
                }
            }, 10)
        },
        filterOption(input, option) {
            return (
                option.componentOptions.children[0].text.toLowerCase().indexOf(input.toLowerCase()) >= 0
            );
        },
        fetchUpdate(value) {
            if (value) {
                this.option.update = Number(value)
                this.$forceUpdate()
            }
        },
        handleImageCheck(e, item) {
            item.checked = e.target.checked
        },
        // 获取图片的宽高
        getImageSize(url) {
            return new Promise((resolve, reject) => {
                var img = document.createElement("img");
                img.src = url;
                img.onload = () => {
                    resolve({ width: img.naturalWidth, height: img.naturalHeight });
                };
                img.onerror = () => {
                    reject({ width: undefined, height: undefined })
                }
            });
        },
        // 生成图片
        handleUpdate() {
            console.log(this.option)
            // 校验
            if (isNone(this.option.update)) {
                this.$message.info('请填写变化值')
                return false
            }
            this.btnLoading = true
            this.showProgressModal = true
            this.title = '调整尺寸'
            this.message = "尺寸调整中，请稍后……"
            this.simulateUpdate()
            let isEnd = false
            // 等比例调整
            if (this.option.model == '1') {
                this.imageList.filter((v) => v.checked).forEach((item, index) => {
                    if (index == this.imageList.filter((v) => v.checked).length - 1) {
                        isEnd = true
                    }
                    let newWidth = 0
                    let newHeight = 0
                    // 图片小边
                    if (this.option.refer == '1') {
                        if (item.width < item.height) {
                            newWidth = this.option.update
                            newHeight = (item.height * (newWidth / item.width)).toFixed(0) * 1
                        }
                        else {
                            newHeight = this.option.update
                            newWidth = (item.width * (newHeight / item.height)).toFixed(0) * 1
                        }
                    }
                    // 图片大边
                    else if (this.option.refer == '2') {
                        if (item.width > item.height) {
                            newWidth = this.option.update
                            newHeight = (item.height * (newWidth / item.width)).toFixed(0) * 1
                        }
                        else {
                            newHeight = this.option.update
                            newWidth = (item.width * (newHeight / item.height)).toFixed(0) * 1
                        }
                    }
                    this.resizeImage(item, newWidth, newHeight, isEnd)
                })
            }
            // 自定义比例调整
            else if (this.option.model == '2') {
                this.imageList.filter((v) => v.checked).forEach((item, index) => {
                    if (index == this.imageList.filter((v) => v.checked).length - 1) {
                        isEnd = true
                    }
                    let newWidth = 0
                    let newHeight = 0
                    // 图片宽
                    if (this.option.refer == '1') {
                        newWidth = this.option.update
                        // 比例换算
                        let proportion = this.getProportion(item)
                        newHeight = ((newWidth * (proportion[1] * 1)) / (proportion[0] * 1)).toFixed(0) * 1
                    }
                    // 图片高
                    else if (this.option.refer == '2') {
                        newHeight = this.option.update
                        // 比例换算
                        let proportion = this.getProportion(item)
                        newWidth = ((newHeight * (proportion[0] * 1)) / (proportion[1] * 1)).toFixed(0) * 1
                    }
                    this.resizeImage(item, newWidth, newHeight, isEnd)
                })
            }
        },
        resizeImage(item, newWidth, newHeight, isEnd) {
            // 等比例调整
            if (this.option.model == '1') {
                let img = new Image()
                img.src = item.url
                img.width = newWidth
                img.height = newHeight
                img.setAttribute('crossOrigin', 'anonymous')
                let canvas = document.createElement("canvas")
                let context = canvas.getContext("2d")
                canvas.width = newWidth
                canvas.height = newHeight
                img.onload = () => {
                    context.drawImage(img, 0, 0, canvas.width, canvas.height)
                    let image = canvas.toDataURL('image/jpg')
                    let file = this.dataURLtoFile(image, '.jpg')
                    // 上传
                    this.uploadImage(file, (res) => {
                        item.url = res
                        item.width = newWidth
                        item.height = newHeight
                        this.$forceUpdate()
                        if (isEnd) {
                            this.status = 'success'
                            this.percent = 100
                            this.message = '尺寸调整完成！'
                            this.btnLoading = false
                        }
                    })
                }
            }
            // 自定义比例调整
            else if (this.option.model == '2') {
                let img = new Image()
                img.src = item.url
                // 图片宽高
                if (item.width > item.height) {
                    img.width = newWidth
                    img.height = ((newWidth / item.width) * item.height).toFixed(0) * 1
                    if (img.height > newHeight) {
                        img.height = newHeight
                        img.width = ((newHeight / item.height) * item.width).toFixed(0) * 1
                    }
                }
                else if (item.width == item.height) {
                    if (newWidth < newHeight) {
                        item.width = newWidth
                        item.height = newWidth
                    }
                    else {
                        item.width = newHeight
                        item.height = newHeight
                    }
                }
                else {
                    img.height = newHeight
                    img.width = ((newHeight / item.height) * item.width).toFixed(0) * 1
                    if (img.width > newWidth) {
                        img.width = newWidth
                        img.height = ((newWidth / item.width) * item.height).toFixed(0) * 1
                    }
                }
                img.setAttribute('crossOrigin', 'anonymous')
                let canvas = document.createElement("canvas")
                canvas.width = newWidth
                canvas.height = newHeight
                let context = canvas.getContext("2d")
                // 转换为白底
                const imageData = context.getImageData(0, 0, canvas.width, canvas.height)
                for (let i = 0; i < imageData.data.length; i += 4) {
                    // 当该像素是透明的，则设置成白色
                    if (imageData.data[i + 3] === 0) {
                        imageData.data[i] = 255;
                        imageData.data[i + 1] = 255;
                        imageData.data[i + 2] = 255;
                        imageData.data[i + 3] = 255;
                    }
                }
                context.putImageData(imageData, 0, 0)
                img.onload = () => {
                    let x = 0
                    let y = 0
                    // 计算坐标
                    if (img.width < newWidth) {
                        x = ((newWidth - img.width) / 2).toFixed(0) * 1
                    }
                    else {
                        x = 0
                    }
                    if (img.height < newHeight) {
                        y = ((newHeight - img.height) / 2).toFixed(0) * 1
                    }
                    else {
                        y = 0
                    }
                    context.drawImage(img, x, y, img.width, img.height)
                    let image = canvas.toDataURL('image/jpg')
                    let file = this.dataURLtoFile(image, '.jpg')
                    // 上传
                    this.uploadImage(file, (res) => {
                        item.url = res
                        item.width = newWidth
                        item.height = newHeight
                        this.$forceUpdate()
                        if (isEnd) {
                            this.status = 'success'
                            this.percent = 100
                            this.message = '尺寸调整完成！'
                            this.btnLoading = false
                        }
                    })
                }
            }

        },
        getProportion(item) {
            let proportion = 1
            // 原图比例
            if (this.option.proportion == 'default') {
                proportion = [item.width, item.height]
            }
            else {
                proportion = this.option.proportion.split(':')
            }
            return proportion
        },
        // dataURL转file
        dataURLtoFile(dataUrl, fileName) {
            var arr = dataUrl.split(','), mime = arr[0].match(/:(.*?);/)[1],
                bstr = atob(arr[1]), n = bstr.length, u8arr = new Uint8Array(n);
            while (n--) {
                u8arr[n] = bstr.charCodeAt(n);
            }
            return new File([u8arr], fileName, { type: mime });
        },
        // 上传图片
        uploadImage(file, callback) {
            const formData = new FormData()
            formData.append('file', file)
            this.$httpUpload(this.APIURL.ossUploadFile, formData).then((res) => {
                if (!res.success) {
                    this.status = 'exception'
                    this.percent = 100
                    this.message = '调整尺寸失败！'
                    setTimeout(() => {
                        this.btnLoading = false
                    }, 200)
                    return false
                }
                callback(res.data)
            }).catch((err) => {
                this.status = 'exception'
                this.percent = 100
                this.message = '调整尺寸失败！'
                setTimeout(() => {
                    this.btnLoading = false
                }, 200)
            })
        },
        handleOk() {
            this.$emit('ok', this.imageList)
        },
        handleCancel() {
            this.$emit('cancel')
        },
    },
}
</script>

<style lang="less" scoped>
.input1 {
    width: 200px;
}

.input2 {
    width: 100px;
}

.tip {
    margin-top: 20px;
}

.content {
    display: flex;
    flex-wrap: wrap;
    margin-top: 20px;

    .productImageBox {
        position: relative;
        border: 1px solid #e8e8e8;
        // width: 120px;
        // height: 147px;
        // overflow: hidden;
        margin-right: 10px;
        margin-bottom: 10px;
        cursor: pointer;

        .image {
            width: 100px;
            height: 100px;
            overflow: hidden;
            position: relative;

            img {
                width: 100%;
                height: 100%;
            }

        }

        .checkbox {
            position: absolute;
            top: 2px;
            left: 5px;
        }

        .line {
            position: absolute;
            bottom: 0;
            width: 100px;
            height: 20px;
            line-height: 20px;
            background: rgba(0, 0, 0, 0.5);
            color: #fff;
            padding: 0 10px;
            box-sizing: border-box;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }
    }

    .productImageBox:nth-child(7n) {
        margin-right: 0;
    }
}
</style>
```

### 72.antd a-upload限制上传的文件类型/校验上传的文件类型

#### 72.1 限制上传文件类型

![image-20221216102520532](https://gitee.com/v876774538/my-img/raw/master/image-20221216102520532.png)

```html
<a-upload :customRequest="uploadMyWaterRemark" :show-upload-list="false" accept=".jpg,.jpeg,.png,.gif,.GIF,.JPG,.PNG">
    <div v-if="form.imgUrl" class="image">
        <img :src="form.imgUrl" alt="">
    </div>
    <div v-else class="image">
        <div class="addImage">
            <a-icon type="plus" class="icon"></a-icon>
            添加图片
        </div>
    </div>
</a-upload>
```

#### 72.2 校验上传的文件类型

```js
// 判断文件类型
checkImgType(file) {
    //用文件名name后缀判断文件类型，可用size属性判断文件大小不能超过500k ， 前端直接判断的好处，免去服务器的压力。 
    if (!/\.(jpg|jpeg|png|GIF|JPG|PNG)$/.test(file.name)) {
        return false;
    } else {
        return true;
    }
},
```

### 73.生成水印

#### 73.1 代码

```vue
<!-- 创建水印 -->
<template>
    <div class="index">
        <div class="left">
            <a-card :bordered="false" class="card">
                <a-form :form="form" layout="inline" :label-col="{ style: { width: '85px' } }">
                    <a-row>
                        <a-form-item label="模板名称" required>
                            <a-input v-model="form.name" placeholder="请输入模板名称" class="input"></a-input>
                        </a-form-item>
                    </a-row>
                    <a-row>
                        <a-form-item label="水印类型">
                            <a-radio-group v-model="form.type" @change="onTypeChange">
                                <a-radio :value="1">水印图片</a-radio>
                                <a-radio :value="2">水印文字</a-radio>
                            </a-radio-group>
                        </a-form-item>
                    </a-row>
                    <div v-if="form.type == 1">
                        <a-row>
                            <a-form-item label="我的水印" required>
                                <a-upload :customRequest="uploadMyWaterRemark" :show-upload-list="false"
                                    accept=".jpg,.jpeg,.png,.gif,.GIF,.JPG,.PNG">
                                    <div v-if="form.imgUrl" class="image">
                                        <img :src="form.imgUrl" alt="">
                                    </div>
                                    <div v-else class="image">
                                        <div class="addImage">
                                            <a-icon type="plus" class="icon"></a-icon>
                                            添加图片
                                        </div>
                                    </div>
                                </a-upload>
                                <div class="tip">
                                    <a-space>
                                        <a-icon type="info-circle" theme="twoTone" />
                                        建议上传透明底的png格式图片！
                                    </a-space>
                                </div>
                            </a-form-item>
                        </a-row>
                        <a-row>
                            <a-form-item label="水印位置" required>
                                <a-radio-group v-model="form.defaultLocation" class="locationTable">
                                    <table>
                                        <tr>
                                            <td v-for="(item, index) in locationList.slice(0, 3)" :key="index"
                                                @click="onLocationChange(item.value)">
                                                <a-radio :value="item.value"></a-radio>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td v-for="(item, index) in locationList.slice(3, 6)" :key="index"
                                                @click="onLocationChange(item.value)">
                                                <a-radio :value="item.value"></a-radio>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td v-for="(item, index) in locationList.slice(6, 9)" :key="index"
                                                @click="onLocationChange(item.value)">
                                                <a-radio :value="item.value"></a-radio>
                                            </td>
                                        </tr>
                                    </table>
                                </a-radio-group>
                            </a-form-item>
                        </a-row>
                        <a-row>
                            <a-form-item label="水印调整">
                                <a-space>
                                    <a-slider v-model="form.resize" :min="20" :max="200" :range="false"
                                        style="width: 190px" @change="onImageResizeChange"></a-slider>
                                    {{ form.resize }}%
                                </a-space>
                                <div class="tip">
                                    <a-space>
                                        <a-icon type="info-circle" theme="twoTone" />
                                        鼠标滚轮可调整水印大小！
                                    </a-space>
                                </div>
                            </a-form-item>
                        </a-row>
                    </div>
                    <div v-else-if="form.type == 2">
                        <a-row>
                            <a-form-item label="水印内容" required>
                                <a-input v-model="form.content" placeholder="请输入水印内容" class="input"
                                    @change="onTextChange" :maxLength="20"></a-input>
                            </a-form-item>
                        </a-row>
                        <a-row>
                            <a-form-item label="字体类型">
                                <a-select v-model="form.fontFamily" class="input" @change="onTextChange()">
                                    <a-select-option v-for="(item, index) in fontFamilyList" :key="index"
                                        :value="item.val">{{ item.name }}</a-select-option>
                                </a-select>
                            </a-form-item>
                        </a-row>
                        <a-row>
                            <a-form-item label="字体大小">
                                <a-select v-model="form.fontSize" class="input" @change="onTextChange()">
                                    <a-select-option v-for="(item, index) in fontSizeList" :key="index" :value="item">{{
                                            item
                                    }}</a-select-option>
                                </a-select>
                            </a-form-item>
                        </a-row>
                        <a-row>
                            <a-form-item label="字体颜色">
                                <colorPicker v-model="form.color" v-on:change="onTextChange()"></colorPicker>
                            </a-form-item>
                        </a-row>
                        <a-row>
                            <a-form-item label="水印位置" required>
                                <a-radio-group v-model="form.defaultLocation" class="locationTable">
                                    <table>
                                        <tr>
                                            <td v-for="(item, index) in locationList.slice(0, 3)" :key="index"
                                                @click="onLocationChange(item.value)">
                                                <a-radio :value="item.value"></a-radio>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td v-for="(item, index) in locationList.slice(3, 6)" :key="index"
                                                @click="onLocationChange(item.value)">
                                                <a-radio :value="item.value"></a-radio>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td v-for="(item, index) in locationList.slice(6, 9)" :key="index"
                                                @click="onLocationChange(item.value)">
                                                <a-radio :value="item.value"></a-radio>
                                            </td>
                                        </tr>
                                    </table>
                                </a-radio-group>
                            </a-form-item>
                        </a-row>
                    </div>
                </a-form>
            </a-card>
            <a-space class="btnGroup">
                <a-button type="default" class="btn" @click="handleCancel">取消</a-button>
                <a-button type="primary" class="btn" @click="handleSubmit">保存</a-button>
            </a-space>
        </div>
        <div class="right">
            <a-select class="canvasChange" placeholder="请选择底图尺寸" v-model="form.canvasSize" @change="onCanvasSizeChange">
                <a-select-option :value="1">600*600</a-select-option>
                <a-select-option :value="2">800*800</a-select-option>
            </a-select>
            <div class="canvas" :style="'width:' + canvasWidth + 'px;height:' + canvasHeight + 'px;'">
                <canvas ref="waterMarkCanvas" :width="canvasWidth" :height="canvasHeight"
                    :style="'width:' + canvasWidth + 'px;height:' + canvasHeight + 'px;' + 'border:1px solid #D9D9D9;'"></canvas>
            </div>
        </div>
        <!-- <a-button type="primary" @click="createWaterMark">保存</a-button> -->
    </div>

</template>
  
<script>
import { isNone } from '@/utils/util';
import { accAdd, accSub, accMul, accDiv } from '@/utils/util';

export default {
    name: 'laborImage',
    components: {
    },
    data() {
        return {
            query: {},  // url参数
            form: {
                type: 1,  // 水印类型
                resize: 100,
                defaultLocation: '1,1',
                canvasSize: 1,
                fontFamily: 'Microsoft Yahei',
                fontSize: 13,
                color: '#000'
            },   // 表单
            locationList: [
                {
                    name: 'topLeft',
                    value: '1,1',
                },
                {
                    name: 'top',
                    value: '3,1',
                },
                {
                    name: 'topRight',
                    value: '5,1',
                },
                {
                    name: 'left',
                    value: '1,3',
                },
                {
                    name: 'center',
                    value: '3,3',
                },
                {
                    name: 'right',
                    value: '5,3'
                },
                {
                    name: 'bottomLeft',
                    value: '1,5',
                },
                {
                    name: 'bottom',
                    value: '3,5',
                },
                {
                    name: 'bottomRight',
                    value: '5,5'
                }
            ],

            canvasWidth: 600, // 画布大小
            canvasHeight: 600,
            extraImgList: [
                {
                    url: '',
                    x: 0,
                    y: 0,
                    width: 0,
                    height: 0,
                }
                // { url: 'https://www.surely.cool/surely-vue-logo.png', x: 0, y: 0, width: 100, height: 100 },
            ],
            myCanvas: null,
            ctx: null,
            imgObject: [],
            imgX: 0, // 图片在画布中渲染的起点x坐标
            imgY: 0,
            imgScale: 1, // 图片的缩放大小
            imageSize: {},  // 图片大小
            defaultLocation: {},    // 默认图片位置

            fontFamilyList: [
                {
                    name: '微软雅黑',
                    val: 'Microsoft Yahei'
                },
                {
                    name: '仿宋',
                    val: 'FangSong'
                },
                {
                    name: '宋体',
                    val: 'SimSun'
                },
                {
                    name: '黑体',
                    val: 'SimHei'
                },
                {
                    name: '楷体',
                    val: 'KaiTi'
                },
                {
                    name: '幼圆',
                    val: 'YouYuan'
                }
            ],  // 字体类型选择
            fontSizeList: [12, 13, 14, 16, 18, 24, 30, 36, 48, 60],   // 字体大小选择
        }
    },
    mounted() {
        this.myCanvas = this.$refs.waterMarkCanvas;
        this.ctx = this.myCanvas.getContext('2d');
        // 获取query参数
        if (this.$route.query) {
            this.query = this.$route.query
            // 编辑回显
            if (this.query.record) {
                let record = JSON.parse(this.query.record)
                console.log('record', record)
                this.form = {
                    id: record.id,
                    name: record.name,
                    type: record.type,
                    content: record.content,
                    defaultLocation: record.defaultLocation,
                    canvasSize: record.canvasSize,
                    fontFamily: record.fontFamily,
                    fontSize: record.fontSize,
                    color: record.fontColor ? record.fontColor : '#000',
                    resize: accMul(record.imgScale, 100).toFixed(0) * 1
                }

                this.defaultLocation = {
                    x: record.defaultX,
                    y: record.defaultY
                }

                this.canvasWidth = this.form.canvasSize == 1 ? 600 : 800
                this.canvasHeight = this.form.canvasSize == 1 ? 600 : 800

                if (this.form.type == 1) {
                    this.extraImgList = []
                    this.extraImgList.push({
                        url: record.url,
                        width: record.width,
                        height: record.height,
                        x: record.defaultX,
                        y: record.defaultY
                    })
                    this.imgScale = record.imgScale
                    this.form.imgUrl = record.url

                    this.imageSize.width = accMul(this.extraImgList[0].width, this.imgScale)
                    this.imageSize.height = accMul(this.extraImgList[0].height, this.imgScale)

                }
                this.imgX = record.imgX
                this.imgY = record.imgY
                this.loadImg();
                this.canvasEventsInit();

            }
        }

    },
    methods: {
        loadImg() {
            var _this = this;
            // 水印图片
            if (this.form.type == 1) {
                let extraImgList = _this.extraImgList;
                let length = extraImgList.length;
                var imageList = [];
                let count = 0;
                //加载背景图片
                var img = new Image();
                var bgImg = extraImgList[0];
                img.src = bgImg.url;
                img.crossOrigin = "Anonymous";  // 解决画布污染
                img.onload = () => {
                    console.log('onload')
                    imageList.push({ url: img, x: bgImg.x, y: bgImg.y, width: bgImg.width, height: bgImg.height });
                    ++count;
                    if (length > 1) {
                        //加载剩余图片
                        for (let key = 1; key < length; key++) {
                            let item = extraImgList[key];
                            let extraImg = new Image();
                            extraImg.src = item.url;
                            extraImg.crossOrigin = "Anonymous";
                            extraImg.onload = () => {
                                imageList.push({ url: extraImg, x: item.x, y: item.y, width: item.width, height: item.height })
                                if (++count >= length) {
                                    _this.imgObject = imageList;
                                    _this.drawImage(imageList);
                                }
                            }
                        }
                    } else {
                        _this.imgObject = imageList;
                        _this.drawImage(imageList);
                    }
                }
            }
            // 水印文字
            else if (this.form.type == 2) {
                this.drawImage()
            }
        },
        drawImage(imgList) {
            var _this = this;
            _this.ctx.clearRect(0, 0, this.canvasWidth, this.canvasHeight);
            // 水印图片
            if (this.form.type == 1) {
                for (let i = 0; i < imgList.length; i++) {
                    console.log('x, y', _this.imgX + imgList[i].x * _this.imgScale, _this.imgY + imgList[i].y * _this.imgScale)
                    // imgList[i].x imgList[i].y 绘图起始坐标
                    _this.ctx.drawImage(
                        imgList[i].url, //规定要使用的图片
                        _this.imgX + imgList[i].x * _this.imgScale, _this.imgY + imgList[i].y * _this.imgScale,//   在画布上放置图像的 x 、y坐标位置。
                        imgList[i].width * _this.imgScale, imgList[i].height * _this.imgScale //    要使用的图像的宽度、高度
                    );
                }
            }
            // 水印文字
            else if (this.form.type == 2) {
                this.ctx.font = this.form.fontSize + 'px ' + this.form.fontFamily;
                this.ctx.fillStyle = this.form.color
                let defaultLocation = this.getTextDefaultLocation()
                console.log('x', defaultLocation.x, this.imgX, defaultLocation.x + this.imgX)
                console.log('y', defaultLocation.y, this.imgY, defaultLocation.y + this.imgY)
                this.ctx.fillText(this.form.content, defaultLocation.x + this.imgX, defaultLocation.y + this.imgY)
            }
            this.$forceUpdate()
            // this.ctx.font="15px Arial";
            // this.ctx.fillStyle = "black"
            // this.ctx.fillText("name",this.imgX + 120 * this.imgScale, this.imgY+ 25 * this.imgScale);
        },
        /**
         * 为画布上鼠标的拖动和缩放注册事件
        */
        canvasEventsInit() {
            var _this = this;
            var canvas = _this.myCanvas;

            canvas.onmousedown = function (event) {
                var imgx = _this.imgX;
                var imgy = _this.imgY;
                var pos = { x: event.clientX, y: event.clientY };  // 坐标转换，将窗口坐标转换成canvas的坐标
                canvas.onmousemove = function (evt) {  //移动
                    canvas.style.cursor = 'move';
                    var x = (evt.clientX - pos.x) + imgx;
                    var y = (evt.clientY - pos.y) + imgy;
                    var defaultX = _this.defaultLocation.x
                    var defaultY = _this.defaultLocation.y    // 偏移
                    defaultX = accMul(_this.defaultLocation.x, _this.imgScale).toFixed(2) * 1
                    defaultY = accMul(_this.defaultLocation.y, _this.imgScale).toFixed(2) * 1

                    _this.imgX = x.toFixed(2) * 1;
                    _this.imgY = y.toFixed(2) * 1;
                    // 不允许超出范围
                    if (_this.form.type == 1) {
                        if (x <= accSub(0, defaultX).toFixed(2) * 1) {
                            _this.imgX = accSub(0, defaultX).toFixed(2) * 1
                        }
                        if (x >= accSub(accSub(_this.canvasWidth, _this.imageSize.width), defaultX).toFixed(2) * 1) {
                            _this.imgX = accSub(accSub(_this.canvasWidth, _this.imageSize.width), defaultX).toFixed(2) * 1
                        }
                        if (y <= accSub(0, defaultY).toFixed(2) * 1) {
                            _this.imgY = accSub(0, defaultY).toFixed(2) * 1
                        }
                        if (y >= accSub(accSub(_this.canvasHeight, _this.imageSize.height), defaultY).toFixed(2) * 1) {
                            _this.imgY = accSub(accSub(_this.canvasHeight, _this.imageSize.height), defaultY).toFixed(2) * 1
                        }
                    }
                    else if (_this.form.type == 2) {
                        // 文字占据面积
                        let width = _this.ctx.measureText(_this.form.content).width
                        let height = _this.form.fontSize
                        if (x <= accSub(0, _this.defaultLocation.x).toFixed(2) * 1) {
                            _this.imgX = accSub(0, _this.defaultLocation.x).toFixed(2) * 1
                        }
                        if (x >= accSub(accSub(_this.canvasWidth, width), _this.defaultLocation.x).toFixed(2) * 1) {
                            _this.imgX = accSub(accSub(_this.canvasWidth, width), _this.defaultLocation.x).toFixed(2) * 1
                        }
                        if (y <= accAdd(accSub(0, _this.defaultLocation.y), height).toFixed(2) * 1) {
                            _this.imgY = accAdd(accSub(0, _this.defaultLocation.y), height).toFixed(2) * 1
                        }
                        if (y >= accSub(_this.canvasHeight, _this.defaultLocation.y).toFixed(2) * 1 - height * 0.1) {
                            _this.imgY = accSub(_this.canvasHeight, _this.defaultLocation.y).toFixed(2) * 1 - height * 0.1
                        }
                    }
                    // console.log(_this.imgX, _this.imgY)
                    _this.drawImage(_this.imgObject);  //重新绘制图片
                };
                canvas.onmouseup = function () {
                    canvas.onmousemove = null;
                    canvas.onmouseup = null;
                    canvas.style.cursor = 'default';
                };
            };

            canvas.onmousewheel = canvas.onwheel = function (event) {    //滚轮放大缩小
                var wheelDelta = event.wheelDelta ? event.wheelDelta : (event.deltalY * (-40));  // 获取当前鼠标的滚动情况
                if (wheelDelta > 0) {
                    if (_this.imgScale < 2) {
                        _this.imgScale = accMul(_this.imgScale, 1.1).toFixed(2) * 1
                        _this.form.resize = accMul(_this.imgScale, 100)
                    }
                } else {
                    if (_this.imgScale > 0.2) {
                        _this.imgScale = accMul(_this.imgScale, 0.9).toFixed(2) * 1
                        _this.form.resize = accMul(_this.imgScale, 100)
                    }
                }
                _this.imageSize.width = accMul(_this.extraImgList[0].width, _this.imgScale)
                _this.imageSize.height = accMul(_this.extraImgList[0].height, _this.imgScale)
                console.log(_this.imageSize.width, _this.imageSize.height, _this.imgScale)
                _this.drawImage(_this.imgObject);   //重新绘制图片
                event.preventDefault && event.preventDefault();
                return false;
            };
        },
        // 上传图片
        uploadImage(file, callback) {
            this.$message.loading({ content: '上传中，请稍后……', key: 'message', duration: 0 })
            const formData = new FormData()
            formData.append('file', file)
            this.$httpUpload(this.APIURL.ossUploadFile, formData).then((res) => {
                if (!res.success) {
                    this.$message.error({ content: res.message, key: 'message' })
                    return false
                }
                this.$message.success({ content: '上传完成！', key: 'message' })
                // console.log('res.data', res.data)
                callback(res.data)
            }).catch((err) => {
                // this.$message.error({ content: err.message, key: 'message' })
            })
        },
        // 上传我的水印
        uploadMyWaterRemark(e) {
            this.$message.loading({ content: '上传中，请稍后……', key: 'message', duration: 0 })
            const formData = new FormData()
            formData.append('file', e.file)
            this.$httpUpload(this.APIURL.ossUploadFile, formData).then((res) => {
                if (!res.success) {
                    this.$message.error({ content: res.message, key: 'message' })
                    return false
                }
                this.$message.success({ content: '上传完成！', key: 'message' })
                console.log('res.data', res.data)
                this.form.imgUrl = res.data
                // 获取默认位置 x y
                this.extraImgList = []
                // 重置放大缩小倍数
                this.imgScale = 1
                this.form.resize = 100
                // 重置位置
                this.form.defaultLocation = '1,1'
                this.imgX = 0
                this.imgY = 0
                this.getImageSize(this.form.imgUrl).then((res) => {
                    let defaultLocation = this.getDefaultLocation(res.width, res.height)
                    this.extraImgList.push({
                        url: this.form.imgUrl,
                        width: res.width,
                        height: res.height,
                        x: defaultLocation.x,
                        y: defaultLocation.y
                    })
                    this.imageSize = {
                        width: res.width,
                        height: res.height
                    }
                    console.log(this.extraImgList[0])
                    // 重新绘制画布
                    this.ctx.clearRect(0, 0, this.canvasWidth, this.canvasHeight);
                    this.loadImg();
                    this.canvasEventsInit();
                }).catch((err) => {
                    let defaultLocation = this.getDefaultLocation(err.width, err.height)
                    this.extraImgList.push({
                        url: this.form.imgUrl,
                        width: err.width,
                        height: err.height,
                        x: defaultLocation.x,
                        y: defaultLocation.y,
                    })
                    this.imageSize = {
                        width: err.width,
                        height: err.height
                    }
                    // 重新绘制画布
                    this.ctx.clearRect(0, 0, this.canvasWidth, this.canvasHeight);
                    this.loadImg();
                    this.canvasEventsInit();
                })
                this.$forceUpdate()
            }).catch((err) => {
                // this.$message.error({ content: err.message, key: 'message' })
            })
        },
        // 获取默认位置 x y
        getDefaultLocation(width, height) {
            let canvasWidth = this.canvasWidth
            let canvasHeight = this.canvasHeight
            let x = 0
            let y = 0
            let defaultLocation = this.form.defaultLocation.split(',')
            if (this.imgScale) {
                width = accMul(width, this.imgScale).toFixed(0) * 1
                height = accMul(height, this.imgScale).toFixed(0) * 1
            }
            // x轴
            if (defaultLocation[0] == '1') {
                x = 0   // 贴左边
            }
            else if (defaultLocation[0] == '3') {
                x = accDiv(accDiv(accSub(canvasWidth, width), 2), this.imgScale).toFixed(2) * 1   // 居中
            }
            else if (defaultLocation[0] == '5') {
                x = accDiv(accSub(canvasWidth, width), this.imgScale).toFixed(2) * 1  // 贴右边
            }
            // y轴
            if (defaultLocation[1] == '1') {
                y = 0   // 贴上边
            }
            else if (defaultLocation[1] == '3') {
                y = accDiv(accDiv(accSub(canvasHeight, height), 2), this.imgScale).toFixed(2) * 1    // 居中
            }
            else if (defaultLocation[1] == '5') {
                y = accDiv(accSub(canvasHeight, height), this.imgScale).toFixed(2) * 1  // 贴下边
            }

            console.log('默认位置', x, y, defaultLocation)
            let obj = {
                x,
                y
            }
            this.defaultLocation = obj
            return obj
        },
        getTextDefaultLocation() {
            let canvasWidth = this.canvasWidth
            let canvasHeight = this.canvasHeight
            let eleWidth = accDiv(canvasWidth, 6)
            let eleHeight = accDiv(canvasHeight, 6)
            let x = 0
            let y = 0
            let width = this.ctx.measureText(this.form.content).width // 文字度量 占据宽度

            let defaultLocation = this.form.defaultLocation.split(',')
            x = accSub(accMul(eleWidth, defaultLocation[0]), accDiv(width, 2)).toFixed(2) * 1
            y = accMul(eleHeight, defaultLocation[1]).toFixed(2) * 1

            // 限制范围
            if (x <= 0) {
                x = 0
            }
            if (x >= this.canvasWidth - width) {
                x = this.canvasWidth - width
            }
            if (y <= 0) {
                y = 0
            }
            if (y >= this.canvasHeight) {
                y = this.canvasHeight
            }
            console.log('默认位置', x, y, defaultLocation)
            let obj = {
                x,
                y
            }
            this.defaultLocation = obj
            return obj
        },
        // 获取图片的宽高
        getImageSize(url) {
            return new Promise((resolve, reject) => {
                var img = document.createElement("img");
                img.src = url;
                img.onload = () => {
                    resolve({ width: img.naturalWidth, height: img.naturalHeight });
                };
                img.onerror = () => {
                    reject({ width: undefined, height: undefined })
                }
            });
        },
        // 水印位置变化
        onLocationChange(value) {
            this.form.defaultLocation = value
            // 重置位置
            this.imgX = 0
            this.imgY = 0
            if (this.form.type == 1) {
                this.extraImgList.forEach((item) => {
                    let defaultLocation = this.getDefaultLocation(item.width, item.height)
                    item.x = defaultLocation.x
                    item.y = defaultLocation.y
                })
            }
            // 重新绘制画布
            this.ctx.clearRect(0, 0, this.canvasWidth, this.canvasHeight);
            this.loadImg();
            this.canvasEventsInit();
        },
        // 水印文字修改
        onTextChange() {
            this.loadImg()
            this.canvasEventsInit()
        },
        // 水印类型修改
        onTypeChange() {
            var _this = this
            // 清空画布提示
            if (this.form.content || this.form.imgUrl) {
                this.$info({
                    title: '提示',
                    content: '切换类型后，当前的水印将被清除，确定切换吗？',
                    onOk() {
                        // 清空画布
                        _this.form = Object.assign(_this.form, {
                            content: '',
                            imgUrl: '',
                            canvasSize: 1,
                            defaultLocation: '1,1',
                            fontFamily: 'Microsoft Yahei',
                            fontSize: 13,
                            color: '#000'
                        })

                        _this.extraImgList = [
                            {
                                url: '',
                                x: 0,
                                y: 0,
                                width: 0,
                                height: 0,
                            }
                        ]
                        _this.canvasWidth = 600
                        _this.canvasHeight = 600
                        _this.imgObject = []
                        _this.imgScale = 1
                        _this.imageSize = {}
                        _this.imgX = 0
                        _this.imgY = 0
                        _this.defaultLocation = {}
                        _this.ctx.clearRect(0, 0, _this.canvasWidth, _this.canvasHeight);
                    },
                })
            }

        },
        // 画布大小修改
        onCanvasSizeChange(e) {
            if (e == 1) {
                this.canvasWidth = 600
                this.canvasHeight = 600
            }
            else if (e == 2) {
                this.canvasWidth = 800
                this.canvasHeight = 800
            }
            this.loadImg()
            this.canvasEventsInit()
            if (this.form.type == 2) {
                setTimeout(() => {
                    this.drawImage()
                }, 100)
            }
        },
        // 修改图片大小
        onImageResizeChange() {
            this.imgScale = accMul(this.form.resize, 0.01).toFixed(2) * 1
            this.imageSize.width = accMul(this.extraImgList[0].width, this.imgScale)
            this.imageSize.height = accMul(this.extraImgList[0].height, this.imgScale)
            this.drawImage(this.imgObject)
        },
        // dataURL转file
        dataURLtoFile(dataUrl, fileName) {
            var arr = dataUrl.split(','), mime = arr[0].match(/:(.*?);/)[1],
                bstr = atob(arr[1]), n = bstr.length, u8arr = new Uint8Array(n);
            while (n--) {
                u8arr[n] = bstr.charCodeAt(n);
            }
            return new File([u8arr], fileName, { type: mime });
        },
        // 保存
        handleSubmit() {
            // 校验
            if (isNone(this.form.name)) {
                this.$message.info('请输入模板名称')
                return false
            }
            if (this.form.type == 1 && isNone(this.form.imgUrl)) {
                this.$message.info('请上传水印')
                return false
            }
            // 生成水印图片
            var _this = this;
            var canvas = _this.myCanvas;
            let image = canvas.toDataURL("image/jpg", 1.0)
            let file = this.dataURLtoFile(image, this.form.name + '.jpg')
            this.uploadImage(file, (res) => {
                console.log(res)
                let params = {
                    id: this.form.id,   // id
                    name: this.form.name,   // 模板名称
                    type: this.form.type,   // 水印类型
                    defaultLocation: this.form.defaultLocation, // 水印位置
                    canvasSize: this.form.canvasSize,   // 底图尺寸 1 600*600 2 800*800
                    content: this.form.content, // 水印内容
                    fontFamily: this.form.fontFamily,   // 字体
                    fontSize: this.form.fontSize,   // 字体大小
                    fontColor: this.form.color, // 字体颜色
                    url: this.extraImgList[0].url,  // 我的水印
                    imgScale: this.imgScale,    // 图片缩放比例
                    height: this.extraImgList[0].height,    // 图片高度
                    width: this.extraImgList[0].width,  // 图片宽度
                    imgX: this.imgX,    // x轴位移距离
                    imgY: this.imgY,    // y轴位移距离
                    defaultX: this.defaultLocation.x,    // 起始x轴偏离
                    defaultY: this.defaultLocation.y,    // 起始y轴偏离
                    newUrl: res,    // 生成水印图片地址
                }
                if (this.query.modalType == 'create') {
                    this.$httpPost(this.APIURL.addWaterMark, params).then((res) => {
                        if (!res.success) {
                            this.$message.error(res.message)
                            return false
                        }
                        this.$message.success('新增水印成功！')
                        setTimeout(() => {
                            this.$router.go(-1)
                        }, 200)
                    }).catch((err) => {
                    })
                }
                else if (this.query.modalType == 'edit') {
                    this.$httpPost(this.APIURL.editWaterMark, params).then((res) => {
                        if (!res.success) {
                            this.$message.error(res.message)
                            return false
                        }
                        this.$message.success('编辑水印成功！')
                        setTimeout(() => {
                            this.$router.go(-1)
                        }, 200)
                    })
                }
            })
        },
        // 取消
        handleCancel() {
            this.$router.go(-1)
        },
    },
}
</script>
<style lang="less" scoped>
.index {
    display: flex;
    flex-direction: row;
    justify-content: center;
    height: 100%;
    background-color: #f8f8f8;
    padding: 60px;
    box-sizing: border-box;

    .left {
        width: 400px;
        min-width: 400px;
        margin-right: 20px;

        .image {
            width: 100px;
            height: 100px;
            max-width: 100px;
            height: 100px;
            cursor: pointer;

            img {
                width: 100%;
                height: 100%;
            }

            .addImage {
                width: 100%;
                height: 100%;
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                border: 1px solid #e8e8e8;
            }
        }

        .locationTable {
            margin-top: 10px;

            td {
                border: 1px solid #E8E8E8;
                padding: 10px 14px;
                box-sizing: border-box;

                .ant-radio-wrapper {
                    margin: 0;
                }
            }
        }

        .btnGroup {
            margin-top: 40px;

            .btn {
                border-radius: 5px;
                padding: 0 20px;
            }
        }
    }

    .right {
        .canvasChange {
            position: absolute;
            top: 15px;
        }
    }
}

.input {
    width: 200px;
}

.canvas {
    background: url('../../assets/imgs/watermark-base-map.jpg') no-repeat 0 0;
    background-size: 100%;
}
</style>
```

**做的有点乱，再遇到了话重新做。**



加减乘除计算方法：

```js
// 计算方法
// 加
export function accAdd(arg1, arg2) {
  var r1, r2, m, c;
  try {
    r1 = arg1.toString().split(".")[1].length;
  } catch (e) {
    r1 = 0;
  }
  try {
    r2 = arg2.toString().split(".")[1].length;
  } catch (e) {
    r2 = 0;
  }
  c = Math.abs(r1 - r2);
  m = Math.pow(10, Math.max(r1, r2));
  if (c > 0) {
    var cm = Math.pow(10, c);
    if (r1 > r2) {
      arg1 = Number(arg1.toString().replace(".", ""));
      arg2 = Number(arg2.toString().replace(".", "")) * cm;
    } else {
      arg1 = Number(arg1.toString().replace(".", "")) * cm;
      arg2 = Number(arg2.toString().replace(".", ""));
    }
  } else {
    arg1 = Number(arg1.toString().replace(".", ""));
    arg2 = Number(arg2.toString().replace(".", ""));
  }
  return (arg1 + arg2) / m;
}
// 减
export function accSub(arg1, arg2) {
  var r1, r2, m, n;
  try {
    r1 = arg1.toString().split(".")[1].length;
  } catch (e) {
    r1 = 0;
  }
  try {
    r2 = arg2.toString().split(".")[1].length;
  } catch (e) {
    r2 = 0;
  }
  m = Math.pow(10, Math.max(r1, r2)); //last modify by deeka //动态控制精度长度
  n = r1 >= r2 ? r1 : r2;
  return Number(((arg1 * m - arg2 * m) / m).toFixed(n));
}
// 乘
export function accMul(arg1, arg2) {
  var m = 0,
    s1 = arg1.toString(),
    s2 = arg2.toString();
  try {
    m += s1.split(".")[1].length;
  } catch (e) {}
  try {
    m += s2.split(".")[1].length;
  } catch (e) {}
  return (
    (Number(s1.replace(".", "")) * Number(s2.replace(".", ""))) /
    Math.pow(10, m)
  );
}
// 除
export function accDiv(arg1, arg2) {
  var t1 = 0,
    t2 = 0,
    r1,
    r2;
  try {
    t1 = arg1.toString().split(".")[1].length;
  } catch (e) {}
  try {
    t2 = arg2.toString().split(".")[1].length;
  } catch (e) {}
  // with (Math) {
    r1 = Number(arg1.toString().replace(".", ""));
    r2 = Number(arg2.toString().replace(".", ""));
    return (r1 / r2) * Math.pow(10, t2 - t1);
  // }
}
```

#### 73.2 效果

![image-20221216164027237](https://gitee.com/v876774538/my-img/raw/master/image-20221216164027237.png)

![image-20221216164331640](https://gitee.com/v876774538/my-img/raw/master/image-20221216164331640.png)

### 74.js 判断多个请求加载完毕 Promise.all

#### 74.1 Promise.all()用法

Promise.all()方法用于将多个Promise实例包装成一个新的Promise实例。

```js
var p = Promise.all([p1,p2,p3]);
```

1. 只有p1、p2、p3的状态**都变成fulfilled，p的状态才会变成fulfilled**，此时p1、p2、p3的返回值组成一个数组，传递给p的[回调函数](https://so.csdn.net/so/search?q=回调函数&spm=1001.2101.3001.7020)。
2. 只要p1、p2、p3之中**有一个被rejected，p的状态就变成rejected**，此时第一个被reject的实例的返回值，会传递给p的回调函数。

```js
let p1 = new Promise((resolve, reject) => {
  resolve('成功了')
})

let p2 = new Promise((resolve, reject) => {
  resolve('success')
})

let p3 = Promise.reject('失败')

Promise.all([p1, p2]).then((result) => {
  console.log(result)               //['成功了', 'success']
}).catch((error) => {
  console.log(error)
})

Promise.all([p1,p3,p2]).then((result) => {
  console.log(result)
}).catch((error) => {
  console.log(error)      // 失败了，打出 '失败'
})
```

#### 74.2 实例

```js
// 获取图片的宽高
getImageSize(url) {
    return new Promise((resolve, reject) => {
        var img = document.createElement("img");
        img.src = url;
        img.onload = () => {
            resolve({ width: img.naturalWidth, height: img.naturalHeight });
        };
        img.onerror = () => {
            reject({ width: undefined, height: undefined })
        }
    });
},
```

```js
// 处理图片
let images = this.form.imagePath.split(',')
let imagesLoadAll = []
images.forEach((item, index) => {
    if (item) {
        imagesLoadAll[index] = this.getImageSize(item).then((res) => {
            this.form.productImageList.push({
                url: item,
                width: res.width,
                height: res.height,
            })
        }).catch((err) => {
            this.form.productImageList.push({
                url: item,
                width: err.width,
                height: err.height,
            })
        })
    }
})
Promise.all(imagesLoadAll).then((res) => {
    this.loading = false
    window.scrollTo(0, 0)
}).catch((err) => {
    setTimeout(() => {
        this.loading = false
        window.scrollTo(0, 0)
    }, 200)
})
```

![image-20221220144206750](https://gitee.com/v876774538/my-img/raw/master/image-20221220144206750.png)

### 75.uni-app 当前页面强制刷新

```js
var pages = getCurrentPages(); //获取所有页面的数组对象
var currPage = pages[pages.length - 1]; //当前页面
uni.redirectTo({
    url: currPage.__page__.fullPath
})
```

### 76.uni-app 全局过滤器

utils.js

```js
import Vue from 'vue'
Vue.filter("priceFilter",(num)=>{
	if(num.toString().indexOf('~')>0){
	    return  num
	}
	var result = [ ], counter = 0;
	num = (num || 0).toString().split('');
	for (var i = num.length - 1; i >= 0; i--) {
	    counter++;
	    result.unshift(num[i]);
	    if (!(counter % 3) && i != 0) { result.unshift(','); }
	}
	return result.join('')
})
```

### 77.uni-app 图片上传及压缩

1.utils.js

```js
function uploadImg(type, sourceType) {
	return new Promise((resolve, reject) => {
		return uni.chooseImage({
			count: 1,
			sizeType: ['compressed'],
			sourceType: sourceType == 'camera' ? ['camera'] : ['album', 'camera'],
			success: (res) => {
				// tempFilePath可以作为img标签的src属性显示图片
				const tempFilePaths = res.tempFilePaths.toString();
				const tempFilePaths1 = res.tempFilePaths;
				console.log(tempFilePaths1)
				// uni.showLoading();
				console.log(res)
				let resSize = res.tempFiles[0].size
				console.log('resSize', resSize)
				// 图片压缩
				if (resSize > 3145728) {
					uni.getImageInfo({
						src: tempFilePaths,
						success: (image) => {
							let canvasWidth = image.width //图片原始长宽
							let canvasHeight = image.height;
							let base = canvasWidth / canvasHeight;
							// 设置画布最大宽度
							if (canvasWidth > 1000) {
								canvasWidth = 1000;
								canvasHeight = Math.floor(canvasWidth / base);
							}
							let img = new Image();
							img.src = tempFilePaths; // 要压缩的图片

							let canvas = document.createElement('canvas');
							let ctx = canvas.getContext('2d');
							canvas.width = canvasWidth;
							canvas.height = canvasHeight;
							// 清除画布
							ctx.clearRect(0, 0, canvasWidth, canvasHeight);
							// 将图片画到canvas上面   使用Canvas压缩
							ctx.drawImage(img, 0, 0, canvasWidth, canvasHeight);
							// canvas.toDataURL 返回的是一串Base64编码的URL
							// 指定格式 PNG
							var base64 = canvas.toDataURL("image/png", 0.5);
							console.log('base64', base64)
							var blob = convertBase64ToBlob(base64)
							console.log('blob', blob)
							let obj = {
								img: '',
								blobImg: ''
							}
							obj.img = blobToFile(blob, '222.png')
							// obj.blobImg = base64
							obj.blobImg = tempFilePaths1[0]
							console.log(obj)
							// 限制图片大小 3M
							if (obj.img.size > 3145728) {
								showToast('上传图片过大，请重新选择')
								return false
							}
							else {
								resolve(obj)
							}
						}
					});
				} else {
					let obj = {
						img: '',
						blobImg: ''
					}
					obj.img = res.tempFiles[0]
					obj.blobImg = res.tempFilePaths[0]
					let resSize = res.tempFiles[0].size
					console.log(obj)
					resolve(obj)
				}

			},
			complete: (res) => {
				console.log(res)
			}
		})
	})
}
```

2.使用

```js
async submit(){
    let url = (await this.utils.uploadImg());
    uni.$emit('idFroPic', url)
    uni.navigateBack({
        delta: 1
    });
},
```

### 78.VsCode格式化配置

需要安装的插件：**ESLint + Premitter + Vetur + koroFileHeader**

<img src="https://upload-images.jianshu.io/upload_images/4067825-d7e54915ab14dc90.png?imageMogr2/auto-orient/strip|imageView2/2/w/592/format/webp" alt="img" style="zoom:50%;" />

```json
{
    // 代码文件头部注释
    "fileheader.customMade": {
        "Descripttion": "",
        "Version": "1.0",
        "Author": "pj",
        "Date": "Do not edit",
        "LastEditors": "pj",
        "LastEditTime": "Do not edit"
    },
    // 函数注释
    "fileheader.cursorMode": {
        "description": "",
        "param": "",
        "return": ""
    },
    "fileheader.configObj": {
        "createFileTime": true,
        "language": {
            "languagetest": {
                "head": "/$$",
                "middle": " $ @",
                "end": " $/",
                "functionSymbol": {
                    "head": "/** ",
                    "middle": " * @",
                    "end": " */"
                },
                "functionParams": "js"
            }
        },
        "autoAdd": true,
        "autoAddLine": 100,
        "autoAlready": true,
        "annotationStr": {
            "head": "/*",
            "middle": " * @",
            "end": " */",
            "use": false
        },
        "headInsertLine": {
            "php": 2,
            "sh": 2
        },
        "beforeAnnotation": {
            "文件后缀": "该文件后缀的头部注释之前添加某些内容"
        },
        "afterAnnotation": {
            "文件后缀": "该文件后缀的头部注释之后添加某些内容"
        },
        "specialOptions": {
            "特殊字段": "自定义比如LastEditTime/LastEditors"
        },
        "switch": {
            "newlineAddAnnotation": true
        },
        "supportAutoLanguage": [],
        "prohibitAutoAdd": ["json"],
        "folderBlacklist": ["node_modules", "文件夹禁止自动添加头部注释"],
        "prohibitItemAutoAdd": [
            "项目的全称, 整个项目禁止自动添加头部注释, 可以使用快捷键添加"
        ],
        "moveCursor": true,
        "dateFormat": "YYYY-MM-DD HH:mm:ss",
        "atSymbol": ["@", "@"],
        "atSymbolObj": {
            "文件后缀": ["头部注释@符号", "函数注释@符号"]
        },
        "colon": [": ", ": "],
        "colonObj": {
            "文件后缀": ["头部注释冒号", "函数注释冒号"]
        },
        "filePathColon": "路径分隔符替换",
        "showErrorMessage": false,
        "writeLog": false,
        "wideSame": false,
        "wideNum": 13,
        "functionWideNum": 0,
        "CheckFileChange": false,
        "createHeader": true,
        "useWorker": false,
        "designAddHead": false,
        "headDesignName": "random",
        "headDesign": false,
        "cursorModeInternalAll": {},
        "openFunctionParamsCheck": true,
        "functionParamsShape": ["{", "}"],
        "functionBlankSpaceAll": {},
        "functionTypeSymbol": "*",
        "typeParamOrder": "type param",
        "customHasHeadEnd": {},
        "throttleTime": 60000
    },

    // 代码格式化
    // vscode默认启用了根据文件类型自动设置tabsize的选项
    "editor.detectIndentation": false,
    // 重新设定tabsize
    "editor.tabSize": 4,
    "vetur.format.options.tabSize": 4,
    // #每次保存的时候自动格式化
    "editor.formatOnSave": true,

    // 添加 vue 支持
    "eslint.validate": ["javascript", "html", "vue"],
    //  去掉代码结尾的分号
    "prettier.semi": false,
    "prettier.tabWidth": 4,
    //  使用单引号替代双引号
    "prettier.singleQuote": true,

    //  让函数(名)和后面的括号之间加个空格
    "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
    //  这个按用户自身习惯选择
    "vetur.format.defaultFormatter.html": "js-beautify-html",
    // "vetur.format.defaultFormatter.html": "prettier",
    "vetur.format.defaultFormatterOptions": {
        // vue组件中html代码格式化样式
        "js-beautify-html": {
            // 对属性进行换行。
            // - auto: 仅在超出行长度时才对属性进行换行。
            // - force: 对除第一个属性外的其他每个属性进行换行。
            // - force-aligned: 对除第一个属性外的其他每个属性进行换行，并保持对齐。
            // - force-expand-multiline: 对每个属性进行换行。
            // - aligned-multiple: 当超出折行长度时，将属性进行垂直对齐。
            "wrap_attributes": "auto"
        },
        "prettier": {
            "semi": false,
            "singleQuote": true
        }
    },
    "vetur.validation.template": false,
    // 每次保存的时候将代码按eslint格式进行修复
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    "[javascript]": {
        "editor.defaultFormatter": "vscode.typescript-language-features"
    },
    // 代码是否按屏幕宽度换行
    "editor.wordWrap": "on",
    "[jsonc]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[vue]": {
        "editor.defaultFormatter": "octref.vetur"
    },
    "[html]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    }
}
```

参考：https://www.jianshu.com/p/48e009f85e13

### 79.通用邮箱正则

```js
let regEmail = /^[A-Za-z\d]+([-_\.][A-Za-z\d]+)*@([A-Za-z\d]+[-\.])+[A-Za-z\d]{2,4}(,[A-Za-z\d]+([-_\.][A-Za-z\d]+)*@([A-Za-z\d]+[-\.])+[A-Za-z\d]{2,4})*$/

if (!regEmail.test(this.formValidate.email)) {
    this.$Message.info('邮箱格式错误！')
    return false
}
```

适用于：

[samata.shasarestha@yahoo.com](mailto:samata.shrestha@yahoo.com)

samsaatamusic@hotmail.co.uk

samsaata@silkinnovation.com.np

79898989@qq.com

### 80.价格补0 小数点后保持有两位小数

```js
function priceFilter(num) {
	var f = parseFloat(num); // 解析一个字符串，返回一个浮点数；
	var s = f.toString(); // 把一个逻辑值转换为字符串，并返回结果；
	var rs = s.indexOf('.'); // 返回某个指定的字符串值在字符串中首次出现的位置；如果字符串值没有出现，返回-1；

	// 没有小数点时：
	if (rs < 0) {
		rs = s.length;
		s += '.';
	}
	while (s.length <= rs + 2) {
		s += '0';
	}

	return s
}

```

### 81.uniapp 滚动监听

```js
// 滚动监听
onPageScroll(e) {
    var _this = this
    var temptop;
    const query = uni.createSelectorQuery();
    query.select('.total').boundingClientRect();
    query.selectViewport().scrollOffset();
    // exec执行所有的请求。请求结果按请求次序构成数组，在callback的第一个参数中返回。
    query.exec(function(res){
        res[0].top       // 节点距离上边界的坐标
        res[1].scrollTop // 显示区域的竖直滚动位置
        temptop = res[0].top;
        if (temptop<='2') {
            _this.topfixed = true;  
        } else{
            _this.topfixed = false;  
        }  
    })
}
```

### 81.js原生请求及封装

#### 81.1 使用XMLHttpRequest

```js
//创建Xhr对象
var xhr = new XMLHttpRequest()
//调用open函数
xhr.open('GET','url地址')
//调用send函数
xhr.send()
//监听onreadystatechange事件
xhr.onreadystatechange = function() {
    if(xhr.readystate === 4 && xhr.status === 200) {
        console.log(xhr.responseText)
    }
}
```

```js
// post请求
 //创建xhr对象
 var xhr = new XMLHttpRequest()
 //调用open函数
 xhr.open('POST','url地址')
 //设置Content-Type属性
 xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
 //调用send函数
 const data = JSON.stringify({
     name:'123'
 })
 xhr.send(data)  
 //监听onreadystatechange事件
 xhr.onreadystatechange = function () {
     if(xhr.readyState === 4 && xhr.status === 200) {
         console.log(xhr.responseText);
     }
 }
```

#### 81.2 简单封装

```js
 function http(){
    var xhr = new XMLHttpRequest()
    var baseUrl =  '基本地址'
    return{
       request:(method,url,data,success,err)=>{
        xhr.open(method,baseUrl+url)
       
        if (method=='GET'){
            xhr.send()  
        } else {
            xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
            xhr.send(data) 
        }
        xhr.onreadystatechange = function () {
            if(xhr.readyState === 4 && xhr.status === 200) {
                console.log(xhr.responseText);
                success(xhr.responseText)
            }else{
                err()
            }
        }
       }
    }
 }
 //调用
 var myHttp = http()
 let data = {}
 myHttp.request('post','/form',data,function(res){

 },function(){

 })
```

#### 81.3 实践

`http.js`

```js
function http(){
    var xhr = new XMLHttpRequest()
    var baseUrl =  'http://sarlisi-vip.jp/api' // 基本地址
    return{
       request:(method,url,data,success,err)=>{
        xhr.open(method,baseUrl + url)
       
        if (method=='GET'){
            xhr.send()  
        } else {
            // xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
            xhr.setRequestHeader('Content-Type', 'application/json')
            xhr.send(JSON.stringify(data)) 
        }
        xhr.onreadystatechange = function () {
            if(xhr.readyState === 4 && xhr.status === 200) {
                console.log(xhr.responseText);
                success(xhr.responseText)
            }else{
                err()
            }
        }
       }
    }
 }
```

`supplyChain.html`中引入http.js

```html
<script src="./js/http.js"></script>
<script src="./js/supplyChain/supplyChain.js"></script>
```

`supplyChain.js`中使用

```js
var myHttp = http()
myHttp.request('post', '/tAfterSale/afterSaleMessage', params, function(res) {
    location.reload()	// 强制刷新
})
```

### 82.js原生幻灯片效果

#### 82.1效果

![image-20230713093754027](https://gitee.com/v876774538/my-img/raw/master/image-20230713093754027.png)

#### 82.2 html

```html
<div class="slideshow">
  <div class="slideshow-wrap"></div>
  <div class="slideshow-sliders"></div>
</div>
```

#### 82.3 js

```js
window.addEventListener("load", function() {
	// 图片组
    var imgs = [
        './images/index/image17-1.jpg',
        './images/index/image1.png',
        './images/index/image2.png',
    ]

    for (var i = 0; i < imgs.length; i++) {
        var img = new Image();
        img.src = imgs[i];
        img.className = 'slideshow-img'
        document.querySelector('.slideshow-wrap').appendChild(img);
    }    

    var currentImgIndex = 0;    // 当前显示的图片索引
    // 添加索引滑块
    for (var i = 0 ; i < imgs.length; i++) {
        var div = document.createElement('div');
        div.className = 'slideshow-slider';
        div.id = i
        document.querySelector('.slideshow-sliders').appendChild(div);
    }

    var imgElements = document.querySelector('.slideshow-wrap').querySelectorAll('.slideshow-img');
    var sliderElements = document.querySelector('.slideshow-sliders').querySelectorAll('.slideshow-slider')

    // 显示当前索引的图片 索引高亮
    function showCurrentImg() {
        for (var i = 0; i < imgElements.length; i++) {
            imgElements[i].classList.remove('show')
            sliderElements[i].classList.remove('active')
        }
        imgElements[currentImgIndex].classList.add('show')
        sliderElements[currentImgIndex].classList.add('active')
    }
    showCurrentImg();

    // 切换到下一张图片
    function showNextImg() {
        currentImgIndex = (currentImgIndex + 1) % imgs.length
        showCurrentImg();
    }

    // 点击滑块切换
    for(var i =0; i < sliderElements.length; i++) {
        sliderElements[i].addEventListener('click', (sliderElement) => {
            console.log('sliderElement',sliderElement)
            currentImgIndex = sliderElement.target.id
            showCurrentImg();
        })
    }

    var timer   // 定时器
    // 自动切换
    function autoplay() {
        timer = setInterval(() => {
            showNextImg()
        }, 5000)
    }

    // 停止自动切换
    function stopplay() {
        clearInterval(timer)
    }

    autoplay();

    // 鼠标悬浮停止自动切换
    var slideshowElement = document.querySelector('.slideshow')
    slideshowElement.addEventListener('mouseover', () => {
        console.log('mouseover')
        stopplay();
    })
    slideshowElement.addEventListener('mouseleave', () => {
        console.log('mouseleave')
        autoplay();
    })

})

```

#### 82.4 css

```css
.slideshow {
    .slideshow-wrap {
        width: 5.89rem;
        height: 8.33rem;
        overflow: hidden;
        position: relative;

        .slideshow-img {
            position: absolute;
            width: 100%;
            height: 100%;
            transition: opacity 1s;
            opacity: 0;
            cursor: pointer;
        }
        .show {
            opacity: 1;
        }
    }

    .slideshow-sliders {
        margin-top: 0.18rem;
        display: flex;

        .slideshow-slider {
            width: 0.28rem;
            height: 0.04rem;
            border-radius: 0.02rem;
            margin-right: 0.09rem;
            background: #DEDEDE;
            cursor: pointer;
        }

        .active {
            background: #3E9AC8;
        }
    }
}
```

### 83.js原生系列左右点击箭头查看更多

#### 83.1 效果

![image-20230713094418048](https://gitee.com/v876774538/my-img/raw/master/image-20230713094418048.png)

#### 83.2 html

```html
  <div class="panle4">
    <div class="top"></div>
    <div class="bottom"></div>
    <div class="box">
        <div class="title">
          News
        </div>
        <div class="des">
          <span>SANTIME</span>
          <span class="line">|</span>
          <span>for Beauty & Life</span>
        </div>
        <div class="arrow">
          <img class="image22 disabled" src="./images/index/image22-disabled.png" alt="">
          <img class="image22 image23" src="./images/index/image23.png" alt="">
        </div>
        <div class="wrap">
          <div class="content">
            <div class="img-box">
              <img class="img18" src="./images/index/image18.jpg" alt="">
              <div class="middle">
                <div class="time">
                  2022.05.21
                </div>
                <div class="more">
                  MORE
                </div>
              </div>
              <div class="bottom">
                「健康的な生活、美しさを保つ」は、SANTIME（三益友）が創業以来、一貫して掲げている目標です。
              </div>
            </div>
            <div class="img-box">
              <img class="img18" src="./images/index/image19.jpg" alt="">
              <div class="middle">
                <div class="time">
                  2022.05.21
                </div>
                <div class="more">
                  MORE
                </div>
              </div>
              <div class="bottom">
                「健康的な生活、美しさを保つ」は、SANTIME（三益友）が創業以来、一貫して掲げている目標です。
              </div>
            </div>
            <div class="img-box">
              <img class="img18" src="./images/index/image20.jpg" alt="">
              <div class="middle">
                <div class="time">
                  2022.05.21
                </div>
                <div class="more">
                  MORE
                </div>
              </div>
              <div class="bottom">
                「健康的な生活、美しさを保つ」は、SANTIME（三益友）が創業以来、一貫して掲げている目標です。
              </div>
            </div>
            <div class="img-box">
              <img class="img18" src="./images/index/image21.jpg" alt="">
              <div class="middle">
                <div class="time">
                  2022.05.21
                </div>
                <div class="more">
                  MORE
                </div>
              </div>
              <div class="bottom">
                「健康的な生活、美しさを保つ」は、SANTIME（三益友）が創業以来、一貫して掲げている目標です。
              </div>
            </div>
            <div class="img-box">
              <img class="img18" src="./images/index/image21.jpg" alt="">
              <div class="middle">
                <div class="time">
                  2022.05.21
                </div>
                <div class="more">
                  MORE
                </div>
              </div>
              <div class="bottom">
                「健康的な生活、美しさを保つ」は、SANTIME（三益友）が創業以来、一貫して掲げている目標です。
              </div>
            </div>
            <div class="img-box">
              <img class="img18" src="./images/index/image21.jpg" alt="">
              <div class="middle">
                <div class="time">
                  2022.05.21
                </div>
                <div class="more">
                  MORE
                </div>
              </div>
              <div class="bottom">
                「健康的な生活、美しさを保つ」は、SANTIME（三益友）が創業以来、一貫して掲げている目標です。
              </div>
            </div>
          </div>
        </div>
    </div>
  </div>
```

关键结构：

![image-20230713094651710](https://gitee.com/v876774538/my-img/raw/master/image-20230713094651710.png)

#### 83.3 js

```js
window.addEventListener("load", function() {
    // 资讯列表切换效果
    var panle4 = document.querySelector('.panle4')
    var wrap = panle4.querySelector('.wrap')
    var wrapWidth = wrap.offsetWidth
    var imgBoxs = wrap.querySelectorAll('.img-box')

    var lastImgBoxIndex = 4
    var imgBoxWidth = 375
    if (imgBoxs && imgBoxs.length != 0) {
        imgBoxWidth = imgBoxs[0].offsetWidth
        lastImgBoxIndex = parseInt(wrapWidth / imgBoxWidth) // 当前页最后一个imgBox的index
        var imgBoxsNum = lastImgBoxIndex // 一页可展示的imgBox的数量
        console.log('lastImgBoxIndex', lastImgBoxIndex)
    }
    // 切换按钮点击事件
    var arrows = panle4.querySelector('.arrow').querySelectorAll('.image22')
    if (arrows && arrows.length != 0) {
        var arrowLeft = arrows[0]
        var arrowRight = arrows[1]
        console.log(arrowLeft, arrowRight)
        arrowLeft.addEventListener('click', () => {
            leftTranslation();
        })
        arrowRight.addEventListener('click', () => {
            rightTranslation();
        })
    }
    var content = wrap.querySelector('.content')
    var translate = 0
    // 左移
    function leftTranslation() {
        if (lastImgBoxIndex > imgBoxsNum) {
            lastImgBoxIndex--
            translate = translate + (imgBoxWidth / 100 + 0.51)
            // 内容平移一个img-box + 盒子外边距的距离
            content.style.transform = "translateX(" + translate + "rem)";
        }
        arrowDisabled();
    }
    // 右移
    function rightTranslation() {
        if (imgBoxs && lastImgBoxIndex < imgBoxs.length) {
            lastImgBoxIndex++
            translate = translate - (imgBoxWidth / 100 + 0.51)
            // 内容平移一个img-box + 盒子外边距的距离
            content.style.transform = "translateX(" + translate + "rem)";
        }
        arrowDisabled();
    }
    // 箭头按钮判断（控制样式及是否可点击）
    function arrowDisabled() {
        if (lastImgBoxIndex <= imgBoxsNum) {
            arrowLeft.src = './images/index/image22-disabled.png'
            arrowLeft.classList.add('disabled')
        }
        else {
            arrowLeft.src = './images/index/image22.png'
            arrowLeft.classList.remove('disabled')
        }
        if (lastImgBoxIndex >= imgBoxs.length) {
            arrowRight.src = './images/index/image23-disabled.png'
            arrowRight.classList.add('disabled')
        }
        else {
            arrowRight.src = './images/index/image23.png'
            arrowRight.classList.remove('disabled')
        }
    }
})
```

#### 83.4 css

```css
.panle4 {
  position: relative;
  width: 100%;

  .top {
    width: 100%;
    height: 4.12rem;
    background-color: #F5F5F5;
  }

  .bottom {
    width: 100%;
    height: 4.11rem;
    background-color: #fff;
  }

  .box {
    position: absolute;
    right: 0;
    top: 1.09rem;

    .title {
      font-family: FuturaLT;
      font-weight: 300;
      color: #333;
      font-size: .8rem;
      // margin-bottom: .44rem;
    }
  
    .des {
      font-family: Mplus1;
      font-weight: 400;
      font-size: .18rem;
      color: #404040;
      margin-bottom: .05rem;
      display: flex;
      align-items: center;
      .line {
        color: #808080;
        margin: 0 .24rem;
      }
    }

    .arrow {
      display: flex;
      justify-content: flex-end;
      margin-bottom: .25rem;

      .image22 {
        width: .36rem;
        height: .36rem;
        cursor: pointer;
      }

      .image23 {
        margin-left: .31rem;
        margin-right: .67rem;
        cursor: pointer;
        
      }

      .disabled {
        cursor: default;
      }
    }

    .wrap {
      max-width: 16.6rem;
      overflow: hidden;
    }

    .content {
      display: flex;
      height: 4rem;
      transition: transform 0.2s ease 0s;

      .img-box {
        margin-left: .51rem;
        width: 3.75rem;
        .img18 {
          width: 3.75rem;
          height: 2.41rem;
        }

        .middle {
          display: flex;
          align-items: center;
          justify-content: space-between;
          margin-top: .34rem;
          margin-bottom: .23rem;
          font-family: FuturaLT;
          font-size: 0.3rem;
          font-weight: 300;
          color: #333333;

          .more {
            font-size: 0.18rem;
            text-align: center;
            line-height: .27rem;
            padding: 0 0.11rem;
            box-sizing: border-box;
            height: .27rem;
            border: .01rem solid #999;
          }
        }

        .bottom {
          font-size: .18rem;
          font-weight: 400;
          font-family: Mplus1;
        }

      }

      .img-box:first-child {
        margin-left: 0;
      }

      .img-box:hover {

        .more {
          border: .01rem solid #3E9AC8;
          color: #3E9AC8;
        }
      }
    }
  }
}
```

### 84.解决缺少h1标签或h1标签内容为空（但不想显示标签内容）的问题

#### 84.1 效果

![image-20230719095349256](https://gitee.com/v876774538/my-img/raw/master/image-20230719095349256.png)

#### 84.2 html

```html
<h1 class="h1 mega-title slideshow__title visually-hidden">Product</h1>
```

#### 84.3 css

隐藏内容。

```css
.visually-hidden {
    position: absolute !important;
    overflow: hidden;
    clip: rect(0 0 0 0);
    height: 1px;
    border: 0;
    width: 1px;
    margin: -1px;
    padding: 0
}
```

### 85.禁止a标签内容被拖动

```js
ondragstart="return false"
```

```html
<a href='{{block.settings.button_link}}' class="slideshow__link" target="_blank" ondragstart="return false">
	....
</a>
```

### 86.uni-app自定义支付键盘/数字键盘组件

#### 86.1 支付键盘、数字键盘、付款键盘、密码键盘

1. 插件地址

   https://ext.dcloud.net.cn/plugin?id=4524

2. 平台兼容性

   ![image-20230801114507690](https://gitee.com/v876774538/my-img/raw/master/image-20230801114507690.png)

3. 使用

   ```vue
   <cu-keyboard ref="cukeyboard" @change="change" @confirm="confirm" @hide="hide"></cu-keyboard>
   ```

   ```js
   this.$refs.cukeyboard.open();	// 调用键盘显示
   ```

4. 实例，**附带输入光标**

   ```vue
   <!-- 重量输入 -->
   <template>
   	<view class="index">
   		<uniHeader title="重量输入"></uniHeader>
   		<view class="main">
   			<view class="card">
   				<view class="title">
   					回收重量
   				</view>
   				<view class="weightInput" @tap="showKeyBoard()">
   					<view class="left">
   						<text class="number" v-if="weight">{{ weight }}</text>
   						<view class="line" v-if="isShow"></view>
   						<text class="placeholder" v-if="!weight && !isShow">0.00</text>
   					</view>
   					<view class="right">
   						<text>kg</text>
   					</view>
   				</view>
   			</view>
   		</view>
   		<cu-keyboard ref="cukeyboard" :number="weight" confirmText="确定" :confirmStyle="{ backgroundColor: '#1890FE' }"
   			@change="change" @confirm="confirm" @hide="hide"></cu-keyboard>
   	</view>
   </template>
   
   <script>
   	export default {
   		components: {},
   		data() {
   			return {
   				weight: undefined, // 重量
   				isShow: false, // 输入光标
   				orderNo: '',
   				userInfo: {}
   			};
   		},
   		onLoad(e) {
   			this.userInfo = Object.assign(uni.getStorageSync('userInfo'))
   			if (e.weight) {
   				this.weight = e.weight
   				this.orderNo = e.orderNo
   
   				console.log("this.orderNo: ", this.orderNo);
   			}
   		},
   		methods: {
   			// 支付键盘
   			showKeyBoard() {
   				this.isShow = true
   				this.$refs.cukeyboard.open()
   			},
   			change(e) {
   				console.log('keyboardChange', e)
   				this.weight = e
   			},
   			confirm(e) {
   				this.isShow = false
   				if (this.utils.isNone(e)) {
   					this.utils.showToast('请输入回收重量')
   					return false
   				}
   				console.log('keyboardConfirm', e)
   				this.weight = e
   				
   
   				if (this.userInfo.partnerType == 1) {
   					this.$http('post', this.APIURL.addRecOrder, {
   						partnerUserId: this.userInfo.id,
   						weight: this.weight,
   						orderNo: this.orderNo,
   					}, 'JSON').then(res => {
   						if (!res.success) {
   							this.utils.showToast(res.message)
   							return false
   						}
   						this.goPath('/pages/Home/recycle/reclaimCode?url=' + res.data.url + '&orderNo=' + res.data
   							.orderNo + '&weight=' + this.weight)
   					})
   				} else {
   					this.$http('post', this.APIURL.createOrder, {
   						weight: this.weight,
   						orderNo: this.orderNo,
   					}, 'JSON').then(res => {
   						if (!res.success) {
   							this.utils.showToast(res.message)
   							return false
   						}
   						this.goPath('/pages/Home/recycle/reclaimCode?url=' + res.data.url + '&orderNo=' + res.data
   							.orderNo + '&weight=' + this.weight)
   					})
   				}
   
   
   			},
   			hide() {
   				this.isShow = false
   				console.log('keyboardHide')
   			},
   			goPath(path) {
   				uni.navigateTo({
   					url: path
   				})
   			}
   		}
   	}
   </script>
   
   <style lang="less" scoped>
   	.index {
   		width: 100%;
   		min-height: 100%;
   		background: #F8F8F8;
   
   		.main {
   			padding: 40rpx 30rpx;
   			box-sizing: border-box;
   
   			.card {
   				width: 100%;
   				background: #fff;
   				border-radius: 30rpx;
   				padding: 30rpx 30rpx 20rpx;
   				box-sizing: border-box;
   
   				.title {
   					font-size: 36rpx;
   					font-weight: 500;
   					font-family: Source Han Sans CN;
   					color: #333;
   					margin-bottom: 20rpx;
   				}
   
   				.weightInput {
   					height: 127rpx;
   					line-height: 127rpx;
   					display: flex;
   					justify-content: space-between;
   					align-items: center;
   					font-size: 60rpx;
   					font-family: Source Han Sans CN;
   					font-weight: 500;
   					border-bottom: 1px solid #E5E7F3;
   
   					text {
   						color: #333;
   					}
   
   					.placeholder {
   						color: #C9C9C9;
   					}
   
   					.line {
   						display: inline-block;
   						width: 4rpx;
   						height: 30px;
   						border: 2rpx;
   						background-color: #0063E5;
   						animation: cursorImg 1s infinite steps(1, start);
   
   						@keyframes cursorImg {
   
   							0%,
   							100% {
   								opacity: 0;
   							}
   
   							50% {
   								opacity: 1;
   							}
   						}
   					}
   				}
   			}
   		}
   	}
   </style>
   ```

#### 86.2 仿微信充值金额输入组件(带键盘、展示)

1. 插件地址

   https://ext.dcloud.net.cn/plugin?id=3341

2. 平台兼容性

   H5 √

3. 使用

   ```vue
   <script>
   import fxAmountInput from '@/components/fx-amountInput/fx-amountInput.vue';
   export default {
       components: {
           fxAmountInput
       }
   }
   </script>
   ```

   ```vue
   <fx-amountInput></fx-amountInput>
   <fx-amountInput :currency="currency" :fontSize="fontSize" :confirmText="confirmText" :btnColor="btnColor" :placeholder="placeholder" :maxNumber="maxNumber" :isBold="isBold" :isFilter="isFilter" @change="change" @confirm="confirm"></fx-amountInput>
   ```

4. 实例

   ```vue
   <template>
   	<view class="index">
   		<view class="storeName">
   			{{ storeName }}
   		</view>
   		<view class="inputAmount">
   			<view class="title">
   				消费金额
   			</view>
   			<view class="input">
   				<fx-amountInput currency="￥" fontSize="30" confirmText="付款" placeholder="请输入消费金额" btnColor="#58BD6D" :isBold="true" :loading="loading" :isFilter="true" @change="keyboardChange" @confirm="keyboardConfirm"></fx-amountInput>
   			</view>
   		</view>
   		<view class="tip">
   			请您在付款前确认商户信息及付款金额，确保支付安全
   		</view>
   		<!-- 自定义迁移弹窗 -->
   		<custom v-if="customData" :customData="customData"></custom>
   	</view>
   </template>
   
   <script>
   	import custom from "./custom.vue";
   	import fxAmountInput from '@/components/fx-amountInput/fx-amountInput.vue';
   	export default {
   		components: {
   			custom,
   			fxAmountInput
   		},
   		data() {
   			return {
   				amount: '',	// 消费金额
   				storeName: '',	// 商户名称
   				
   				repeated: false, //防止重复提交
   				loading: false,	// 按钮加载中
   				customData: '',//自定义弹窗
   			}
   		},
   		onLoad() {
   			uni.hideKeyboard(); 
   			
   			uni.removeStorage({key: 'merchantId'})
   			uni.removeStorage({key: 'openId'})
   			uni.removeStorage({key: 'mobile'})
   			uni.removeStorage({key: 'token'})
   			var merchantId = this.getQueryString('state');
   			var jsCode = this.getQueryString('code');
   			
   			// uni.setStorageSync('merchantId', 5514)
   			// uni.setStorageSync('openId', 'oZlAL5oF8Vkc7syrdcPi3UTO-xKM')
   			// uni.setStorageSync('mobile', 15959180039)
   			
   			if (jsCode != undefined) {
   				this.wechatPay(jsCode);
   				uni.setStorageSync('merchantId', merchantId)
   				this.maintenance()
   			}
   			var auth_code = this.getQueryString('auth_code');
   			if (auth_code != undefined) {
   				this.Alipay(auth_code);
   				uni.setStorageSync('merchantId', merchantId)
   				this.maintenance()
   			}
   			this.getMerchantName()
   			
   		},
   		methods: {
   			maintenance() {
   				this.$http("post", this.$APIURL.maintenance, {
   					merchantId: uni.getStorageSync('merchantId'),
   				}).then((res) => {
   					if (res.code !== this.config.SUCCESS) {
   						this.utils.showToast(res.message);
   						return false;
   					}
   					this.customData = res.data
   				});
   			},
   			// 获取商户名称
   			getMerchantName() {
   				this.$http('post', this.$APIURL.getMerchantName, {
   					merchantId: uni.getStorageSync('merchantId'),
   				}).then((res) => {
   					if (res.code !== this.config.SUCCESS) {
   						this.utils.showToast(res.message);
   						return false;
   					}
   					this.storeName = res.data
   				})
   			},
   			wechatPay(code) {
   				this.$http('post', this.$APIURL.auth, {
   					code: code
   				}).then(res => {
   					if (res.code !== this.config.SUCCESS) {
   						// this.utils.showToast(res.message);
   						return false;
   					}
   					uni.setStorageSync('openId', res.data.openId)
   				})
   			},
   			Alipay(code) {
   				this.$http('post', this.$APIURL.aliAuth, {
   					code: code
   				}).then(res => {
   					if (res.code !== this.config.SUCCESS) {
   						// this.utils.showToast(res.message);
   						return false;
   					}
   					uni.setStorageSync('auth_code', res.data.openId)
   				})
   			},
   			getQueryString(key) {
   				var after = window.location.search;
   				// if (after.indexOf('?') === -1) return null; //如果url中没有传参直接返回空
   				//key存在先通过search取值如果取不到就通过hash来取
   				after = after.substr(1) || window.location.hash.split("?")[1];
   
   				if (after) {
   					var reg = new RegExp("(^|&)" + key + "=([^&]*)(&|$)");
   					var r = after.match(reg);
   					console.log(r)
   					if (r != null) {
   						return decodeURIComponent(r[2]);
   					} else {
   						return null;
   					}
   				}
   			},
   			// 收款码下单
   			createPC() {
   				if (this.repeated) {
   					return false;
   				}
   				if (this.amount == '') {
   					this.utils.showToast("请正确填写充值金额");
   					return false;
   				}
   			
   				this.repeated = true;
   				this.loading = true;
   				uni.showLoading()
   				var openId, businessCode;
   				if (uni.getStorageSync('openId') != undefined && uni.getStorageSync('openId') != null && uni
   					.getStorageSync('openId') != '') {
   					openId = uni.getStorageSync('openId')
   					businessCode = '1'
   				} else if (uni.getStorageSync('auth_code') != undefined && uni.getStorageSync('auth_code') != null && uni
   					.getStorageSync('auth_code') != '') {
   					openId = uni.getStorageSync('auth_code')
   					businessCode = '2'
   				}
   				this.$http('POST', this.$APIURL.createPC, {
   					addAmount: this.amount,
   					merchantId: uni.getStorageSync('merchantId'),
   					openId: openId,
   					payType: businessCode
   				}).then(res => {
   					this.repeated = false;
   					if (res.code !== this.config.SUCCESS) {
   						this.utils.showToast(res.message);
   						this.loading = false;
   						uni.hideLoading()
   						return false;
   					}
   					this.paying(res.data)
   				})
   			},
   			// 支付
   			paying(data) {
   				this.repeated = true;
   				this.$http('POST', this.$APIURL.gaspaying, {
   					orderNo: data.orderNo,
   				}).then(res => {
   					uni.hideLoading()
   					this.repeated = false;
   					if (res.code !== this.config.SUCCESS) {
   						this.utils.showToast(res.message);
   						this.loading = false;
   						return false;
   					}
   					if (uni.getStorageSync('openId') != undefined && uni.getStorageSync('openId') != null && uni
   						.getStorageSync('openId') != '') {
   						// 触发微信支付
   						this.onBridgeReady(data)
   					}
   					if (uni.getStorageSync('auth_code') != undefined && uni.getStorageSync('auth_code') != null &&
   						uni.getStorageSync('auth_code') != '') {
   						// 触发支付宝支付
   						this.onAlipayReady(data)
   					}
   				})
   			},
   			// 微信支付
   			onBridgeReady(data) {
   				var that = this
   				WeixinJSBridge.invoke('getBrandWCPayRequest', {
   						"appId": data.spAppId, //公众号ID，由商户传入    
   						"timeStamp": data.spTimestamp, //自1970年以来的秒数    
   						"nonceStr": data.spNonceStr, //随机串    
   						"package": data.spPackages,
   						"signType": data.spSignType, //微信签名方式：    
   						"paySign": data.spPaySign //微信签名
   					},
   					function(res) {
   						if (res.err_msg == "get_brand_wcpay_request:ok") {
   							// 使用以上方式判断前端返回,微信团队郑重提示：
   							//res.err_msg将在用户支付成功后返回ok，但并不保证它绝对可靠。
   							that.utils.showToast("充值成功")
   							this.amount = ''
   						} else {
   							that.cancel(data.orderNo)
   							that.utils.showToast("支付失败!")
   						}
   						this.loading = false
   					});
   			},
   			// 支付宝支付
   			onAlipayReady(data) {
   				var that = this
   				AlipayJSBridge.call("tradePay", {
   					tradeNO: data.spPackages // 必传，此使用方式下该字段必传
   				}, function(result) {
   					if (result.resultCode == '9000') {
   						that.utils.showToast("充值成功")
   						this.amount = ''
   					} else {
   						that.cancel(data.orderNo)
   						that.utils.showToast("支付失败!")
   					}
   					this.loading = false;
   				});
   			},
   			// 支付键盘
   			keyboardChange(e) {
   				console.log('keyboardChange', e)
   				this.amount = e
   			},
   			keyboardConfirm(e) {
   				console.log('keyboardConfirm', e)
   				this.createPC()	// 收款码下单
   			},
   		}
   	}
   </script>
    
   <style lang="less" scoped>
   	.index {
   		width: 100%;
   		height: 100%;
   		position: fixed;
   		top: 0;
   		left: 0;
   		background: #F0EFF5;
   		// padding: 140rpx 32rpx 0;
   		padding: 32rpx;
   		box-sizing: border-box;
   	}
   	
   	.storeName {
   		color: #7CB3E8;
   		font-size: 30rpx;
   		font-weight: bold;
   		margin-bottom: 20rpx;
   	}
   	
   	.inputAmount {
   		width: 100%;
   		padding: 30rpx 16rpx;
   		box-sizing: border-box;
   		background-color: #fff;
   		margin-bottom: 20rpx;
   		.title {
   			font-size: 34rpx;
   			font-weight: normal;
   			margin-bottom: 20rpx;
   		}
   		.input {
   			display: flex;
   			align-items: center;
   			text {
   				font-size: 60rpx;
   				font-weight: bold;
   			}
   			input {
   				font-size: 60rpx;
   				font-weight: bold;
   			}
   		}
   	}
   	
   	.tip {
   		font-size: 28rpx;
   		color: #888;
   	}
   </style>
   
   ```

   组件代码：

   ```vue
   <template>
   	<view class="keyboard-main" :style="{height:height+'px',lineHeight:height+'px'}">
   		<text :style="{fontSize:parseInt(fontSize)+'px',fontWeight:isBold?'bold':'initial'}">{{currency}}</text>
   		<view class="keyboard-content" :style="{height:height+'px'}">
   			<view class="placeholder" :style="{fontSize:parseInt((fontSize/3*2))+'px',height:height+'px', paddingLeft: '5px'}" v-if="!money">
   				{{placeholder}}
   			</view>
   			<view class="input" :class="{zIndex:isShow}" :style="{fontSize:size+'px',height:height+'px', fontWeight:isBold?'bold':'initial'}" @click.stop="show">
   				<span id="text">
   					<block v-if="isFilter">
   						{{filterMoney(money)}}
   					</block>
   					<block v-if="!isFilter">
   						{{money}}
   					</block>
   					<view class="line" :style="{height:parseInt(height)+'px','background':btnColor}" v-show="isShow"></view>
   				</span>
   			</view>
   		</view>
   		<view class="mask" @click.stop="hide" v-if="isShow"></view>
   		<view class='keyboard' :class="{noPadding:!isShow}">
   		    <view class='key-row' v-if="isShow">
   		        <view class='key-cell' @click.stop='_handleKeyPress(1)'>1</view>
   		        <view class='key-cell' @click.stop='_handleKeyPress(2)'>2</view>
   		        <view class='key-cell' @click.stop='_handleKeyPress(3)'>3</view>
   				<view class='key-cell last-child' @click.stop="_handleKeyPress('delete')">
   					<image class="icon" src="../../static/fx-amountInput/backspace.png" mode="aspectFill"></image>
   				</view>
   		    </view>
   		    <view class='key-row' v-if="isShow">
   		        <view class='key-cell' @click.stop='_handleKeyPress(4)'>4</view>
   		        <view class='key-cell' @click.stop='_handleKeyPress(5)'>5</view>
   		        <view class='key-cell' @click.stop='_handleKeyPress(6)'>6</view>
   		        <view class='key-cell last-child'></view>
   		    </view>
   		    <view class='key-row' v-if="isShow">
   		        <view class='key-cell' @click.stop='_handleKeyPress(7)'>7</view>
   		        <view class='key-cell' @click.stop='_handleKeyPress(8)'>8</view>
   		        <view class='key-cell' @click.stop='_handleKeyPress(9)'>9</view>
   		        <view class='key-cell last-child'></view>
   		    </view>
   			<view class="key-zero-and-point" v-if="isShow">
   				<view class="a zero" @click.stop='_handleKeyPress(0)'>0</view>
   				<view class="a point" @click.stop="_handleKeyPress('.')">.</view>
   				 <view class='a last-child'></view>
   			</view>
   		    <button class='key-confirm' :class="{big:isShow,frist:fristShow}" :style="{'background': loading ? '#8a8a8d' : btnColor}" :disabled="loading" @click.stop="_handleKeyPress('confirm')">
   				{{confirmText}}
   			</button>
   		</view>
   		<view id="input-text" :style="{fontSize:(size+5)+'px',fontWeight:isBold?'bold':'initial'}">
   			{{filterMoney(money)}}
   		</view>
   	</view>
   </template>
   
   <script>
   	export default{
   		name:"keyBoard",
   		props:{
   			confirmText:{
   				default:'充值',
   				type:String
   			},
   			btnColor:{
   				default:'#2B76EF',
   				type:String
   			},
   			placeholder:{
   				default:'请输入充值金额',
   				type:String
   			},
   			currency :{
   				default:'￥',
   				type:String
   			},
   			maxNumber:{
   				default:100000000000,
   				type:Number
   			},
   			fontSize:{
   				type:[String,Number],
   				default:30
   			},
   			isBold:{
   				type:Boolean,
   				default:true
   			},
   			isFilter:{
   				type:Boolean,
   				default:true
   			},
   			loading: {
   				type: Boolean,
   				default: false,
   			}
   		},
   		data(){
   			return {
   				fristShow:true,
   				isShow:false,
   				size:0,
   				height:0,
   				allWidth:0,
   				money:''
   			}
   		},
   		created() {
   			this.height = this.fontSize;
   			this.size = this.fontSize;
   			var query = uni.createSelectorQuery().in(this)
   			setTimeout(()=>{
   				this.show()
   				query.select('.keyboard-content').boundingClientRect(data => {
   				  this.allWidth = data.width
   				}).exec();
   			},200)
   		},
   		watch:{
   			money(val){
   				this.$emit('change',parseFloat(val));
   			}
   		},
   		methods : {
   			show(){
   				this.isShow = true;
   			},
   			hide(){
   				// this.fristShow = false
   				this.isShow = false;
   			},
   			filterMoney(value){
   				if(!value){
   				    return ''
   				}else {
   				    value=value.replace(/\$\s?|(,*)/g, '')
   				    return value.replace(/\B(?=(\d{3})+(?!\d))/g, ',')
   				}
   			},
   			//处理按键
   			_handleKeyPress(num) {
   				if (num == -1) return false;
   				switch (String(num)) {
   					//小数点
   					case '.':
   						this._handleDecimalPoint();
   						break;
   					//删除键
   					case 'delete':
   						this._handleDeleteKey();
   						break;
   					//确认键
   					case 'confirm':
   						this._handleConfirmKey();
   						break;
   					default:
   						this._handleNumberKey(num);
   						break;
   				}
   			},
   			//处理小数点函数
   			_handleDecimalPoint() {
   				//如果包含小数点，直接返回
   				if (this.money.indexOf('.') > -1) return false;
   				//如果小数点是第一位，补0
   				if (!this.money.length)
   					this.money = '0.';
   				//如果不是，添加一个小数点
   				else
   					this.money = this.money + '.';
   				var query = uni.createSelectorQuery().in(this)
   				query.select('#text').boundingClientRect(data => {
   					var _w = data.width;
   					if(_w+Number(this.size)>this.allWidth){
   						this.size -=5
   					}
   				}).exec();
   			},
   			//处理删除键
   			_handleDeleteKey() {
   				let S = this.money;
   				//如果没有输入，直接返回
   				if (!S.length) return false;
   				//否则删除最后一个
   				this.money = S.substring(0, S.length - 1);
   				var query = uni.createSelectorQuery().in(this)
   				query.select('#input-text').boundingClientRect(data => {
   					var _w = data.width;
   					if(_w+20<this.allWidth && this.size<this.height){
   						this.size +=5
   					}
   				}).exec();
   			},
   			//处理数字
   			_handleNumberKey(num) {
   				if(Number(this.money+num)>this.maxNumber){
   					return
   				}
   				let S = this.money;
   				//如果有小数点且小数点位数不小于2
   				if ( S.indexOf('.') > -1 && S.substring(S.indexOf('.') + 1).length < 2)
   					this.money = S + num;
   				if (S.indexOf('.') > -1 && S.substring(S.indexOf('.') + 1).length >= 2)
   					return
   				//没有小数点
   				if (!(S.indexOf('.') > -1)) {
   					//如果第一位是0，只能输入小数点
   					if (num == 0 && S.length == 0)
   						this.money = '0.';
   					else {
   						if (S.length && Number(S.charAt(0)) === 0) return;
   						this.money = S + num;
   					}
   				}
   				var query = uni.createSelectorQuery().in(this)
   				query.select('#text').boundingClientRect(data => {
   					var _w = data.width;
   					if(_w+Number(this.size)>this.allWidth){
   						this.size -=5
   					}
   				}).exec();
   			},
   			
   			//提交
   			_handleConfirmKey() {	
   				let S = this.money;
   				//未输入
   				if (!S.length||S==0){
   					uni.showToast({
   						title: this.placeholder,
   						icon:'none',
   						duration: 1000
   					});
   					return false;
   				}
   				//将 8. 这种转换成 8.00
   				if (S.indexOf('.') > -1 && S.indexOf('.') == (S.length - 1))
   					S = Number(S.substring(0, S.length - 1)).toFixed(2);
   				//保留两位
   				S = Number(S).toFixed(2);
   				this.$emit('confirm',parseFloat(S));    //提交参数
   			}
   		}
   	}
   </script>
   
   <style lang="less" scoped>
   	.keyboard-main{
   		width: 100%;
   		display: flex;
   		justify-content: flex-start;
   		align-items: flex-end;
   		padding: 20rpx 0;
   		box-sizing: initial;
   		color: #1B1B1B;
   		text{
   			font-size: 24px;
   			margin-right: 5px;
   		}
   	}
   	.keyboard-content{
   		width: 100%;
   		height: 30px;
   		position: relative;
   		.placeholder{
   			position: absolute;
   			top: 0;
   			left: 0;
   			width: 100%;
   			color:#c0c4cc;
   			display: flex;
   			justify-content: flex-start;
   			align-items: flex-end;
   		}
   		.input{
   			position: absolute;
   			top: 0;
   			left: 0;
   			width: 100%;
   			display: flex;
   			justify-content: flex-start;
   			align-items: flex-end;
   			font-size: 30px;
   			font-weight: bold;
   			&.zIndex{
   				z-index: 999;
   			}
   			#text{
   				display: flex;
   				justify-content: flex-start;
   				align-items: flex-end;
   			}
   			.line{
   				display: inline-block;
   				width: 4rpx;
   				height: 30px;
   				border: 2rpx;
   				background-color: #0063E5;
   				margin-left: 8rpx;
   				animation:cursorImg 1s infinite steps(1, start);
   				@keyframes cursorImg {
   					0%, 100% {
   						opacity: 0;
   					}
   					50% {
   						opacity: 1;
   					}
   				}
   			}
   		}
   	}
   	.mask{
   		position: fixed;
   		top: 0;
   		left: 0;
   		right: 0;
   		bottom: 0;
   		z-index: 1;
   	}
       .keyboard {
   		flex: 1;
           position: fixed;
           bottom: 0;
           left: 0;
           width: 100%;
   		background-color: #F5F5F5;
   		padding: 20rpx;
   		transition: all 0.6s;
   		z-index: 9;
   		box-sizing: border-box;
   		&.noPadding{
   			padding: 0;
   			bottom: -100%;
   		}
       }
       .keyboard .key-row {
           display: flex;
   		justify-content: space-between;
           display: -webkit-flex;
           position: relative;
   		box-sizing: border-box;
       }
    
       .keyboard .key-cell {
   		font-size: 20px;
   		width: 160rpx;
   		height: 80rpx;
   		/* margin-right: 20rpx; */
   		margin-bottom: 20rpx;
   		background-color: #fff;
   		border-radius: 8rpx;
   		display: flex;
   		justify-content: center;
   		align-items: center;
   		&.last-child{
   			/* margin-right: 0px; */
   			width: 170rpx;
   		}
   		.icon{
   			width: 50rpx;
   			height: 40rpx;
   		}
       }
     
       .keyboard .key-confirm {
           position: fixed;
           text-align: center;
           /* min-height: 100rpx; */
           width: 170rpx;
   		padding: 20rpx 30rpx;
   		border-radius: 8rpx;
   		box-sizing: border-box;
   		color: #FFFFFF;
           z-index: 10;
           right: 20rpx;
   		top: calc(100vh - 300rpx);
           bottom: 200rpx;
   		display:flex;
   		justify-content: center;
   		align-items: center;
   		font-size: 20px;
   		letter-spacing: 4px;
   		font-weight: bold;
   		transition: all 0.3s;
   		border: 0;
   		&.big{
   			right: 20rpx;
   			bottom: 20rpx;
   			padding: 0 30rpx;
   			bottom: 20rpx;
   		}
   		&.frist{
   			position:absolute;
   			top: auto;
   			right: 20rpx;
   			height: 280rpx;
   			bottom: 20rpx;
   		}
       }
   	.key-zero-and-point{
   		display: flex;
   		height: 80rpx;
   		justify-content: space-between;
   		align-items: center;
   		font-size: 20px;
   		.zero{
   			display: flex;
   			justify-content: center;
   			align-items: center;
   			width: 340rpx;
   			text-align: center;
   			background-color: #fff;
   			border-radius: 8rpx;
   			height: 100%;
   		}
   		.point{
   			display: flex;
   			justify-content: center;
   			align-items: center;
   			background-color: #fff;
   			border-radius: 8rpx;
   			width: 160rpx;
   			height: 100%;
   		}
   		.last-child{
   			background-color: #fff;
   			border-radius: 8rpx;
   			width: 170rpx;
   			height: 100%;
   		}
   	}
   	.key-cell:active{
   		color: white;  
   		background: black;  //黑色
   		opacity: 0.1;    //这里重要，就是通过这个透明度来设置
   	}
   	.a:active,.key-confirm2:active{
   		color: white;
   		background: black;  //黑色
   		opacity: 0.1;    //这里重要，就是通过这个透明度来设置
   	}
   	#input-text{
   		width: max-content;
   		position: fixed;
   		bottom: -200%;
   	}
   </style>
   
   ```

   ### 87.uni-app自定义选项卡 tab栏

   ![image-20230823141037098](https://gitee.com/v876774538/my-img/raw/master/image-20230823141037098.png)

   ```html
   <scroll-view class="tabBar" :scroll-x="true" :scroll-with-animation="true">
       <view class="tab" v-for="(item, index) in tabsList" :key="index" :class="index == selectIndex ? 'tabActive' : ''" @tap="handleTabChange(index)"><text>{{ item.label }}</text></view>
   </scroll-view>
   ```

   ```js
   tabsList: [
       {
           label: '分类1'
       },
       {
           label: '分类1'
       },
       {
           label: '分类1'
       },
       {
           label: '分类1'
       },
       {
           label: '分类1'
       },
   ],	// 分类
   selectIndex: 0,
   ```

   ```css
   .tabBar {
       width: 100%;
       max-width: 100%;
       height: 70rpx;
       line-height: 70rpx;
       white-space: nowrap;
       position: relative;
   
       .tab {
           display: inline-block;
           width: 25%;
           height: 70rpx;
           text-align: center;
           padding: 0 9rpx;
           box-sizing: border-box;
   
           font-size: 28rpx;
           font-weight: 500;
           font-family: Source Han Sans SC-Medium, Source Han Sans CN;
           color: #333;
       }
       .tabActive {
           color: #1890FF;
           position: relative;
   
           text::after {
               content: '';
               display: block;
               width: 50%;
               height: 3px;
               background: #1890FF;
               position: absolute;
               bottom: 0;
               left: 50%;
               margin-left: -25%;
               border-radius: 3px;
           }
       }
   }
   ```

   ### 87.uniapp 排序tab栏 升降序

   #### 87.1 效果展示

   ![image-20230901115540463](https://gitee.com/v876774538/my-img/raw/master/image-20230901115540463.png)

   #### 87.2 代码实现

   ![image-20230901115510846](https://gitee.com/v876774538/my-img/raw/master/image-20230901115510846.png)

   ```html
   <view class="sorts" v-else>
       <view class="sort" v-for="(item, index) in sortTypeList" :key="index" @tap="handleSortTypeChange(item, index)" :class="item.checked ? 'sortActive' : ''">
           {{ item.name }}
           <view class="arrowBox" v-if="Object.keys(item.valMap).length > 1">
               <image class="arrow" :src="fileImgPath('/static2/home/transhipment/common.png')" mode="" v-if="!item.checked"></image>
               <image class="arrow" :src="fileImgPath('/static2/home/transhipment/asc.png')" mode="" v-else-if="item.checked && item.selectVal == 0"></image>
               <image class="arrow" :src="fileImgPath('/static2/home/transhipment/desc.png')" mode="" v-else-if="item.checked && item.selectVal == 1"></image>
           </view>
       </view>
   </view>
   ```

   ```css
   .sort {
       display: flex;
       align-items: center;
       margin-right: 30rpx;
       font-size: 28rpx;
       color: #C4C4C4;
   
       .arrowBox {
           display: flex;
           align-items: center;
   
           .arrow {
               display: flex;
               flex-direction: column;
               justify-content: center;
               width: 18rpx;
               height: 32rpx;
               margin-left: 20rpx;
           }
       }
   }
   
   .sortActive {
       color: #1890FF;
       font-weight: 500;
   }
   ```

   ```js
   sortTypeList: [
       {
           name:'默认',
           checked:true,
           valMap: {
               0: '',
           },
           selectVal: 0
       },
       {
           name:'销量',
           checked:false,
           valMap: {
               0: 1,
               1: 2
           },
           selectVal: 0,
       },
       {
           name:'米币',
           checked:false,
           valMap: {
               0: 3,
               1: 4
           },
           selectVal: 0
       },
       {
           name:'最新上架',
           checked:false,
           valMap: {
               0: 5,
           },
           selectVal: 0
       },
   ],//排序 1-销量高到低 2-销量低到高 3-米币高到低 4-米币低到高 5-最新上架
   ```

   ```js
   handleSortTypeChange(item, index) {
       if (Object.keys(item.valMap).length > 1 && item.checked) {
           item.selectVal = item.selectVal == 0 ? item.selectVal = 1 : item.selectVal = 0;	// 排序升降序切换
       }
       this.sortTypeList2.forEach((itemm, indexx) => {
           itemm.checked = false
       })
       item.checked = true
       // 获取对应值
       this.sortType = item.valMap[item.selectVal]
       // 获取列表
       this.loadStatus = "loading";
       this.pagination.pageNo = 1;
       this.list = [];
       this.hmGiftInfoPage()
   },
   ```

### 87.APP应用更新（应用外更新、热更新）

> 小云秘书项目：http://syy333.dynv6.net:20080/xshb/xshbAPP.git

`config.js`存放版本名、更新地址等全局变量

```js
const version_name = '1.0.3'  // 版本名
const downUrl = ''	// 更新地址
const isUpdate = false	// 需要更新
const isForce = false	// 强制更新
const isShow = true	// 是否展示
```

`utils.js`

```js
// 检查更新
function checkUpdate(context) {
	// 判断环境
	let platform = uni.getSystemInfoSync().platform
	console.log('platform', platform)
	let type = 1
	if (platform == 'android') {
		type = 2 // android
	} else if (platform == 'ios') {
		type = 3 // ios
	} else {
		type = 1 // h5
	}

	// 更新 Android/IOS
	if (type == 2 || type == 3) {
		getUpdate(context, type, (data) => {
			config.isShow = data.isShow // 控制显示隐藏

			// 需要（应用外）更新
			if (config.isUpdate) {
				uni.showModal({
					title: '版本更新',
					content: '发现新版本，是否下载？',
					confirmColor: config.theme,
					showCancel: !config.isForce,
					success: function(res) {
						if (res.confirm) {
							plus.runtime.openURL(config.downUrl);
						} else if (res.cancel) {
							console.log('用户点击取消');
						}
					}
				});
			} else {
				// 判断是否需要（应用内）热更新
				getUpdate(context, 1, () => {
					if (config.isUpdate) {
						context.$refs.updateApp.open()	// 打开热更新弹窗
					}
				})
			}
		})
	}
	// 更新 h5
	else {
		getUpdate(context, type, (data) => {
			config.isShow = data.isShow // 控制显示隐藏
			
			if (config.isUpdate) {
				context.$refs.updateApp.open()	// 打开热更新弹窗
			}
		})
	}
}

function getUpdate(context, type, callback) {
	context.$http('get', context.APIURL.getUpdate, {
		version: config.version_name,
		type: type
	}).then((res) => {
		console.log('getUpdate', type, res)
		if (!res.success) {
			context.utils.showToast(res.message);
			return false;
		}
		config.isUpdate = res.data.isUpdate	// 是否更新
		config.downUrl = res.data.url	// 下载地址
		config.isForce = res.data.isForce // 控制强制更新

		callback(res.data)
	})
}

export default {
	checkUpdate,
}
```

`updateApp.vue`自定义热更新弹窗组件

```vue
<template>
	<view>
		<uni-popup ref="updateApp" class="updateApp" type="center" :mask-click="false">
		<view class="updatetips-whole" v-if="isShow">
			<view class="updatetips">
				<image class="close" src="@/static/close.png" @tap="close()" v-if="!config.isForce"></image>
				<!-- <image :src="fileImgPath('/static/updateIcon.png')" class="updateIcon" mode="widthFix"></image> -->
				<view>
					<view class="updatetips-head">
						<view class="updatetips-version" :style="`color: ${getTheme}`">
							版本更新
						</view>
						<view class="des">
							当前APP版本较低，访问该页面需要更新
						</view>
					</view>
					<view class="updatetips-content" v-if="versionContent">{{versionContent}}</view>
					<!-- 进度条 -->
					<progress v-if="isProgress" :percent="progress" :activeColor="getTheme" stroke-width="3" style="margin-top: 40rpx;"/>
				</view>
				<view class="updatetips-btn-disable" v-if="isProgress">立即更新</view>
				<view class="updatetips-btn" v-else @click="downloadBtn()" :style="`background: ${getTheme}`">立即更新</view>
			</view>
		</view>
		</uni-popup>
	</view>
</template>

<script>
	export default {
		props:['show','versionNum','versionContent','downloadUrl'],
		data() {
			return {
				progress:0,
				isProgress:false,
				isShow: false,
			};
		},
		computed:{
			getTheme() {
				return this.$store.getters.getTheme
			},
		},
		mounted() {
		},
		methods: {
			open(){
				this.isShow = true
				this.$refs.updateApp.open('center')
			},
			close() {
				this.isShow = false
				this.$refs.updateApp.close()
			},
			downloadBtn(){
				// if(uni.getSystemInfoSync().platform == 'android'){
					this.isProgress = true
					const downloadTask = uni.downloadFile({
						url: this.config.downUrl,
						success: (res) => {
							//安装
							plus.runtime.install(
								res.tempFilePath, {
									force: true
								},
								function(_res) {
									plus.runtime.restart();
								},(e)=>{
									plus.nativeUI.alert('资源更新失败,原因:' + e.message)
								}
							)
						},
						fail: (err)=> {
							// uni.$u.toast('下载失败')
							this.utils.showToast('下载失败')
						}
					})
					// 查看下载进度
					downloadTask.onProgressUpdate((res) => {
						this.progress = res.progress
					})
				// }
				// if(uni.getSystemInfoSync().platform == 'ios'){
				// 	plus.runtime.openURL(this.config.downUrl)
				// }			
			}
		}
	};
</script>

<style lang="less" scoped>
	.updateApp{
		/deep/.uni-popup__wrapper{
			width: 100%;
		}
	}
	.updatetips-whole{
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100%;
	}
	.updatetips{
		width: 80%;
		background: #fff;
		border-radius: 20rpx;
		padding: 40rpx 0;
		box-sizing: border-box;
		position: relative;
		.close {
			width: 40rpx;
			height: 40rpx;
			position: absolute;
			top: 10rpx;
			right: 10rpx;
		}
	}
	.updatetips-version{
		text-align: center;
		color: #1890FF;
		font-size: 48rpx;
		margin-bottom: 20rpx;
	}
	.des{
		width: 100%;
		text-align: center;
		font-size: 28rpx;
		font-family: Source Han Sans SC-Medium, Source Han Sans SC;
		font-weight: 500;
		color: #333333;
	}
	.updatetips-content{
		width: 80%;
		// min-height: 144rpx;
		margin: 40rpx auto 0;
	}
	.updatetips-btn-disable {
		height: 120rpx;
		line-height: 120rpx;
		text-align: center;
		color: #E6E6E6;
	}
	.updatetips-btn {
		width: 401rpx;
		height: 90rpx;
		line-height: 90rpx;
		background: #1890FF;
		color: #fff;
		box-shadow: 0px 3rpx 6rpx 1px rgba(0,0,0,0.16);
		border-radius: 45rpx;
		text-align: center;
		margin: 60rpx auto 0;
	}
	
</style>
```

`index.vue`调用检查更新

```vue
<template>
	<view class="login">
		...
		<!-- 更新 -->
		<update-app ref="updateApp"></update-app>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				...
			}
		},
		onLoad() {
			...
		},
		onShow() {
			this.utils.getOrgConfig(this)	// 获取app配置信息
            ...
		},
		methods: {
			...
		}
	}
</script>

<style lang="less" scoped>
    ...
</style>
```

### 88.uni-app 支付密码输入弹窗/验证码输入页面

> 杉通宝公众号项目：http://syy333.dynv6.net:20080/syy/shantongbao-exchange.git

#### 88.1 支付密码输入弹窗

1. 效果

   ![image-20231011153934146](https://gitee.com/v876774538/my-img/raw/master/image-20231011153934146.png)

2. 组件

   `payPassword.vue`

   ```vue
   <template>
   	<uni-popup ref="popup" class="popup" :mask-click="false">
   		<view class="content">
   			<view class="title">
   				<text>请输入支付密码</text>
   				<image src="@/static/close1.png" mode="" @tap="close()"></image>
   			</view>
   			<view class="des">
   				{{ tip }}
   			</view>
   			<view class="price">
   				￥<text class="em">{{ utils.priceFilter(price) }}</text>
   			</view>
   			<view class="code">
   				<input type="number" v-model="form.code" :maxlength="maxLength" @input="onInput" @blur="onBlur"
   					@focus="onFocus" :focus="isFocus" @confirm="handleSubmit()">
   				<view class="numbers">
   					<view class="number" v-for="(item, index) in codeArr">
   						<text v-if="item && isShow">{{ item }}</text>
   						<text v-else-if="item && !isShow" class="dot"></text>
   						<view class="focusLine" v-if="isFocus && currentIndex + 1 == index"></view>
   					</view>
   				</view>
   			</view>
   		</view>
   	</uni-popup>
   </template>
   
   <script>
   	export default {
   		name: "payPassword",
   		props: {
   			price: {
   				type: [String, Number],
   				default: 0
   			},
   			tip: {
   				type: String,
   				default: '提现'
   			}
   		},
   		data() {
   			return {
   				form: {},
   				codeArr: ['', '', '', '', '', ''],
   				maxLength: 6,
   				currentIndex: -1,
   				isFocus: true, // 默认进入时获取输入焦点
   				isShow: false, // 控制显示数字或隐藏
   			};
   		},
   		methods: {
   			open() {
   				this.handleClear()
   				this.$refs.popup.open('center')
   			},
   			close() {
   				this.$refs.popup.close()
   			},
   			onInput(e) {
   				var value = e.detail.value;
   				if (value.length <= this.maxLength) {
   					var valueArr = value.split('');
   					this.currentIndex = valueArr.length - 1
   					for (var i = 0; i < this.maxLength; i++) {
   						this.codeArr[i] = valueArr[i]
   					}
   				}
   			},
   			onBlur() {
   				this.isFocus = false
   			},
   			onFocus() {
   				this.isFocus = true
   			},
   			handleClear() {
   				this.form.code = ''
   				this.codeArr = ['', '', '', '', '', '']
   				this.currentIndex = -1
   				this.isFocus = false
   				setTimeout(() => {
   					this.isFocus = true
   				}, 500)
   				this.$forceUpdate()
   			},
   			handleSubmit() {
   				if (this.form.code.length < this.maxLength) {
   					this.utils.showToast(`请输入${this.maxLength}位支付密码`)
   					return false
   				}
   				this.$emit('onConfirm', this.form.code)
   			}
   		}
   	}
   </script>
   
   <style lang="less" scoped>
   	.content {
   		width: 690rpx;
   		background: #fff;
   		border-radius: 20rpx;
   		padding: 30rpx 30rpx 105rpx;
   		box-sizing: border-box;
   		text-align: center;
   		font-family: Source Han Sans CN-Medium, Source Han Sans CN;
   		font-weight: 500;
   		color: #333333;
   		
   		.title {
   			font-size: 36rpx;
   			margin-bottom: 40rpx;
   			position: relative;
   			
   			image {
   				width: 30rpx;
   				height: 30rpx;
   				position: absolute;
   				top: 10rpx;
   				right: 0;
   			}
   		}
   		
   		.des {
   			font-size: 28rpx;
   			margin-bottom: 10rpx;
   		}
   		
   		.price {
   			font-size: 37rpx;
   			display: flex;
   			justify-content: center;
   			align-items: center;
   			
   			.em {
   				font-size: 64rpx;
   				margin-left: 10rpx;
   			}
   		}
   	}
   	
   	.code {
   		position: relative;
   		margin-top: 40rpx;
   
   		input {
   			position: relative;
   			z-index: 2;
   			width: 100%;
   			height: 86rpx;
   			color: transparent;
   		}
   
   		.numbers {
   			position: absolute;
   			top: 0;
   			width: 100%;
   			z-index: 1;
   			display: flex;
   			justify-content: space-between;
   			align-items: center;
   
   			.number {
   				position: relative;
   				width: 86rpx;
   				height: 86rpx;
   				line-height: 86rpx;
   				text-align: center;
   				border-radius: 16rpx;
   				background: #f6f6f6;
   				font-size: 60rpx;
   				font-family: Source Han Sans CN-Regular, Source Han Sans CN;
   				font-weight: 400;
   				color: #333333;
   				display: flex;
   				justify-content: center;
   				align-items: center;
   
   				.dot {
   					display: inline-block;
   					width: 24rpx;
   					height: 24rpx;
   					border-radius: 50%;
   					background: #333;
   				}
   
   				.focusLine {
   					position: absolute;
   					left: 0;
   					top: 25%;
   					width: 1px;
   					height: 50%;
   					background: #000;
   					opacity: 1;
   					-webkit-animation: sharkLight 1s linear infinite;
   					animation: sharkLight 1s linear infinite;
   				}
   
   				@-webkit-keyframes sharkLight {
   					from {
   						-webkit-transform: scale(1);
   						opacity: 1;
   					}
   
   					to {
   						-webkit-transform: scale(0.9);
   						opacity: 0;
   					}
   				}
   			}
   		}
   	}
   </style>
   ```

3. 使用

   ![image-20231011154221021](https://gitee.com/v876774538/my-img/raw/master/image-20231011154221021.png)

   `withdraw.vue`

   ```vue
   <template>
   	<view class="index">
   		<goBack title="提现" backgroundColor="#fff"></goBack>
   		<view class="main">
   			<view class="card card-account" @tap="utils.goPath('/pages/merchant/my/changeAccount')">
   				<view class="left">
   					<image src="@/static/my/alipay.png" mode=""></image>
   					<view class="center">
   						<text>{{ utils.hideName(merchantInfo.name)}}</text>
   						<text>{{ utils.hideTel(merchantInfo.alipayAccount) }}</text>
   					</view>
   				</view>
   				<view class="right">
   					<text v-if="merchantInfo.alipayAccount">更换账号</text>
   					<text v-else>设置提现账号</text>
   					<image src="@/static/arrow-right.png" mode=""></image>
   				</view>
   			</view>
   			<view class="card card-withdraw">
   				<view class="title">
   					提现金额
   				</view>
   				<view class="number">
   					<text>￥</text>
   					<input type="number" v-model="money" placeholder="请输入转出金额" placeholder-class="placeholder">
   				</view>
   				<view class="bottom">
   					<text>可提现的余额： ¥{{ utils.priceFilter(merchantInfo.balance ? merchantInfo.balance : 0) }}</text>
   					<button @tap="getAll">全部提现</button>
   				</view>
   			</view>
   			<view class="btnGroup">
   				<button class="btn" @tap="handleConfirm()">确认提现</button>
   			</view>
   		</view>
   		<pay-password ref="payPasswordPopup" :price="money" @onConfirm="handleSubmit"></pay-password>
   	</view>
   </template>
   
   <script>
   	import payPassword from '@/components/payPassword.vue'
   	export default {
   		components: {
   			payPassword
   		},
   		data() {
   			return {
   				merchantInfo: {},
   				money: '',
   			};
   		},
   		onShow() {
   			this.getMerchantInfo()
   		},
   		methods: {
   			getAll() {
   				this.money = this.merchantInfo.balance
   				this.$forceUpdate()
   			},
   			getMerchantInfo() {
   				this.$http('get',this.APIURL.getMerchantInfo).then(res=>{
   					this.merchantInfo = res.data
   				})
   			},
   			handleConfirm() {
   				console.log(this.money)
   				if (this.utils.isNone(this.merchantInfo.alipayAccount)) {
   					this.utils.showToast('请先设置提现账号')
   					return false
   				}
   				if (this.utils.isNone(this.money) && this.money != 0) {
   					this.utils.showToast('请输入提现金额')
   					return false
   				}
   				if (Number(this.money) > Number(this.merchantInfo.balance)) {
   					this.utils.showToast('提现金额不能超过余额')
   					return false
   				}
   				if (Number(this.money) <= 0) {
   				// if (Number(this.money) < 0) {
   					this.utils.showToast('提现金额有误，请重新输入')
   					return false
   				}
   				if(this.merchantInfo.isSetPayPwd == 2) {
   					var that = this
   					uni.showModal({
   						title: '提示',
   						content: '该账号未设置支付密码，请设置密码后再提现',
   						cancelText: '取消',
   						confirmText: '设置',
   						success: (ress) => {
   							if (ress.confirm) {
   								that.utils.goPath('/pages/merchant/my/setPayPassword/verification', { type: 'set' })
   							}
   						},
   					})
   					return false
   				}
   				
   				this.$refs.payPasswordPopup.open()
   			},
   			handleSubmit(payPwd) {
   				var that = this
   				console.log('支付密码', payPwd)
   				this.$refs.payPasswordPopup.close()
   				this.$http('post',this.APIURL.withdraw,{
   					money: this.money,
   					payPwd: payPwd,
   				},'JSON').then(res=>{
   					// 支付密码错误
   					if (!res.success) {
   						uni.showModal({
   							title: res.message,
   							content: '请重试',
   							cancelText: '忘记密码',
   							confirmText: '重试',
   							success: (ress) => {
   								if (ress.confirm) {
   									// 重试
   									that.$refs.payPasswordPopup.open()
   								}
   								else if (ress.cancel) {
   									// 忘记密码
   									that.utils.goPath('/pages/merchant/my/setPayPassword/verification', { type: 'forget' })
   								}
   							},
   						})
   						return false
   					}
   					
   					// 支付密码正确
   					this.utils.showToast('提现成功')
   					setTimeout(()=>{
   						this.utils.reLaunch('/pages/merchant/tabBar/my')
   					},800)
   					
   				})
   	
   			}
   		}
   	}
   </script>
   
   <style lang="less">
   	.index {
   		.main {
   			padding: 20rpx 30rpx;
   			box-sizing: border-box;
   
   			.card {
   				background: #fff;
   				border-radius: 20rpx;
   			}
   
   			.card-account {
   				display: flex;
   				justify-content: space-between;
   				align-items: center;
   				padding: 20rpx 30rpx;
   				box-sizing: border-box;
   
   				.left {
   					display: flex;
   					align-items: center;
   					font-size: 28rpx;
   					font-family: Source Han Sans CN-Medium, Source Han Sans CN;
   					font-weight: 500;
   					color: #333333;
   
   					image {
   						width: 92rpx;
   						min-width: 92rpx;
   						height: 92rpx;
   						margin-right: 20rpx;
   					}
   
   					.center {
   						display: flex;
   						flex-direction: column;
   
   						text:first-child {
   							margin-bottom: 17rpx;
   						}
   
   						text:last-child {
   							font-size: 24rpx;
   							color: #B9B8BE;
   						}
   					}
   				}
   
   				.right {
   					font-size: 28rpx;
   					font-family: Source Han Sans CN-Medium, Source Han Sans CN;
   					font-weight: 500;
   					color: #333333;
   
   					image {
   						width: 25rpx;
   						height: 25rpx;
   						margin-left: 10rpx;
   					}
   				}
   			}
   		
   			.card-withdraw {
   				margin-top: 20rpx;
   				padding: 30rpx;
   				box-sizing: border-box;
   				
   				.title {
   					font-size: 36rpx;
   					font-family: Source Han Sans CN-Medium, Source Han Sans CN;
   					font-weight: 500;
   					color: #333333;
   					margin-bottom: 40rpx;
   				}
   				
   				.number {
   					position: relative;
   					font-size: 60rpx;
   					font-family: Source Han Sans CN-Medium, Source Han Sans CN;
   					font-weight: 500;
   					color: #333333;
   					border-bottom: 1px solid #E7E7E7;
   					padding-bottom: 20rpx;
   					margin-bottom: 20rpx;
   					
   					input {
   						width: 100%;
   						line-height: 87rpx;
   						padding-left: 74rpx;
   						font-size: 60rpx;
   						font-family: Source Han Sans CN-Medium, Source Han Sans CN;
   						font-weight: 500;
   						color: #333333;
   					}
   					
   					.placeholder {
   						color: #CCCCCC;
   					}
   					
   					text {
   						position: absolute;
   						line-height: 87rpx;
   					}
   				}
   			
   				.bottom {
   					height: 40rpx;
   					line-height: 40rpx;
   					font-size: 28rpx;
   					font-family: Source Han Sans CN-Regular, Source Han Sans CN;
   					font-weight: 400;
   					color: #999999;
   					display: flex;
   					justify-content: space-between;
   					align-items: center;
   					
   					button {
   						background: transparent;
   						border: none;
   						width: fit-content;
   						font-size: 28rpx;
   						font-family: Source Han Sans CN-Regular, Source Han Sans CN;
   						font-weight: 400;
   						color: #3E9AFD;
   					}
   				}
   			}
   		
   			.btnGroup {
   				position: fixed;
   				bottom: 178rpx;
   				left: 0;
   				width: 100%;
   				
   				.btn {
   					width: 610rpx;
   					height: 90rpx;
   					line-height: 90rpx;
   					background: #3E9AFD;
   					border-radius: 45rpx;
   					margin: 0 auto;
   					font-size: 28rpx;
   					font-family: Source Han Sans CN-Medium, Source Han Sans CN;
   					font-weight: 500;
   					color: #FFFFFF;
   				}
   			}
   		}
   	}
   </style>
   ```

#### 88.2 验证码输入页面

> 流程：获取验证码前需要先通过图形验证码校验，点击“获取验证码”按钮，调用获取验证码接口，通过后直接跳转到验证码输入页面。

1. 图形验证码弹窗

   ![image-20231011154402206](https://gitee.com/v876774538/my-img/raw/master/image-20231011154402206.png)

   组件`graphic-verification.vue`

   ```vue
   <!-- 图形验证码弹窗 -->
   <template>
   	<view class="popup" v-if="isShow">
   		<view class="content">
   			<image class="close" src="@/static/close.png" @tap="handleCancel()"></image>
   			<view class="title">请先按图形输入正确字符</view>
   			<view class="code" @tap="handleReset()">
   				<image :src="'data:image/png;base64,'+imgUrl" mode=""></image>
   				<view class="tip">
   					看不清？点击刷新
   				</view>
   			</view>
   			<input type="text" placeholder="请输入图形验证码" placeholder-style="color: #E6E6E6;" v-model="dataForm.pictureCode" class="input">
   			<view class="btnGroup">
   				<button class="btn" @tap="handleSubmit()">获取验证码</button>
   			</view>
   		</view>
   	</view>
   </template>
   
   <script>
   	export default {
   		name:"graphic-verification",
   		data() {
   			return {
   				imgUrl: '',	// 图形验证码图片
   				dataForm: {
   					pictureId: '',	// 验证码id
   					pictureCode: '',	// 输入图形验证码
   				},
   				isShow: false,
   			};
   		},
   		methods: {
   			open(){
   				this.isShow = true
   				this.handleReset()
   			},
   			close(){
   				this.isShow = false
   			},
   			// 获取图形验证码
   			getGraphicCode() {
   				console.log('获取图形验证码')
   				let api = uni.getStorageSync('userType') == 'client' ? this.APIURL.userGetImgCode : this.APIURL.merchantGetImgCode
   				this.$http('post', api).then((res) => {
   					if (!res.success) {
   						this.utils.showToast(res.message);
   						return false;
   					}
   					this.imgUrl = res.data.image
   					this.dataForm.pictureId = res.data.imageId
   				})
   			},
   			// 刷新
   			handleReset() {
   				this.dataForm = {
   					pictureId: '',	// 验证码id
   					pictureCode: '',	// 输入图形验证码
   				}
   				this.getGraphicCode()
   			},
   			// 提交
   			handleSubmit() {
   				if (this.utils.isNone(this.dataForm.pictureCode)) {
   					this.utils.showToast('请输入图形验证码')
   					return false
   				}
   				this.$emit('ok', this.dataForm)
   			},
   			// 取消
   			handleCancel() {
   				this.$emit('cancel')
   			}
   		}
   	}
   </script>
   
   <style lang="less" scoped>
   .popup {
       	width: 100%;
       	height: 100%;
       	background: rgba(0, 0, 0, 0.3);
       	position: fixed;
       	width: 100%;
       	height: 100%;
       	top: 0;
       	left: 0;
       	right: 0;
       	bottom: 0;
       	z-index: 999;
   		
   		.content {
   			width: 686rpx;
   			background: #ffffff;
   			border-radius: 20rpx;
   			padding: 32rpx;
   			box-sizing: border-box;
   			margin: 300rpx auto 0;
   			display: flex;
   			flex-direction: column;
   			align-items: center;
   			position: relative;
   			
   			.close {
   				width: 40rpx;
   				height: 40rpx;
   				position: absolute;
   				top: 10rpx;
   				right: 10rpx;
   			}
   			
   			.title {
   				text-align: center;
   				font-size: 32rpx;
   				font-weight: 500;
   			}
   			
   			.code {
   				width: 100%;
   				display: flex;
   				flex-direction: column;
   				align-items: center;
   				margin-top: 20rpx;
   				.tip {
   					font-size: 26rpx;
   					color: #333;
   					margin-top: 20rpx;
   				}
   				
   				image {
   					width: 300rpx;
   					height: 100rpx;
   					// background-color: red;
   					border: 1px solid #E6E6E6;
   				}
   				
   			}
   			
   			.input {
   				width: 100%;
   				height: 80rpx;
   				line-height: 80rpx;
   				text-align: center;
   				font-size: 28rpx;
   				background: #F6F6F8;
   				margin-top: 20rpx;
   				border-radius: 40rpx;
   			}
   			
   			.btnGroup {
   				width: 100%;
   				display: flex;
   				align-items: center;
   				margin-top: 20rpx;
   				
   				.btn {
   					flex: 1;
   					width: 100%;
   					height: 80rpx;
   					line-height: 80rpx;
   					font-size: 32rpx;
   					font-weight: 500;
   					font-family: Source Han Sans SC;
   					margin-right: 20rpx;
   					background: #E6E6E6;
   					border-radius: 40rpx;
   				}
   				.btn:last-child {
   					color: #333;
   					margin-right: 0;
   				}
   				.btn:first-child {
   					background: #3E9AFD;
   					color: #fff;
   				}
   			}
   		}
       }
   </style>
   ```

   使用`login.vue`

   ```vue
   <template>
   	<view class="index">
   		<goBack></goBack>
   		<view class="main">
   			<view class="title">
   				<text>手机号登录</text>
   				<view class="register" v-if="userType == 'merchant'" @tap="utils.goPath('/pages/public/login/register')">
   					注册
   				</view>
   			</view>
   			<view class="form">
   				<view class="input">
   					<input type="text" class="phone" v-model="form.phone" placeholder="请输入您的手机号"
   						placeholder-style="color: #ccc">
   					<image src="../../../static/clear.png" class="clearIcon" v-if="!disabled" @tap="form.phone = ''">
   					</image>
   				</view>
   			</view>
   			<view class="btnGroup">
   				<button class="btn" :disabled="disabled" :class="disabled ? 'btn-disabled' : ''"
   					@tap="getCode()">获取验证码</button>
   				<!-- <button class="btn btn-transparent" @tap="utils.goPath('/pages/public/login/loginByPassword')">密码登录</button> -->
   			</view>
   		</view>
   		<!-- 图形验证码弹窗 -->
   		<graphicVerification ref="graphicVerification" @cancel="handleCancel()" @ok="handleSubmit"></graphicVerification>
   	</view>
   </template>
   
   <script>
   	import graphicVerification from '@/components/graphic-verification.vue'
   	export default {
   		components: {
   			graphicVerification
   		},
   		data() {
   			return {
   				form: {}, // 表单
   				userType: 'client',	// 用户端(client):18533330014 商家端(merchant):18533330015
   				codeTouch: false,	// 防连点
   			}
   		},
   		computed: {
   			disabled() {
   				return this.form.phone ? false : true
   			}
   		},
   		onLoad(options) {
   			uni.removeStorage({
   				key: 'token'
   			});
   			uni.removeStorage({
   				key: 'userInfo'
   			});
   			uni.removeStorage({
   				key: 'merchantInfo'
   			});
   			// 返回页面时刷新
   			window.addEventListener('pageshow', function(e) {
   			    // 通过persisted属性判断是否存在 BF Cache
   			    if (e.persisted) {  // persisted判断是否后退进入
   			        location.reload();
   			    }
   			});
   			
   			// 判断商家端/用户端
   			if (options && options.userType) {
   				console.log('options', options.userType)
   				this.userType = options.userType
   				uni.setStorageSync('userType', this.userType)
   			}
   			else if (uni.getStorageSync('userType')) {
   				this.userType = uni.getStorageSync('userType')
   			}
   			else {
   				this.userType = 'client'
   				uni.setStorageSync('userType', this.userType)
   			}
   		},
   		methods: {
   			// 获取验证码
   			getCode() {
   				// 校验手机号
   				let regPhone = /^1[3456789]\d{9}$/;
   				if (this.utils.isNone(this.form.phone)) {
   					this.utils.showToast('请输入手机号码')
   					return false
   				} else if (!regPhone.test(this.form.phone)) {
   					this.utils.showToast('手机号码格式有误')
   					return false;
   				}
   				// 获取图形验证码
   				this.$refs.graphicVerification.open()
   			},
   			// 图形验证码取消
   			handleCancel() {
   				this.$refs.graphicVerification.close()
   			},
   			// 图形验证码确认
   			handleSubmit(dataForm) {
   				Object.assign(this.form, dataForm)
   				console.log(this.form)
   				this.getCode2()
   			},
   			// 获取验证码
   			getCode2() {
   				let api = uni.getStorageSync('userType') == 'client' ? this.APIURL.userGetCodeNoToken : this.APIURL
   					.merchantGetCodeNoToken
   				if (this.codeTouch) {
   					return false
   				}
   				this.codeTouch = true
   				uni.showLoading()
   				this.$http('post', api, {
   					phone: this.form.phone,
   					type: 2, // 登录
   					pictureId: this.form.pictureId,
   					pictureCode: this.form.pictureCode
   				}).then((res) => {
   					setTimeout(() => {
   						this.codeTouch = false
   						uni.hideLoading()
   					}, 500)
   					if (!res.success) {
   						this.utils.showToast(res.message)
   						if (res.code == 10110010) {
   							// 账号不存在
   							this.$refs.graphicVerification.close()
   						}
   						else if (res.code == -1) {
   							// 图片验证码错误
   							this.$refs.graphicVerification.handleReset()
   						}
   						return false
   					}
   					this.$refs.graphicVerification.close()
   					this.utils.goPath('/pages/public/login/getCode', this.form)
   				})
   			},
   		}
   	}
   </script>
   
   <style lang="less" scoped>
   	.index {
   		width: 100%;
   		height: 100%;
   		background: #FFFFFF;
   
   		.main {
   			padding: 60rpx 70rpx;
   			box-sizing: border-box;
   
   			.title {
   				font-size: 40rpx;
   				font-family: Source Han Sans CN-Medium, Source Han Sans CN;
   				font-weight: 500;
   				color: #333333;
   				margin-bottom: 59rpx;
   				
   				display: flex;
   				justify-content: space-between;
   				align-items: center;
   				.register {
   					font-size: 28rpx;
   					font-family: Source Han Sans CN-Medium, Source Han Sans CN;
   					font-weight: 500;
   					color: #3E9AFD;
   				}
   			}
   
   			.form {
   				margin-bottom: 50rpx;
   
   				.input {
   					position: relative;
   
   					input {
   						height: 102rpx;
   						line-height: 102rpx;
   						font-size: 28rpx;
   						font-family: Source Han Sans CN-Regular, Source Han Sans CN;
   						font-weight: 400;
   						color: #333;
   						border-bottom: 1px solid #EAEAEA;
   					}
   
   					.clearIcon {
   						width: 32rpx;
   						height: 32rpx;
   						position: absolute;
   						top: 50%;
   						right: 0;
   						margin-top: -16rpx;
   					}
   				}
   
   
   			}
   
   			.btnGroup {
   				.btn {
   					height: 90rpx;
   					line-height: 90rpx;
   					border-radius: 45rpx;
   					font-size: 28rpx;
   					font-family: Source Han Sans CN-Medium, Source Han Sans CN;
   					font-weight: 500;
   					margin-bottom: 15rpx;
   					color: #fff;
   					background-color: #3E9AFD;
   				}
   
   				.btn-disabled {
   					color: #FFFFFF;
   					background-color: #CCCCCC;
   				}
   
   				.btn-transparent {
   					color: #333;
   					background: transparent;
   				}
   			}
   		}
   	}
   </style>
   ```

   

2. 验证码输入页面

   ![image-20231011154428798](https://gitee.com/v876774538/my-img/raw/master/image-20231011154428798.png)

   ```vue
   <template>
   	<view class="index">
   		<goBack></goBack>
   		<view class="main">
   			<view class="title">请输入验证码</view>
   			<view class="des">
   				已发送至手机{{ form.phone }}
   			</view>
   			<view class="code">
   				<input type="number" v-model="form.code" :maxlength="maxLength" @input="onInput" @blur="onBlur"
   					@focus="onFocus" :focus="isFocus" @confirm="login()">
   				<view class="numbers">
   					<view class="number" v-for="(item, index) in codeArr">
   						<text>{{ item }}</text>
   						<view class="focusLine" v-if="isFocus && currentIndex + 1 == index"></view>
   					</view>
   				</view>
   				<view class="getCode">
   					<button v-show="codeShow" @tap="getCode()">获取验证码</button>
   					<button v-show="!codeShow" style="color: #ccc;">重新发送（{{count}})</button>
   				</view>
   			</view>
   		</view>
   	</view>
   </template>
   
   <script>
   	export default {
   		data() {
   			return {
   				form: {},
   				codeArr: ['', '', '', ''],
   				maxLength: 4,
   				currentIndex: -1,
   				isFocus: true, // 默认进入时获取输入焦点
   				// 获取验证码
   				codeShow: true,
   				count: '',
   				timer: null,
   				codeTouch: false,
   			};
   		},
   		onLoad(options) {
   			if (options && options.query) {
   				this.form = JSON.parse(options.query)
   				// this.getCode()
   				this.verification()
   			}
   		},
   		methods: {
   			// 输入验证码
   			onInput(e) {
   				var value = e.detail.value;
   				if (value.length <= this.maxLength) {
   					var valueArr = value.split('');
   					this.currentIndex = valueArr.length - 1
   					for (var i = 0; i < this.maxLength; i++) {
   						this.codeArr[i] = valueArr[i]
   					}
   				}
   			},
   			onBlur() {
   				this.isFocus = false
   			},
   			onFocus() {
   				this.isFocus = true
   			},
   			// 获取验证码
   			getCode() {
   				let regPhone = /^1[3456789]\d{9}$/;
   				if (this.utils.isNone(this.form.phone)) {
   					this.utils.showToast('请输入手机号码');
   					return false;
   				} else if (!regPhone.test(this.form.phone)) {
   					this.utils.showToast('手机号码格式有误');
   					return false;
   				}
   				if (this.codeTouch) {
   					return false
   				}
   				this.codeTouch = true
   				this.verification();
   				let api = uni.getStorageSync('userType') == 'client' ? this.APIURL.userGetCodeNoToken : this.APIURL
   					.merchantGetCodeNoToken
   				this.$http('post', api, {
   					phone: this.form.phone,
   					type: 2, // 登录
   					pictureId: this.form.pictureId,
   					pictureCode: this.form.pictureCode
   				}).then((res) => {
   					setTimeout(() => {
   						this.codeTouch = false
   					}, 500)
   					if (!res.success) {
   						this.utils.showToast(res.message)
   						return false
   					}
   					this.utils.showToast('短信发送成功');
   				})
   			},
   			// 验证码60s倒计时
   			verification() {
   				const TIME_COUNT = 60;
   				if (!this.timer) {
   					this.count = TIME_COUNT;
   					this.codeShow = false;
   					this.timer = setInterval(() => {
   						if (this.count > 1 && this.count <= TIME_COUNT) {
   							this.count--;
   						} else {
   							this.codeShow = true;
   							clearInterval(this.timer);
   							this.timer = null;
   						}
   					}, 1000)
   				}
   			},
   			// 登录
   			login() {
   				let userType = uni.getStorageSync('userType') ? uni.getStorageSync('userType') : 'client'
   
   				// 商家端
   				if (userType == 'merchant') {
   					this.$http('post', this.APIURL.merchantLogin, {
   						account: this.form.phone,
   						verCode: this.form.code,
   					}).then((res) => {
   						if (!res.success) {
   							this.utils.showToast(res.message)
   							return false
   						}
   						console.log('token', res.data)
   						uni.setStorageSync('token', res.data)
   						this.utils.reLaunch('/pages/merchant/tabBar/order')
   					})
   				}
   				// 用户端
   				else {
   					this.$http('post', this.APIURL.clientLogin, {
   						account: this.form.phone,
   						verCode: this.form.code,
   					}).then((res) => {
   						if (!res.success) {
   							this.utils.showToast(res.message)
   							return false
   						}
   						console.log('token', res.data)
   						uni.setStorageSync('token', res.data)
   						this.utils.reLaunch('/pages/client/tabBar/home')
   					})
   				}
   			},
   		},
   	}
   </script>
   
   <style lang="less" scoped>
   	.index {
   		width: 100%;
   		height: 100%;
   		background: #FFFFFF;
   
   		.main {
   			padding: 60rpx 70rpx;
   			box-sizing: border-box;
   
   			.title {
   				font-size: 40rpx;
   				font-family: Source Han Sans CN-Medium, Source Han Sans CN;
   				font-weight: 500;
   				color: #333333;
   				margin-bottom: 20rpx;
   			}
   
   			.des {
   				font-size: 28rpx;
   				font-family: Source Han Sans CN-Regular, Source Han Sans CN;
   				font-weight: 400;
   				color: #CCCCCC;
   				margin-bottom: 70rpx;
   			}
   
   			.code {
   				position: relative;
   
   				input {
   					position: relative;
   					z-index: 2;
   					width: 100%;
   					height: 120rpx;
   					color: transparent;
   					margin-bottom: 40rpx;
   				}
   
   				.numbers {
   					position: absolute;
   					top: 0;
   					width: 100%;
   					z-index: 1;
   					display: flex;
   					justify-content: space-between;
   					align-items: center;
   
   					.number {
   						position: relative;
   						width: 120rpx;
   						height: 120rpx;
   						line-height: 120rpx;
   						text-align: center;
   						border-radius: 16rpx;
   						background: #f6f6f6;
   						font-size: 60rpx;
   						font-family: Source Han Sans CN-Regular, Source Han Sans CN;
   						font-weight: 400;
   						color: #333333;
   
   						.focusLine {
   							position: absolute;
   							left: 0;
   							top: 25%;
   							width: 1px;
   							height: 50%;
   							background: #000;
   							opacity: 1;
   							-webkit-animation: sharkLight 1s linear infinite;
   							animation: sharkLight 1s linear infinite;
   						}
   
   						@-webkit-keyframes sharkLight {
   							from {
   								-webkit-transform: scale(1);
   								opacity: 1;
   							}
   
   							to {
   								-webkit-transform: scale(0.9);
   								opacity: 0;
   							}
   						}
   					}
   
   
   				}
   
   				.getCode {
   					button {
   						font-size: 28rpx;
   						font-family: Source Han Sans CN-Regular, Source Han Sans CN;
   						font-weight: 400;
   						color: #333;
   						background: transparent;
   						text-align: left;
   						height: 40rpx;
   						line-height: 40rpx;
   					}
   				}
   			}
   		}
   	}
   </style>
   ```

### 89.日期范围选择弹窗

> 杉通宝公众号项目：http://syy333.dynv6.net:20080/syy/shantongbao-exchange.git

#### 89.1 效果

未选择时显示【全部】；选择某日时显示具体日期，如【2023-10-11】；选择日期范围显示【区间】；按月份选择则显示具体月份，如【2023-10】

<img src="https://gitee.com/v876774538/my-img/raw/master/image-20231011155244225.png" alt="image-20231011155244225"  />

![image-20231011155259912](https://gitee.com/v876774538/my-img/raw/master/image-20231011155259912.png)

#### 89.2 组件

![image-20231011155620675](https://gitee.com/v876774538/my-img/raw/master/image-20231011155620675.png)

`utils.js`

```js
/**
 * 获取某年某月有多少天
 */
export const getOneMonthDays = (year,month)=>{
	month = Number(month);
	const baseMonthsDays = [31,28,31,30,31,30,31,31,30,31,30,31];
	if(year % 4 == 0 && (year % 100 != 0 || year % 400 == 0)){
		if(month === 2){
			baseMonthsDays[month] = 29;
		}
	}
	return baseMonthsDays[month];
}

/**
 * 获取日期的年月日时分秒
 */
export const getTimeArray = (date)=>{
	const year = date.getFullYear();
	const month = date.getMonth()+1;
	const day = date.getDate();
	const hour = date.getHours();
	const minute = date.getMinutes();
	const second = date.getSeconds();
	return [year,month,day,hour,minute,second];
}
/**
 * 小于10的数字前面补0
 */
export const addZero = (num)=>{
	return num < 10 ? '0' + num : num;
}

/**
 * 获取当前值在数组中的索引
 */
export const getIndexOfArray = (value,array)=>{
	let index = array.findIndex(item => item == value);
	return index > -1 ? index : 0;
}
```

`jp-timePicker.vue`

```vue
<template>
	<view class="date-time-picker" v-if="visible">
		<view class="date-time-mask" @click.stop="hide"></view>
		<view class="date-time-container" @click.stop="handleEvent">
			<view class="time-picker-tool">
				<view class="cancel-btn">
				</view>
				<view class="tool-title">
					<text>选择时间</text>
				</view>
				
				<view class="cancel-btn" @click.stop="cancel">
					<image class="cancal" src="https://api.fzhuanmi.com/file/static2/recycle/cancal.png" mode=""></image>
				</view>
			</view>
			<view class="jp-picker">
				<!-- <view @click="gettype('year')" class="jp-picker-year"  :class="type=='year'?'jp-picker-xzr':''">按年</view> -->
				
				<view @click="gettype('date')" class="jp-picker-year-month" :class="type=='date'?'jp-picker-xzr':''">按日选择</view>
				<view @click="gettype('year-month')" class="jp-picker-year-month jp-picker-date "
					:class="type=='year-month'?'jp-picker-xzr':''">按月选择</view>
			</view>
			
			<view class="date-time" v-if="type!='date'">
				{{formatDateArrays1[0]}}-{{formatDateArrays1[1]}}
			</view>
			<view class="date-time date-time2" v-else>
				<view class="left" @click="changeTab('left')" :class="tabType=='left'?'active':''">
					<text v-if="formatDateArrays2!=[]">{{formatDateArrays2[0]}}-{{formatDateArrays2[1]}}-{{formatDateArrays2[2]}}</text>
					<text v-else>请选择</text>
				</view>
				<text style="color: #333333;">至</text>
				<view class="left right"  @click="changeTab('right')" :class="tabType=='right'?'active':''">
					<text v-if="formatDateArrays3.length!=0">{{formatDateArrays3[0]}}-{{formatDateArrays3[1]}}-{{formatDateArrays3[2]}}</text>
					<text v-else>请选择</text>
					<!-- {{formatDateArrays3}} -->
				</view>
			</view>
			
			<picker-view class="picker-view" :indicator-style="indicatorStyleString" :value="dateTime"
				@change="dateTimePickerChange">
				<picker-view-column data-id='year' v-if='isShowYear'>
					<view class="item" v-for="(item,index) in years" :key="index"
						:style="formatDateArrays[0]==item?'color: #1890FF':''">{{item}}年</view>
				</picker-view-column>
				<picker-view-column data-id='month' v-if='isShowMonth'>
					<view class="item" v-for="(item,index) in months" :key="index"
						:style="formatDateArrays[1]==item?'color: #1890FF':''">{{item}}月</view>
				</picker-view-column>
				<picker-view-column data-id='day' v-if='isShowDay'>
					<view class="item" v-for="(item,index) in days" :key="index"
						:style="formatDateArrays[2]==item?'color: #1890FF':''">{{item}}日</view>
				</picker-view-column>
			</picker-view>
			
			
			<view class="confirm-btn" @click.stop="confirm">
				确定
			</view>
		</view>
	</view>
</template>

<script>
	import {
		getOneMonthDays,
		getTimeArray,
		addZero,
		getIndexOfArray,
	} from './uitls/util.js'
	export default {
		name: 'jp-timePicker',
		props: {
			startYear: {
				type: Number,
				default: 1900
			},
			endYear: {
				type: Number,
				default: new Date().getFullYear()
			},
			datestring: {
				type: [String, Array],
				default: ''
			},
			datestype: {
				type: String,
				default: 'year'
			},
		},
		data() {
			return {
				formatDateArrays: [],
				formatDateArrays1: [],
				formatDateArrays2: [],
				formatDateArrays3: [],
				visible: false,
				dateTime: [],
				days: [],
				indicatorStyle: {
					background: '',
					height: '40px',
				},
				indicatorStyleString: '',
				type: 'year',
				tabType:'left'
			}
		},
		watch: {
			datestype() {
				this.type = this.datestype
			},
			indicatorStyle(val) {
				this.getIndicatorStyle();
			},
			type() {
				this.initDateTime()
			},
			datestring() {
				this.initDateTime()
			}
		},
		computed: {
			years() {
				return this.initTimeData(this.endYear, this.startYear);
			},
			isShowYear() {
				return this.type !== 'time' && this.type !== 'hour-minute';
			},
			months() {
				return this.initTimeData(12, 1);
			},
			isShowMonth() {
				return this.type !== 'year' && this.type !== 'time' && this.type !== 'hour-minute';
			},
			isShowDay() {
				return this.type === 'date' || this.type === 'datetime' || this.type === 'datetime-all';
			},
			hours() {
				return this.initTimeData(23, 0);
			},
			isShowHour() {
				return this.type !== 'date' && this.type !== 'year-month' && this.type !== 'year';
			},
			minutes() {
				return this.initTimeData(59, 0);
			},
			isShowMinute() {
				return this.type !== 'date' && this.type !== 'year-month' && this.type !== 'year';
			},
			seconds() {
				return this.initTimeData(59, 0);
			},
			isShowSecond() {
				return this.type === 'datetime-all' || this.type === 'time';
			}
		},
		methods: {
			changeTab(type) {
				this.tabType = type
			},
			gettype(type) {
				this.type = type
			},
			getIndicatorStyle() {
				if (this.indicatorStyle) {
					for (let key in this.indicatorStyle) {
						this.indicatorStyleString += `${key}:${this.indicatorStyle[key]};`
					}
				}
			},
			handleEvent() {
				return;
			},
			cancel() {
				this.hide();
				this.$emit('cancel')
			},
			confirm() {
				if(this.type === 'date') {
					console.log('formatDateArrays2', this.formatDateArrays2)
					console.log('formatDateArrays3', this.formatDateArrays3)
					if((this.formatDateArrays2 == '' || (this.formatDateArrays2 && this.formatDateArrays2.length == 0)) || this.formatDateArrays3 == '' || (this.formatDateArrays3 && this.formatDateArrays3.length == 0)) {
						this.utils.showToast('请选择日期')
						return false
					}
					// 比较日期大小
					else {
						var startDate = Array(this.formatDateArrays2).join('-')
						var endDate = Array(this.formatDateArrays3).join('-')
						console.log('startDate:', new Date(startDate))
						console.log('endDate:', new Date(endDate))
						if (new Date(startDate) > new Date(endDate)) {
							this.utils.showToast('日期区间错误')
							return false
						}
					}
				}
				this.formatDate();
				this.hide();
			},
			show() {
				this.visible = true;
			},
			hide() {
				this.visible = false;
			},
			initDateTime() {
				let value;
				if (this.datestring.length > 0) {
					if (this.type === 'year') {
						value = new Date(this.datestring, 0);
					} else if (this.type === 'time' || this.type === 'hour-minute') {
						let date = new Date();
						let ary = this.datestring.split(':');
						ary.forEach((item, index) => {
							if (index == 0) {
								date.setHours(item)
							} else if (index == 1) {
								date.setMinutes(item)
							} else if (index == 2) {
								date.setSeconds(item)
							}
						})
						value = date;
					} else {
						value = new Date(this.datestring.replace(/-/g, '/'));
					}

				} else {
					value = new Date();
				}
				let len, timeArray, index;
				let array = getTimeArray(value);
				let [year, month, day, hour, minute, second] = array;
				this.days = this.initTimeData(getOneMonthDays(year, month - 1), 1);
				let names = ['year', 'month', 'day', 'hour', 'minute', 'second'];
				switch (this.type) {
					case "date":
						len = 3;
						break;
					case "year-month":
						len = 2;
						break;
					case "year":
						len = 1;
						break;
					case "datetime":
						len = 5;
						break;
					case "datetime-all":
						len = 6;
						break;
					case "time":
						len = 3;
						break;
					case "hour-minute":
						len = 2;
						break;
				}
				timeArray = new Array(len).fill(0);
				if (this.type === 'time' || this.type === 'hour-minute') {
					names = names.slice(3);
					array = array.slice(3);
				}
				timeArray = timeArray.map((item, index) => {
					const name = names[index];
					return getIndexOfArray(array[index], this[name + 's'])
				})
				this.dateTime = timeArray;

				if (this.type === 'date' || this.type === 'year-month' || this.type === 'year') {
					this.formatDateArrays = this.dateTime.map((item, index) => {
						return this[names[index] + 's'][item] < 10 ? addZero(this[names[index] + 's'][item]) :
							this[names[index] + 's'][item];
					})
				}
				// console.log("this.formatDateArrays:",this.formatDateArrays)
				if(this.type=='year-month') {
					this.formatDateArrays1=this.formatDateArrays
				}
				if(this.type=='date'&&this.tabType=='left') {
					this.formatDateArrays2=this.formatDateArrays
				}
				if(this.type=='date'&&this.tabType=='right') {
					this.formatDateArrays3=this.formatDateArrays
				}
			},
			initTimeData(end, start) {
				let timeArray = [];
				while (start <= end) {
					timeArray.push(start);
					start++;
				}
				return timeArray;
			},
			formatDate() {
				let names = ['year', 'month', 'day', 'hour', 'minute', 'second'];
				let dateString=[], formatDateArray = [];
				// if (this.type === 'date' || this.type === 'year-month' || this.type === 'year') {
				// 	formatDateArray = this.dateTime.map((item, index) => {
				// 		return this[names[index] + 's'][item] < 10 ? addZero(this[names[index] + 's'][item]) :
				// 			this[names[index] + 's'][item];
				// 	})
				// 	dateString = formatDateArray.join('-');
				// }
				// console.log("this.formatDateArrays1: ",this.formatDateArrays1);
				// console.log("this.formatDateArrays2: ",this.formatDateArrays2);
				// console.log("this.formatDateArrays:3 ",this.formatDateArrays3);
				dateString.formatDateArrays1 = this.formatDateArrays1
				dateString.formatDateArrays2 = this.formatDateArrays2
				dateString.formatDateArrays3 = this.formatDateArrays3
				dateString.type = this.type
				this.$emit('change', dateString)
			},
			dateTimePickerChange(e) {
				let columns = e.target.value;
				if (this.type === 'date' || this.type === 'datetime' || this.type === 'datetime-all') {
					this.dateTime.splice(0, 1, columns[0]);
					if (columns[0] != this.dateTime[0]) {
						this.days = this.initTimeData(getOneMonthDays(this.years[this.dateTime[0]], this.months[this
							.dateTime[1]]), 1);
						if (this.dateTime[1] == 1) {
							if (this.dateTime[2] === this.days.length - 1) {
								if (getOneMonthDays(this.years[columns[0]], this.dateTime[1]) < getOneMonthDays(this.years[
										this.dateTime[0]], this.dateTime[1])) {
									this.dateTime.splice(2, 1, this.days.length - 1)
								}
							}
						}
					} else {
						this.dateTime.splice(1, 1, columns[1]);
						this.days = this.initTimeData(getOneMonthDays(this.years[this.dateTime[0]], this.dateTime[1]), 1);
						if (columns[1] != this.dateTime[1]) {
							if (this.dateTime[1] == 1) {
								if (this.dateTime[2] === this.days.length - 1) {
									if (getOneMonthDays(this.years[columns[0]], this.dateTime[1]) < getOneMonthDays(this
											.years[this.dateTime[0]],
											this.dateTime[1])) {
										this.dateTime.splice(2, 1, this.days.length - 1)
									}
								}
							} else {
								if (this.dateTime[2] > this.days.length - 1) {
									this.dateTime.splice(2, 1, this.days.length - 1)
								} else {
									this.dateTime.splice(2, 1, columns[2])
								}
							}
						} else {
							this.dateTime.splice(2, 1, columns[2])
						}
					}
					if (columns.length > 2) {
						columns.splice(3).forEach((column, index) => {
							this.dateTime.splice(index + 3, 1, column);
						})
					}
				} else {
					columns.forEach((column, index) => {
						this.dateTime.splice(index, 1, column);
					})
				}
				// if (!this.isShowToolBar) {
				// 	this.formatDate();
				// }

				let names = ['year', 'month', 'day', 'hour', 'minute', 'second'];
				this.formatDateArrays = [];
				if (this.type === 'date' || this.type === 'year-month' || this.type === 'year') {
					this.formatDateArrays = this.dateTime.map((item, index) => {
						return this[names[index] + 's'][item] < 10 ? addZero(this[names[index] + 's'][item]) :
							this[names[index] + 's'][item];
					})
				}
				console.log(this.formatDateArrays)
				if(this.type=='year-month') {
					this.formatDateArrays1=this.formatDateArrays
				}
				if(this.type=='date'&&this.tabType=='left') {
					this.formatDateArrays2=this.formatDateArrays
				}
				if(this.type=='date'&&this.tabType=='right') {
					this.formatDateArrays3=this.formatDateArrays
				}
			},
		
				
		},
		mounted() {
			this.type = this.datestype
			this.getIndicatorStyle();
			this.initDateTime();
		}
	}
</script>

<style lang='scss' scoped>
	.date-time-picker {
		.date-time-mask {
			position: fixed;
			top: 0;
			bottom: 0;
			left: 0;
			right: 0;
			background-color: rgba($color: #000000, $alpha: .5);
			z-index: 998;
		}

		.jp-picker {
			background-color: #fff;
			display: flex;
			justify-content: center;
			align-items: center;
			height: 120rpx;
			font-size: 30rpx;
			
		}

		.jp-picker-year {
			padding: 10rpx 20rpx;
			border-top-left-radius: 30rpx;
			border-bottom-left-radius: 30rpx;
			height: 30rpx;
			line-height: 30rpx;
		}

		.jp-picker-year-month {
			width: 285rpx;
			height: 90rpx;
			line-height: 90rpx;
			text-align: center;
			font-size: 32rpx;
			color: #1890FF;
			border-radius: 20rpx 0 0 20rpx;
			border: 1rpx solid #1890FF;
		}

		.jp-picker-date {
			border-radius: 0 20rpx 20rpx 0;
		}

		.jp-picker-xzr {
			background-color: #1890FF;
			color: #fff;
		}

		.date-time-container {
			position: fixed;
			height: 60%;
			bottom: 0;
			right: 0;
			left: 0;
			background-color: #fff;
			z-index: 999;
			display: flex;
			flex-direction: column;

			.time-picker-tool {
				height: 80rpx;
				display: flex;
				align-items: center;
				justify-content: space-between;
				font-size: 28rpx;

				.cancel-btn {
					padding: 0 28rpx;
					box-sizing: border-box;
					color: #333;
					
					
					.cancal {
						width: 35rpx;
						height: 35rpx;
					}
				}

				.tool-title {
					font-weight: 500;
					font-size: 16px;
					max-width: 50%;
					overflow: hidden;
					white-space: nowrap;
					text-overflow: ellipsis;
				}

			
			}
			
			
			
			
			.date-time {
				padding-bottom: 11rpx;
				box-sizing: border-box;
				margin: 60rpx auto;
				color: #1890FF;
				font-size: 32rpx;
				width: 515rpx;
				text-align: center;
				border-bottom: 1rpx solid #1890FF;
			}
			
			
			.date-time2 {
				display: flex;
				justify-content: space-between;
				border-bottom: none;
				
				
				.left {
					margin-right: 40rpx;
					padding-bottom: 11rpx;
					box-sizing: border-box;
					border-bottom: 1rpx solid #333333;
					width: 230rpx;
					text-align: center;
					color: #333333;
				}
				
				
				.right {
					margin-left: 40rpx;
					margin-right: 0;
				}
				
				
				.active {
					color: #1890FF;
					border-bottom: 1rpx solid #1890FF;
				}
			}

			.picker-view {
				width: 100%;
				flex: 1;

				.item {
					font-size: 34rpx;
					display: flex;
					align-items: center;
					justify-content: center;
				}
			}
		
		
			.confirm-btn {
				margin: 36rpx auto;
				width: 570rpx;
				height: 90rpx;
				border-radius: 20rpx;
				background-color: #1890FF;
				font-size: 32rpx;
				line-height: 92rpx;
				text-align: center;
				color: #fff;
			}
		
		
		}
	}
</style>
```

#### 89.3 使用

```vue
<template>
	<view class="index">
		<view class="main">
			<image src="@/static/home/bg2.png" mode="" class="bg"></image>
			<view class="card card-total">
				<view class="row1">
					<view class="left">
						我的收益（元）
					</view>
					<view class="right" @tap="utils.goPath('/pages/merchant/my/setPayPassword/verification')">
						<image src="@/static/my/setIcon.png" mode=""></image>
						<text>支付密码</text>
					</view>
				</view>
				<view class="row2">
					<view class="left">
						<image src="@/static/my/balanceIcon.png" mode=""></image>
						<text>{{ utils.numberFilter(merchantInfo.balance, 2) }}</text>
					</view>
					<button class="right btn" @tap="utils.goPath('/pages/merchant/my/withdraw')">
						<text>提现</text>
						<image src="@/static/arrow-right-white.png" mode=""></image>
					</button>
				</view>
				<view class="row3">
					<view class="left">
						<text>当日收益</text><text>+{{ utils.numberFilter(merchantInfo.intradayMoney, 2) }}</text>
					</view>
					<view class="right">
						<text>合计收益</text><text>+{{ utils.numberFilter(merchantInfo.sumMoney, 2) }}</text>
					</view>
				</view>
			</view>
			<view class="card card-detail">
				<view class="header">
					<view class="left">
						<view class="li" v-for="(item, index) in tabs" :class="selectIndex == index ? 'li-active' : ''"
							@tap="handleTabChange(index)">
							<text>{{ item.label }}</text>
						</view>
					</view>
					<view class="right" @tap="handleDate()">
						<text :class="dateShow != '全部' ? 'fontColorBlue' : ''">{{ dateShow }}</text>
						<image src="@/static/my/calanderIcon.png" mode="" v-if="dateShow == '全部'"></image>
						<image src="@/static/my/calanderIcon-active.png" mode="" v-else></image>
					</view>
				</view>
				<view class="content">
					<view class="li" v-for="(item, index) in list" :key="item.id">
						<view class="left">
							<text class="row1">
								{{ item.earningsType | earningsTypeFilter }}
							</text>
							<text class="row2">
								{{ item.createTime }}
							</text>
						</view>
						<view class="right">
							<text :class="item.earnings == '+' ? 'fontColorBlue' : ''">{{ item.earnings }}{{ utils.numberFilter(item.money, 2) }}</text>
						</view>
					</view>
				</view>
			</view>
			<uni-load-more :status="loadStatus" :content-text="contentText"></uni-load-more>
		</view>
		<tabBar currentPage="/pages/merchant/tabBar/my"></tabBar>
		<!-- 日期选择 -->
		<jpTimePicker ref='date-time' :datestype="type" :datestring='dateString' @change='dateTimeChange'></jpTimePicker>
	</view>
</template>

<script>
	import jpTimePicker from '@/components/jp-timePicker/jp-timePicker.vue'
	export default {
		components: {
			jpTimePicker,
		},
		data() {
			return {
				merchantInfo: {},	// 商户信息
				
				form: {
					earnings: '',	// 收益 +收入 -支出
					earingsType: '',	// 流水类型
					createTimeStart: '',	// 开始时间
					createTimeEnd: '',	// 结束时间
				},
				
				selectIndex: 0,
				tabs: [{
						label: '收益明细',
						val: ''
					},
					{
						label: '支出',
						val: '-'
					},
					{
						label: '收入',
						val: '+'
					},
				],
				
				list: [],	// 积分流水
				pagination: {
					pageSize: 10,
					pageNo: 1
				},	// 分页
				
				// 加载更多
				contentText: {
					contentdown: "上拉显示更多",
					contentrefresh: "正在加载...",
					contentnomore: "没有更多数据了"
				},
				loadStatus: "loading", //'loading','noMore'
				
				// 日期选择
				dateString: '',
				dateShow: '全部',	// 筛选列表展示的日期
				type: 'date',
				month: '',
				date: '',
				form: {},
				timeType: '',
			};
		},
		onLoad() {
			// 获取用户信息
			this.utils.updateMerchantInfo((data) => {
				this.merchantInfo = data
				this.handleSearch()
			})
		},
		methods: {
			// 获取收益统计
			getEarningSum() {
				this.$http('get', this.APIURL.getEarningSum).then((res) => {
					if (!res.success) {
						this.utils.showToast(res.message)
						return false
					}
					this.merchantInfo = Object.assign(this.merchantInfo, res.data)
					uni.setStorageSync('merchantInfo', this.merchantInfo)
					this.$forceUpdate()
				})
			},
			// 收益流水查询
			getEarningFlow() {
				this.$http('post', this.APIURL.getEarningFlow + `?pageNo=${this.pagination.pageNo}&pageSize=${this.pagination.pageSize}`, {
					createTimeStart: this.form.createTimeStart,
					createTimeEnd: this.form.createTimeEnd,
					earnings: this.form.earnings,
				}).then((res) => {
					if (!res.success) {
						this.utils.showToast(res.message)
						return false
					}
					this.list = this.list.concat(res.data.rows)
					if(this.list.length >= res.data.totalRows){
						this.loadStatus = "noMore";
					}
				})
			},
			handleClear() {
				this.list = []
				this.pagination.pageNo = 1
				this.loadStatus = 'loading'
			},
			// 查询
			handleSearch() {
				this.getEarningSum()
				this.handleClear()
				this.getEarningFlow()
			},
			handleTabChange(index) {
				this.selectIndex = index
				this.form.earnings = this.tabs[this.selectIndex].val
				this.handleSearch()
			},
			// 打开日期选择弹窗
			handleDate() {
				this.timeType = ''
				this.$refs['date-time'].show();
			},
			// 日期选择
			dateTimeChange(value) {
				this.dateString = value
				console.log("value: ",value);
				
				// 按月选择
				if (value.type == 'year-month') {
					this.month = value.formatDateArrays1.join('-')
					console.log("this.month: ", this.month);
					this.timeType  = this.month
					this.date= ''
					
					this.dateShow = this.timeType
					
					this.form.createTimeStart = this.month + '-01'
					this.form.createTimeEnd = this.getLastDay(value.formatDateArrays1[0], value.formatDateArrays1[1])
					console.log('form', this.form)
				}
				// 按日期选择
				else {
					this.date = value.formatDateArrays2.join('-') + ' - ' + value.formatDateArrays3.join('-')
					console.log("this.date: ", this.date);
					this.timeType  = this.date
					this.month = ''
					
					if (value.formatDateArrays2.join('-') == value.formatDateArrays3.join('-')) {
						this.dateShow = value.formatDateArrays2.join('-')
					}
					else {
						this.dateShow = '区间'
					}
					
					this.form.createTimeStart = value.formatDateArrays2.join('-')
					this.form.createTimeEnd = value.formatDateArrays3.join('-')
					console.log('form', this.form)
				}
				
				this.handleSearch()
			},
			// 获取当月最后一天
			getLastDay(year, month) {
				var lastDay = new Date(year, month, 0)
				return `${year}-${month}-${lastDay.getDate()}`
			}
		},
		filters: {
			earningsTypeFilter(val) {
				switch(val) {
					case 1:
						return 'POS交易'
					case 2:
						return '积分兑换'
					case 3:
						return '退款'
					default:
						return ''
				}
			}
		},
		//上拉加载
		onReachBottom() {
			if(this.loadStatus == 'loading'){
				this.pagination.pageNo = this.pagination.pageNo + 1;
				this.getEarningFlow()
			}
		},
		//下拉刷新
		onPullDownRefresh() {
			this.loadStatus = "loading";
			this.handleSearch()
			setTimeout(()=>{
				uni.stopPullDownRefresh()
			},800)
		},
	}
</script>

<style lang="less" scoped>
	.fontColorBlue {
		color: #3E9AFD;
	}
	
	.index {
		.main {
			position: relative;
			padding: 210rpx 30rpx 120rpx;
			box-sizing: border-box;

			.bg {
				width: 100%;
				height: 450rpx;
				position: fixed;
				top: 0;
				left: 0;
				right: 0;
				z-index: 0;
			}

			.card {
				position: relative;
				background: #fff;
				border-radius: 20rpx;
			}

			.card-total {
				padding: 40rpx 40rpx 30rpx;
				box-sizing: border-box;
				font-family: Source Han Sans CN-Medium, Source Han Sans CN;
				font-weight: 500;
				color: #333333;
				margin-bottom: 20rpx;
				
				.row1,
				.row2,
				.row3 {
					display: flex;
					align-items: center;
				}
				
				.row1 {
					font-size: 28rpx;
					margin-bottom: 30rpx;
					justify-content: space-between;
					
					.right {
						display: flex;
						align-items: center;
						
						image {
							width: 24rpx;
							height: 24rpx;
							margin-right: 10rpx;
						}
					}
				}

				.row2 {
					font-size: 48rpx;
					margin-bottom: 40rpx;
					justify-content: space-between;

					image {
						width: 48rpx;
						height: 48rpx;
						margin-right: 20rpx;
					}
					
					.right {
						height: 60rpx;
						line-height: 60rpx;
						background: #3E9AFD;
						border-radius: 34rpx;
						padding: 0 30rpx;
						box-sizing: border-box;
						display: flex;
						align-items: center;
						font-size: 28rpx;
						font-family: Source Han Sans CN-Medium, Source Han Sans CN;
						font-weight: 500;
						color: #FFFFFF;
						
						image {
							width: 25rpx;
							height: 25rpx;
							margin: 0;
							margin-left: 10rpx;
						}
					}
				}

				.row3 {
					justify-content: space-between;
					font-size: 28rpx;
					font-family: Source Han Sans CN-Regular, Source Han Sans CN;
					font-weight: 400;
					color: #999999;
				}
			}

			.card-detail {
				padding: 40rpx 30rpx;
				box-sizing: border-box;

				.header {
					display: flex;
					justify-content: space-between;
					align-items: center;

					.left {
						display: flex;
						align-items: flex-end;

						.li {
							margin-right: 30rpx;
							font-size: 28rpx;
							font-family: Source Han Sans CN-Medium, Source Han Sans CN;
							font-weight: 500;
							color: #333333;
							position: relative;

							text {
								position: relative;
								z-index: 1;
							}
						}

						.li:first-child {
							font-size: 36rpx;
						}

						.li-active:after {
							content: '';
							display: block;
							width: 100%;
							height: 3px;
							background: #3E9AFD;
							position: absolute;
							bottom: 4rpx;
							z-index: 0;
						}
					}

					.right {
						background: #EAECFF;
						border-radius: 26rpx;
						width: fit-content;
						height: 51rpx;
						line-height: 51rpx;
						display: flex;
						align-items: center;
						padding: 0 23rpx;
						box-sizing: border-box;
						font-size: 28rpx;
						font-family: Source Han Sans SC-Medium, Source Han Sans SC;
						font-weight: 500;
						color: #333333;
						
						image {
							width: 24rpx;
							height: 24rpx;
							margin-left: 9rpx;
						}
					}
				}
			
				.content {
					.li {
						padding: 30rpx 0;
						box-sizing: border-box;
						display: flex;
						justify-content: space-between;
						border-bottom: 1px solid #E7E7E7;
						
						.left {
							display: flex;
							flex-direction: column;
							
							.row1 {
								font-size: 32rpx;
								font-family: Source Han Sans SC-Medium, Source Han Sans SC;
								font-weight: 500;
								color: #333333;
								margin-bottom: 10rpx;
							}
							
							.row2 {
								font-size: 24rpx;
								font-family: Source Han Sans SC-Regular, Source Han Sans SC;
								font-weight: 400;
								color: #999999;
							}
						}
						
						.right {
							font-size: 32rpx;
							font-family: Source Han Sans SC-Medium, Source Han Sans SC;
							font-weight: 500;
							color: #333333;
						}
					}
					
					.li:last-child {
						border-bottom: 0;
						padding-bottom: 0;
					}
				}
			}
		}
	}
</style>
```

### 90.大屏适配

参考：https://blog.csdn.net/Liushiliu104/article/details/129372083?spm=1001.2100.3001.7377&utm_medium=distribute.pc_feed_blog_category.none-task-blog-classify_tag-8-129372083-null-null.nonecase&depth_1-utm_source=distribute.pc_feed_blog_category.none-task-blog-classify_tag-8-129372083-null-null.nonecase

#### 90.1 rem+font-size

> SANTIME项目：http://syy333.dynv6.net:20080/syy/santime.git

```js
<script>
    (function (win) {
        var tid;

        function refreshRem() {
            let designSize = 1920; // 设计图尺寸
            let html = document.documentElement;
            let wW = html.clientWidth; // 窗口宽度
            let rem = (wW * 100) / designSize;
            document.documentElement.style.fontSize = rem + "px";
        }

        win.addEventListener(
            "resize",
            function () {
                clearTimeout(tid);
                tid = setTimeout(refreshRem, 300);
            },
            false
        );
        win.addEventListener(
            "pageshow",
            function (e) {
                if (e.persisted) {
                    clearTimeout(tid);
                    tid = setTimeout(refreshRem, 300);
                }
            },
            false
        );

        refreshRem();
    })(window);

    $(function () {
        $("#foot").load("foot.html");
    });
</script>
```

![image-20231011164950570](https://gitee.com/v876774538/my-img/raw/master/image-20231011164950570.png)

#### 90.2 scale缩放

三益友官网：http://syy333.dynv6.net:20080/zhangzl/syy.git master分支

```js
window.onload = function() {
  setScale();
}
window.onresize = function () {
  setScale();
};
function setScale() {
  // 设计稿：1920 * 1080
  // 1.设计稿尺寸
  let targetWidth = 1920;
  // 2.拿到当前设备（浏览器）的宽度
  // document.documentElement  获取html的宽度
  let currentWidth = document.documentElement.clientWidth || document.body.clientWidth;
  // 3.计算缩放比率(屏幕过宽，根据高度计算缩放比例)
  let scaleRatio = currentWidth / targetWidth;
  // 4.开始缩放网页
  // 宽度>1920 顶部中心缩放
  if (currentWidth > targetWidth) {
    document.body.style = `transform: scale(${scaleRatio}); transform-origin: top center;`;
  }
  // 宽度<1920 顶部靠左缩放
  else {
    document.body.style = `transform: scale(${scaleRatio}); transform-origin: top left;`;
  }
}
```

注意：`transform`会导致顶部导航栏`position:fixed`失效，故只能使用`position:absolute`，采用将滚动距离赋值给绝对定位的元素的方法。

```js
handleScroll() {
  var scrollTop =
    window.pageYOffset ||
    document.documentElement.scrollTop ||
    document.body.scrollTop;
  // let top = this.selectIndex == 0 ? 670 : 502;
  let top = document.documentElement.querySelector(".header").offsetHeight + document.documentElement.querySelector(".header").offsetTop;
  var headerElement = document.documentElement.querySelector(".header1");
  if (scrollTop >= top) {
    if (!this.show) {
      this.show = true;
      this.show1 = true;
    }
    headerElement.style = `top: ${scrollTop / this.scaleRatio}px`;
  } else {
    if (this.show) {
      this.show1 = false;
      setTimeout(() => {
        this.show = false;
      }, 400);
    }
  }
},
```

完整代码：

```vue
<template>
  <div class="index">
    <div
      class="main1"
      :style="{ height: selectIndex == 0 ? '670px' : '502px' }"
    >
      <div style="height: 25px"></div>
      <div class="header" id="header">
        <div class="left">
          <img
            @click="goPath({ path: '/home' })"
            src="@/assets/img/logo1.png"
            alt=""
          />
        </div>
        <div class="right">
          <ul>
            <li
              class="li"
              v-for="(item, index) in menuList"
              :key="index"
              @click="selectMenu(index)"
            >
              <div :class="selectIndex == index ? 'active' : ''">
                {{ item.name }}
              </div>
            </li>
            <div class="kailong" v-show="selectIndex == 2"></div>
            <div class="program" v-show="selectIndex == 2">
              <div
                :class="paySelectIndex == 0 ? 'programActive' : ''"
                @click="paySelect(0)"
              >
                金融支付
              </div>
              <div
                :class="paySelectIndex == 1 ? 'programActive' : ''"
                @click="paySelect(1)"
              >
                互联网
              </div>
              <div
                :class="paySelectIndex == 2 ? 'programActive' : ''"
                @click="paySelect(2)"
              >
                跨境 / 进出口
              </div>
            </div>
          </ul>
        </div>
      </div>
      <div
        class="header header1"
        :class="show1 ? 'slideUp' : 'slideDown'"
        v-show="show"
      >
        <div class="left">
          <img
            @click="goPath({ path: '/home' })"
            src="@/assets/img/logo2.png"
            alt=""
          />
        </div>
        <div class="right">
          <ul>
            <li
              v-for="(item, index) in menuList"
              :key="index"
              @click="selectMenu(index)"
            >
              <div :class="selectIndex == index ? 'active' : ''">
                {{ item.name }}
              </div>
            </li>
          </ul>
        </div>
      </div>
      <img class="homeBg" :src="menuList[selectIndex].img" alt="" />
      <div class="title" :style="{ top: selectIndex == 0 ? '258px' : '220px' }">
        {{ menuList[selectIndex].title }}
      </div>
      <div class="des" :style="{ top: selectIndex == 0 ? '377px' : '320px' }">
        {{ menuList[selectIndex].des }}
      </div>
      <img
        class="select"
        src="@/assets/img/select.png"
        alt=""
        v-show="selectIndex == 0"
      />
    </div>
    <router-view />
    <div class="foot">
      <div class="content">
        <div class="foot1">
          <div><img src="@/assets/img/footLogo.png" alt="" /></div>
          <div><span @click="goPath({ path: '/aboutUs' })">关于我们</span></div>
          <div><span @click="goPath({ path: '/new' })">新闻资讯</span></div>
          <div>
            <span @click="goPath({ path: '/contactUs' })">联系我们</span>
          </div>
        </div>
        <div class="foot2" style="margin-top: 20px">
          <div style="color: #333333"><span>关注我们</span></div>
          <div>
            <span @click="goPath({ path: '/solutionPay' })">解决方案</span>
          </div>
          <div>
            <span @click="goPath({ path: '/new', query: { type: 0 } })"
              >公司资讯</span
            >
          </div>
          <div>你更喜欢电子邮件吗?</div>
        </div>
        <div class="foot2">
          <div>实时动态与招聘信息</div>
          <div><span @click="goPath({ path: '/aboutUs' })">关于我们</span></div>
          <div>
            <span @click="goPath({ path: '/new', query: { type: 1 } })"
              >活动资讯</span
            >
          </div>
          <div>
            <a href="mailto:linying@syy333.com" style="color: #8f90a5"
              >linying@syy333.com</a
            >
          </div>
        </div>
        <div class="foot2">
          <div style="position: relative">
            <img class="weixin" src="@/assets/img/weixin.png" alt="" />
            <img
              class="erweima"
              src="@/assets/img/contactUs/erweima1.png"
              alt=""
            />
          </div>
          <div><span @click="goPath({ path: '/joinUs' })">加入我们</span></div>
        </div>
      </div>
      <a href="https://beian.miit.gov.cn/" target="_blank" class="bah">
        ©三益友（福州）信息技术有限公司
        <img src="@/assets/img/bah.png" alt="" />闽ICP备案2020021055号
      </a>
    </div>
  </div>
</template>

<script>
/**
 *
 * @Author zzl
 * @Date 2020/11/18 15:34.
 */
import homeBg1 from "@/assets/img/homeBg.png";
import homeBg2 from "@/assets/img/homeBg2.png";

export default {
  components: {},
  props: {},
  data() {
    return {
      show: false,
      show1: false,
      show2: false,
      selectIndex: 0,
      paySelectIndex: 0,
      menuList: [
        {
          name: "首 页",
          title: "面向电商互联网服务提供商",
          des: "业务多元化 | 服务定制化 | 市场全球化",
          img: homeBg1,
        },
        {
          name: "关于我们",
          title: "关于我们",
          des: "态度正确、能力非凡、品质高尚、追求极致",
          img: homeBg2,
        },
        {
          name: "解决方案",
          title: "金融支付",
          des: "便携高效 安全支付 全方位个性服务",
          img: homeBg2,
        },
        {
          name: "新闻资讯",
          title: "新闻资讯",
          des: "我们一起去创造、发现更对",
          img: homeBg2,
        },
        {
          name: "加入我们",
          title: "加入我们",
          des: "我们在一起，就会了不起",
          img: homeBg2,
        },
        {
          name: "联系我们",
          title: "联系我们",
          des: "一起去发现更多",
          img: homeBg2,
        },
      ],
      scaleRatio: 1, // 缩放比率
    };
  },
  computed: {},
  mounted() {
    switch (this.$route.path) {
      case "/home":
        this.selectIndex = 0;
        break;
      case "/aboutUs":
        this.selectIndex = 1;
        break;
      case "/solutionPay":
        this.selectIndex = 2;
        this.paySelectIndex = 0;
        break;
      case "/internet":
        this.selectIndex = 2;
        this.paySelectIndex = 1;
        break;
      case "/outbound":
        this.selectIndex = 2;
        this.paySelectIndex = 2;
        break;
      case "/new":
        this.selectIndex = 3;
        break;
      case "/newDetail":
        this.selectIndex = 3;
        break;
      case "/joinUs":
        this.selectIndex = 4;
        break;
      case "/contactUs":
        this.selectIndex = 5;
        break;
    }

    // 设置缩放
    window.onload = () => {
      this.scaleRatio = setScale();
    };
    window.onresize = () => {
      this.scaleRatio = setScale();
    };

    function setScale() {
      // 设计稿：1920 * 1080
      // 1.设计稿尺寸
      let targetWidth = 1920;
      // 2.拿到当前设备（浏览器）的宽度
      // document.documentElement  获取html的宽度
      let currentWidth =
        document.documentElement.clientWidth || document.body.clientWidth;
      // 3.计算缩放比率(屏幕过宽，根据高度计算缩放比例)
      let scaleRatio = currentWidth / targetWidth;
      // 4.开始缩放网页
      // 宽度>1920 顶部中心缩放
      if (currentWidth > targetWidth) {
        document.body.style = `transform: scale(${scaleRatio}); transform-origin: top center;`;
      }
      // 宽度<1920 顶部靠左缩放
      else {
        document.body.style = `transform: scale(${scaleRatio}); transform-origin: top left;`;
      }
      return scaleRatio;
    }

    window.addEventListener("scroll", this.handleScroll);
  },
  methods: {
    mouseenter(index) {
      if (index == 2) {
        this.show2 = true;
      }
    },
    mouseleave(index) {
      if (index == 2) {
        setTimeout(() => {
          this.show2 = false;
        }, 1000);
      }
    },
    goPath(obj) {
      this.$router.push(obj);
      window.scrollTo(0, 0);
    },
    handleScroll() {
      var scrollTop =
        window.pageYOffset ||
        document.documentElement.scrollTop ||
        document.body.scrollTop;
      // let top = this.selectIndex == 0 ? 670 : 502;
      let top = document.documentElement.querySelector(".header").offsetHeight + document.documentElement.querySelector(".header").offsetTop;
      var headerElement = document.documentElement.querySelector(".header1");
      if (scrollTop >= top) {
        if (!this.show) {
          this.show = true;
          this.show1 = true;
        }
        headerElement.style = `top: ${scrollTop / this.scaleRatio}px`;
      } else {
        if (this.show) {
          this.show1 = false;
          setTimeout(() => {
            this.show = false;
          }, 400);
        }
      }
    },
    paySelect(index) {
      window.scrollTo(0, 0);
      this.paySelectIndex = index;
      switch (index) {
        case 0:
          this.$router.push({ path: "/solutionPay" });
          this.menuList[this.selectIndex].title = "金融支付";
          this.menuList[this.selectIndex].des =
            "便携高效 安全支付 全方位个性服务";
          break;
        case 1:
          this.$router.push({ path: "/internet" });
          this.menuList[this.selectIndex].title = "互联网";
          this.menuList[this.selectIndex].des = "大数据，打通国际物流";
          break;
        case 2:
          this.$router.push({ path: "/outbound" });
          this.menuList[this.selectIndex].title = "跨境/进出口";
          this.menuList[this.selectIndex].des =
            "降低成本，打造一站式便捷跨境物流";
          break;
      }
    },
    selectMenu(index) {
      window.scrollTo(0, 0);
      this.selectIndex = index;
      switch (index) {
        case 0:
          this.$router.push({ path: "/home" });
          break;
        case 1:
          this.$router.push({ path: "/aboutUs" });
          break;
        case 2:
          this.$router.push({ path: "/solutionPay" });
          this.paySelectIndex = 0;
          break;
        case 3:
          this.$router.push({ path: "/new" });
          break;
        case 4:
          this.$router.push({ path: "/joinUs" });
          break;
        case 5:
          this.$router.push({ path: "/contactUs" });
          break;
      }
    },
  },
  watch: {
    ["$route.path"]: function (val) {
      switch (val) {
        case "/home":
          this.selectIndex = 0;
          break;
        case "/aboutUs":
          this.selectIndex = 1;
          break;
        case "/solutionPay":
          this.selectIndex = 2;
          this.paySelectIndex = 0;
          break;
        case "/internet":
          this.selectIndex = 2;
          this.paySelectIndex = 1;
          break;
        case "/outbound":
          this.selectIndex = 2;
          this.paySelectIndex = 2;
          break;
        case "/new":
          this.selectIndex = 3;
          break;
        case "/newDetail":
          this.selectIndex = 3;
          break;
        case "/joinUs":
          this.selectIndex = 4;
          break;
        case "/contactUs":
          this.selectIndex = 5;
          break;
      }
    },
  },
  filters: {},
  beforeDestroy() {},
};
</script>

<style lang="less" scoped>
.slideUp {
  animation-name: slideUp;
  -webkit-animation-name: slideUp;
}

@keyframes slideUp {
  0% {
    transform: translateY(-100%);
  }
  100% {
    transform: translateY(0);
  }
}

.slideDown {
  animation-name: slideDown;
  -webkit-animation-name: slideDown;
}

@keyframes slideDown {
  0% {
    transform: translateY(0);
  }
  100% {
    transform: translateY(-100%);
  }
}

.index {
  width: 100%;
  min-width: 1920px;
  /*height: 100%;*/

  .main1 {
    width: 100%;
    height: 670px;
    position: relative;

    .homeBg {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
    }

    .title {
      position: absolute;
      top: 258px;
      width: 100%;
      font-size: 62px;
      font-family: Source Han Sans CN;
      font-weight: 400;
      color: #ffffff;
      text-align: center;
    }

    .des {
      position: absolute;
      top: 377px;
      width: 100%;
      font-size: 28px;
      font-family: Source Han Sans CN;
      font-weight: 400;
      color: #ffffff;
      text-align: center;
    }

    .select {
      width: 55px;
      height: 55px;
      position: absolute;
      top: 551px;
      left: calc(50% - 27px);
    }
  }

  .header {
    width: 100%;
    min-width: 1920px;
    height: 50px;
    line-height: 50px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    color: white;
    padding: 0 6%;
    box-sizing: border-box;

    .left {
      font-size: 30px;
      font-family: HuXiaoBo-NanShen;
      font-weight: 400;
      cursor: pointer;
      img {
        display: block;
      }
    }

    .right {
      position: relative;
      .li:nth-child(3):hover .program {
        display: block;
      }
      .kailong {
        width: 0;
        height: 0;
        border-right: 20px solid transparent;
        border-left: 20px solid transparent;
        border-bottom: 20px solid white;
        position: absolute;
        top: 85px;
        left: 246px;
      }

      .programActive {
        color: #fe3b35;
      }

      .program {
        position: absolute;
        top: 100px;
        left: 56px;
        width: 420px;
        height: 45px;
        line-height: 45px;
        background: #ffffff;
        border-radius: 5px;
        font-size: 18px;
        font-family: Source Han Sans CN;
        font-weight: 300;
        color: #232330;
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        cursor: pointer;
      }
    }

    .right ul {
      font-size: 20px;
      font-family: Source Han Sans CN;
      font-weight: 500;
      display: inline-flex;

      li {
        list-style: none;
        padding-left: 20px;
        padding-right: 20px;
        cursor: pointer;
        box-sizing: content-box;
        /*font-weight: bold;*/
      }

      li .active:after {
        content: "";
        display: block;
        bottom: 0;
        width: 100%;
        height: 5px;
        background: #fe3b35;
        transition: all 0.2s linear;
        -webkit-transition: all 0.2s linear;
        left: 0;
        right: 0;
        margin: auto;
      }

      li div:after {
        content: "";
        display: block;
        bottom: 0;
        width: 0%;
        height: 5px;
        background: #fe3b35;
        transition: all 0.2s linear;
        -webkit-transition: all 0.2s linear;
        left: 0;
        right: 0;
        margin: auto;
        color: #fe3b35;
      }

      li div:hover:after {
        width: 100%;
      }

      li div:hover {
        color: #fe3b35;
      }

      .active {
        color: #fe3b35;
        /*font-weight: bold;*/
        /*border-bottom: 5px solid #FE3B35;*/
      }
    }
  }

  .header1 {
    width: 100%;
    min-width: 1920px;
    color: #333333;
    height: 80px;
    z-index: 999;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    padding: 25px 6%;
    background: #fff;
    animation-duration: 0.5s;
    /* Safari and Chrome */
    -webkit-animation-duration: 0.5s;
    box-shadow: 0px 5px 10px 0px rgba(35, 35, 48, 0.05);
  }

  .foot {
    width: 100%;
    height: 390px;
    background: url("~@/assets/img/footBg.png") no-repeat;
    background-size: 100% 100%;

    .content {
      width: 100%;
      min-width: 1920px;
      margin: 0 auto;
      padding: 67px 10% 0;

      .foot1 {
        width: 100%;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        font-size: 20px;
        font-family: Source Han Sans CN;
        font-weight: 400;
        color: #333333;
        line-height: 77px;
        img {
          width: 188px;
          height: 77px;
          display: block;
        }

        div {
          width: 25%;
          span {
            cursor: pointer;
          }
        }
      }

      .foot2 {
        font-size: 16px;
        font-family: Source Han Sans CN;
        font-weight: 400;
        color: #8f90a5;
        line-height: 36px;
        display: flex;
        flex-direction: row;
        justify-content: space-between;

        div {
          width: 25%;
          span {
            cursor: pointer;
          }
        }

        .weixin {
          margin-top: 10px;
          margin-left: -10px;
          cursor: pointer;
        }

        .erweima {
          position: absolute;
          bottom: 0;
          left: 70px;
          width: 150px;
          display: none;
        }

        .weixin:hover + .erweima {
          display: block;
        }
      }
    }

    .bah {
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: center;
      color: #8997a4;
      font-size: 16px;
      font-family: Source Han Sans CN;
      font-weight: 400;

      img {
        margin-left: 66px;
        margin-right: 23px;
      }
    }
  }
}
</style>
```

### 91.PC高德地图地址定位展示

#### 91.1 效果

![image-20231023161220475](https://gitee.com/v876774538/my-img/raw/master/image-20231023161220475.png)

#### 91.2 实现

利用`iframe`在页面中嵌套网页：

```html
<iframe style="width: 690px;
height: 443px;" src="https://www.amap.com/search?query=%E4%B8%89%E7%9B%8A%E5%8F%8B(%E7%A6%8F%E5%B7%9E)%E4%BF%A1%E6%81%AF%E6%8A%80%E6%9C%AF%E6%9C%89%E9%99%90%E5%85%AC%E5%8F%B8&city=350100&geoobj=119.249042%7C26.059009%7C119.258062%7C26.064235&zoom=17.5" frameborder="0"></iframe>
```

![image-20231023161332368](https://gitee.com/v876774538/my-img/raw/master/image-20231023161332368.png)

### 92.uniapp自定义简单消息提示组件 popup

#### 92.1 组件

`tipPopup.vue`

```vue
<template>
	<view>
		<uni-popup ref="popup" type="center">
			<view class="content">
				<view class="title">
					{{ response.title }}
				</view>
				<view class="msg">
					{{ response.msg }}
				</view>
				<view class="btnGroup">
					<button class="btn" :style="{ background: getTheme }" @tap="close()">我知道了</button>
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	export default {
		name: "tipPopup",
		data() {
			return {
				response: {
					type: Object,
					default: {
						title: '',
						msg: ''
					}
				}
			};
		},
		computed: {
			getTheme() {
				return this.$store.getters.getTheme
			},
		},
		methods: {
			open(res) {
				this.response = res
				this.$refs.popup.open('center')
			},
			close() {
				this.$refs.popup.close()
			}
		}
	}
</script>

<style lang="less" scoped>
.content {
	width: 630rpx;
	background: #fff;
	border-radius: 20rpx;
	padding: 30rpx;
	box-sizing: border-box;
	display: flex;
	flex-direction: column;
	align-items: center;
	z-index: 99;
	
	.title {
		font-size: 36rpx;
		font-family: Source Han Sans CN, Source Han Sans CN;
		font-weight: 500;
		color: #333333;
		margin-bottom: 40rpx;
	}
	
	.msg {
		font-size: 28rpx;
		font-family: Source Han Sans CN, Source Han Sans CN;
		font-weight: 400;
		color: #333;
	}
	
	.btnGroup {
		margin-top: 69rpx;
		width: 100%;
		padding: 0 75rpx;
		box-sizing: border-box;
		display: flex;
		align-items: center;
		
		.btn {
			flex: 1;
			height: 80rpx;
			line-height: 80rpx;
			background: var(--theme-color);
			border-radius: 45rpx;
			font-size: 28rpx;
			font-family: Source Han Sans CN, Source Han Sans CN;
			font-weight: 500;
			color: #FFFFFF;
		}
	}
}
</style>
```

#### 92.2 使用

```html
<tip-popup ref="tipPopup"></tip-popup>
```

```js
import tipPopup from '@/components/tipPopup.vue'

export default {
    components: {
        tipPopup
    },
    methods: {
        withdraw(item) {
            if (this.type == 1) { // 账户余额提现
                this.$http('post', this.APIURL.withdraw, {
                    amount: this.amount,
                    password: item,
                    channel: this.modalType,
                    bankId: this.modalType == 'LG' ? this.userInfo.bankId : null
                }).then(res => {
                    if (!res.success) {
                        // this.utils.showToast(res.message);
                        // 提现失败弹窗
                        this.$refs.tipPopup.open({ title: '提现失败', msg: res.message })
                        return false;
                    }
                    this.utils.showToast('提现成功');
                    setTimeout(() => {
                        uni.navigateBack({
                            delta: 1
                        });
                    }, 800)
                })
        },
    }
}
```

#### 92.3 效果

![image-20231124142508276](https://gitee.com/v876774538/my-img/raw/master/image-20231124142508276.png)



### 93.uniapp下载图片（app、h5）

```js
let that = this
// #ifdef APP-PLUS
uni.downloadFile({
    url: that.shareData.imageUrl,	// 下载图片地址
    success: (res) => {
        if (res.statusCode === 200) {
            uni.saveImageToPhotosAlbum({
                filePath: res.tempFilePath,
                success: function() {
                    that.utils.showToast('保存成功')
                },
                fail: function() {
                    that.utils.showToast('保存失败')
                }
            });
        }
    }
});
// #endif
// #ifdef H5
// this.utils.showToast('h5暂不支持')
// console.log(window.location.origin, this.config.httpPath)
// if (window.location.origin == this.config.httpPath) {
// 	// var img = document.querySelector(".content")
// 	var img = document.querySelector("#qrCode")
//  html2canvas 截图
// 	html2canvas(img, {
// 		useCORS: true,
// 	}).then(canvas => {
// 		const file = document.createElement("a");
// 		file.style.display = "none";
// 		file.href = canvas.toDataURL("image/png");
// 		file.download = decodeURI('邀请分享');
// 		document.body.appendChild(file);
// 		file.click();
// 		document.body.removeChild(file);
// 	});
// }
// else {
// 	this.utils.showToast('h5暂不支持')
// }
const url = that.shareData.imageUrl; // 下载的图片地址
var xhr = new XMLHttpRequest();
xhr.open('get', url, true);
xhr.responseType = 'blob';
xhr.onload = () => {
    if (xhr.status === 200) {
        console.log(xhr)
        var blobUrl = new Blob([xhr.response]);
        const link = document.createElement('a');
        link.style.display = 'none';
        var urlObject = window.URL.createObjectURL(blobUrl);
        link.href = urlObject;
        link.download = url;
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
    }
}
xhr.onerror = () => {
    that.utils.showToast('h5暂不支持')
}
xhr.send();
// #endif
```

### 94.antd 表格选择框后添加“全选”字眼提示

#### 94.1 效果

![image-20231130165054818](https://gitee.com/v876774538/my-img/raw/master/image-20231130165054818.png)

#### 94.2 实现

利用**伪类**，在选择框后添加“全选”字眼。

```css
.ant-table-thead {
  .ant-table-selection-column {
    .ant-checkbox-wrapper::after {
      content: '全选';
      margin-left: 10px;
    }
  }
}
```

### 95.uni-app使用uni.request获取的文件流图片转base64数据

#### 95.1 参考

```js
uni.request({
    url: '', 
    data: {},
    header:  {},
    responseType: 'arraybuffer',
    success: (res) => {
        const base64 = "data:image/png;base64,"+uni.arrayBufferToBase64(res.data)
        console.log(base64)
    }
});
```

1. responseType：设置响应的数据类型为arraybuffer。
2. uni.arrayBufferToBase64将ArrayBuffer对象转成 Base64 字符串
3. 注：uni.arrayBufferToBase64支持平台分别为App、H5、微信小程序、快手小程序、京东小程序
4. 代码逻辑基础说明：使用uni.request获取服务端反馈的文件流数据（注这里的responseType必须设置为arraybuffer），使用uni.arrayBufferToBase64将获取的文件流转换成base64数据。
   转换后的base64数据需要拼接文件头：`data:image/png;base64,`

#### 95.2 项目使用

> 杉通宝项目：http://syy333.dynv6.net:20080/syy/shantongbao.git

1. 请求封装

   ```js
   function http4(method, url, data) {
   	return new Promise((resolve, reject) => {
   		if (!method) {
   			method = 'GET'
   		}
   		uni.request({
   			url: '/api/app/clientNew' + url,
   			data: data,
   			method: method,
   			header: {
   				'content-type': 'application/json',
   				// 'content-Type': 'application/x-www-form-urlencoded',
   				'Authorization': apiFilter(url) ? 'Bearer ' + uni.getStorageSync('token') : '',
   			},
   			responseType: 'arraybuffer',
   			success: (res) => {
   				if (res.data.code == '4000') {
   					this.utils.showToast("请重新登录")
   					setTimeout(() => {
   						uni.reLaunch({
   							url: '/pages/index/Login'
   						})
   					}, 800)
   					return;
   				}
   				if (res.statusCode !== 200) {
   					this.utils.showToast("抱歉，服务器出错")
   					resolve(res.data)
   					return;
   				}
   
   				resolve(res.data)
   			},
   			fail: (res) => {
   				console.log(res)
   				this.utils.showToast("网络连接错误")
   				reject(res)
   			}
   		})
   	})
   }
   ```

2. 后端返回

   ![image-20231205134845093](https://gitee.com/v876774538/my-img/raw/master/image-20231205134845093.png)

   ![image-20231205134836142](C:\Users\pc01\AppData\Roaming\Typora\typora-user-images\image-20231205134836142.png)

   ![image-20231205135318037](https://gitee.com/v876774538/my-img/raw/master/image-20231205135318037.png)

3. 前端展示

   ```html
   <view class="code" v-if="show">
       <image src="/static/oem_login_password.png" mode=""></image>
       <input v-model="filter.capText" type="text" autocomplete="off" placeholder="请输入验证码"
           placeholder-style="font-size:28upx;color:#9E9FA1;">
       <image :src="graphCode" mode="" class="graphCode" @tap="getGraphCode()"></image>
   </view>
   ```

   ```js
   // 获取图形验证码
   getGraphCode() {
       this.$http4('get', this.APIURL.getGraphCode).then((res) => {
           this.graphCode = 'data:image/png;base64,' + uni.arrayBufferToBase64(res)
           this.$forceUpdate()
       })
   },
   ```


### 96.uniapp生成推广海报

> 焕米App项目：http://syy333.dynv6.net:20080/huanmi/huanmiApp.git

#### 96.1 效果

![image-20231206175219818](https://gitee.com/v876774538/my-img/raw/master/image-20231206175219818.png)

#### 96.2 实现

```html
<!-- 推广海报 弹窗 -->
<uni-popup ref="rejectPopup" class="rejectPopup" :maskClick='false'>
    <view class="content">
        <view class="photo">
            <!-- <image class="photo" :src="fileImgPath('/static/my/invite/share-bg.png')" mode="">
            </image> -->
            <canvas class="photo" canvas-id="myCanvas" id="myCanvas"></canvas>
        </view>
        <view class="btnGroup2" v-if="btnIsShow">
            <button class="btn1" @click="close">关闭</button>
            <button class="btn1 btn2" @click="save">保存图片至相册</button>
        </view>
    </view>
</uni-popup>
```

```css
.rejectPopup {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;


    .content {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    .photo {
        margin-bottom: 40rpx;
        width: 690rpx;
        height: 952rpx;
        // background-color: pink;
        border-radius: 20rpx;
    }


    .btnGroup2 {
        display: flex;
        justify-content: center;


        .btn1 {
            font-size: 28rpx;
            width: 214rpx;
            height: 70rpx;
            text-align: center;
            line-height: 70rpx;
            border-radius: 45rpx;
            color: #FFFFFF;
            background-color: #D7D7D7;
        }

        .btn2 {
            margin-left: 40rpx;
            width: 295rpx;
            background-color: #1890FF;
            color: #fff;
        }
    }

}
```

```js
async open() {
    await this.$refs.rejectPopup.open('center')	// 打开弹窗
    await this.getImg()	// 生成图片
},
```

```js
// 生成海报图片
getImg() {
    console.log(1);
    // 获取canvas上下文
    const canvas = uni.createCanvasContext('myCanvas', this);
    canvas.width = 400;
    canvas.height = 400;

    // 加载两张图片
    // 加载第一张图片
    uni.getImageInfo({
        src: this.img1,
        success: (res1) => {
            console.log(res1,'re1')

            // 加载第二张图片
            uni.getImageInfo({
                src: this.img2,
                success: (res2) => {
                    console.log(res2, 'res2')

                    // 绘制第一张图片
                    const canvasWidth = uni.upx2px(690);
                    const canvasHeight = uni.upx2px(952);
                    const imgWidth = uni.upx2px(690);
                    const imgHeight = uni.upx2px(952);
                    const imgX = (canvasWidth - imgWidth) / 2;	// 图片坐标
                    const imgY = (canvasHeight - imgHeight) / 2;
                    // canvas.drawImage(res1.path, 0, 0, 345, 476);
                     canvas.drawImage(res1.path, imgX, imgY, imgWidth, imgHeight);
                    // 绘制第二张图片
                    const canvasWidth2 = uni.upx2px(690);
                    const canvasHeight2 = uni.upx2px(952);
                    const imgWidth2 = uni.upx2px(200);
                    const imgHeight2 = uni.upx2px(200);
                    const imgX2 = (canvasWidth2 - imgWidth2*1.2);	// 图片坐标
                    const imgY2 = (canvasHeight2 - imgHeight2*1.3);
                    // canvas.drawImage(res2.path, 217, 345, 100, 100);
                    canvas.drawImage(res2.path, imgX2, imgY2, imgWidth2, imgHeight2);

                    // 绘制完成，保存图片
                    setTimeout(()=>{
                        canvas.draw(false, () => {
                            console.log(2);
                            uni.canvasToTempFilePath({
                                canvasId: 'myCanvas',
                                success: (res) => {
                                    console.log(res
                                        .tempFilePath
                                    );
                                    uni.setStorageSync(
                                        'filePath',
                                        res
                                        .tempFilePath
                                    ) //保存临时文件路径到缓存
                                    console.log("res: ",res);
                                    this.btnIsShow = true
                                }
                            }, this);
                        });
                        this.btnIsShow = true
                    },800)
                }
            })
        }
    })

},
```

```js
// 保存图片到相册
save() {
    console.log(11111);
    let that = this
    let filePath = uni.getStorageSync('filePath') //从缓存中读取临时文件路径
    console.log("filePath: ",filePath);
    // 保存本地文件 h5不支持该方法
    uni.saveImageToPhotosAlbum({
      filePath: filePath,
      success: function() {
        uni.showToast({save
          title: "保存成功",
          icon: "none"
        });
      },
      fail: function() {
        uni.showToast({
          title: "保存失败，请稍后重试",
          icon: "none"
        });
      }
    });
},
```

### 97.uniapp携带参数返回上一页

> 参考：[uniapp返回上一页携带参数,两种方法，实测有效_uniapp返回上一页带参数-CSDN博客](https://blog.csdn.net/m0_67402235/article/details/123432105)

#### 97.1 方法1

`pre.vue`

```vue
<template>
	<view>
		<view>返回的数据为:</view>
		<view>id: {{testdata.id}}</view>
		<view>name: {{testdata.name}}</view>
		<button type="primary" @click="goNext">跳转到下一页面</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				testdata: {
					id: '',
					name: ''
				}
			}
		},
		onShow() {
			let that = this
			uni.$on('updateData',function(data){
				that.testdata = data
				const params = 'id:'+data.id+', name:'+data.name;
				console.log('监听到事件来自 updateData ，携带参数为：' + params);
			})
		},
		methods: {
			goNext() {
				uni.navigateTo({
					url: '/pages/next/next'
				})
			}
		}
	}
</script>

<style>

</style>
```

`next.vue`

```vue
<template>
	<view>
		<button type="primary" @click="goBack">点击返回上一页</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mydata: {
					id: 1,
					name: 'test'
				}
			}
		},
		methods: {
			goBack() {
				uni.$emit('updateData', this.mydata)
				uni.navigateBack({
					delta: 1
				})
			}
		}
	}
</script>

<style>

</style>
```

#### 97.2 方法2

`pre.vue`

```vue
<template>
	<view>
		<view>返回的数据为:</view>
		<view>id: {{testdata.id}}</view>
		<view>name: {{testdata.name}}</view>
		<button type="primary" @click="goNext">跳转到下一页面</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				testdata: {
					id: '',
					name: ''
				}
			}
		},
		onShow() {
			let pages = getCurrentPages();
			let currPage = pages[pages.length - 1]; //当前页面
			let json = currPage.data.testdata;
			this.testdata = json;
		},
		methods: {
			goNext() {
				uni.navigateTo({
					url: '/pages/next/next'
				})
			}
		}
	}
</script>

<style>

</style>
```

`next.vue`

```vue
<template>
	<view>
		<button type="primary" @click="goBack">点击返回上一页</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mydata: {
					id: 1,
					name: 'test'
				}
			}
		},
		methods: {
			goBack() {
				var pages = getCurrentPages();
				var prevPage = pages[pages.length - 2];
				// #ifdef H5
				prevPage.$vm.testdata = this.mydata;	// 给上一页的testdata赋值
				// #endif
				// #ifdef MP-WEIXIN
				 prevPage.setData(this.mydata);
				// #endif
				uni.navigateBack({//返回
					delta: 1
				})
			}
		}
	}
</script>

<style>

</style>

```

#### 97.3 方法2简单版

```js
let pages = getCurrentPages();  //获取所有页面栈实例列表
let nowPage = pages[ pages.length - 1];  //当前页页面实例
let prevPage = pages[ pages.length - 2 ];  //上一页页面实例
prevPage.$vm.searchVal = 1211;   //修改上一页data里面的searchVal参数值为1211
uni.navigateBack({  //uni.navigateTo跳转的返回，默认1为返回上一级
    delta: 1
})
```

> 鲸品优选项目：http://syy333.dynv6.net:20080/jpyx/trialmall-jpyx.git

```js
// 跳转
goBack(search) {
    if (!this.goIntegrated || this.goIntegrated == 'false') {
        let pages = getCurrentPages();  //获取所有页面栈实例列表
        let nowPage = pages[ pages.length - 1];  //当前页页面实例
        let prevPage = pages[ pages.length - 2 ];  //上一页页面实例
        if (prevPage.$vm.queryParams.search) {
            prevPage.$vm.queryParams.search = search;  // 将搜索的文字传给上一页
        }
        if (prevPage.$vm.goodsName) {
            prevPage.$vm.goodsName = search;
        }
        console.log(search);
        uni.navigateBack({
            delta: 1
        })
    }
    else {
        if (this.type=='联盟'){
            uni.navigateTo({
                url: '/pages/product/AlliedGoods?goodsName=' + search
                }) 
        }else if (this.type=='拼团'){
            uni.navigateTo({
                url: '/pages/groupActivities/list?goodsName=' + search
                }) 
        }else {
            uni.navigateTo({
                url: '/pages/product/Integrated?search=' + search
            })
        }

    }
},
```

### 98.uniapp下拉选择组件

> saas双钱包展业项目：http://syy333.dynv6.net:20080/xshb/sfzyAPP.git

#### 98.1 组件

![image-20231229165333607](https://gitee.com/v876774538/my-img/raw/master/image-20231229165333607.png)

#### 98.2 使用

```vue
<!-- 产品类型 -->
<w-picker mode="selector" @confirm="posConfirm" ref="selector" :themeColor="getTheme" :selectList="posTypeList"></w-picker>
```

```js
// 打开弹窗
toggleTab(str) {
    this.$refs[str].show();	// this.$refs.profession.show()
},
```

```js
// 获取产品列表
posTypeDict() {
    this.$http('get',this.APIURL.getClassificationInfo).then(res=>{
        if (!res.success) {
            this.utils.showToast(res.message);
            return false;
        }
        res.data.map(item=>{
            item.label = item.productName
            item.value = item.productCode
        })	// 数据结构
        this.posTypeList = res.data
        console.log("this.posTypeList: ",this.posTypeList);
        this.myDirect();
    })
},
```

```js
// 选择
posConfirm(val) {
    // 赋值
    this.posClassify = val.checkArr.label;
    this.filter.goodsId = val.checkArr.value;
},
```

#### 98.3 效果

![image-20231229170508680](https://gitee.com/v876774538/my-img/raw/master/image-20231229170508680.png)

### 99.uniapp消息滚动通知组件

> saas双钱包展业项目：http://syy333.dynv6.net:20080/xshb/sfzyAPP.git

#### 99.1 组件

```vue
<template>
	<view class="notice-bar">
		<scroll-view class="notice-scroll" :scroll-y="true" :scroll-with-animation="true" :scroll-top="scrollTop">
			<view class="notice-content">
				<view class="notice-item" v-for="(item, index) in noticeList" :key="index"
					@tap="handleClickNotice(item)">
					<text>{{ item.title }}</text>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		name: "noticeScroll",
		data() {
			return {
				noticeList: [], // 通知列表
				timer: null, // 定时器
				interval: 2000, // 滚动时间间隔
				scrollTop: 0, // 滚动距离
				currentIndex: 0, // 当前通知索引
			};
		},
		props: {
			notices: {
				// 外部传入的通知列表
				type: Array,
				default: [],
			},
		},
		mounted() {
			this.initNoticeList();
		},
		methods: {
			// 初始化通知列表
			initNoticeList() {
				console.log('notices', this.notices)
				const _this = this;
				_this.noticeList = _this.notices;
				if (_this.noticeList.length > 1) {
					_this.timer = setInterval(() => {
						_this.handleScrollNotice();
					}, _this.interval);
				}
			},
			// 点击通知时触发
			handleClickNotice(item) {
				this.$emit("click", item);
			},
			// 滚动通知
			handleScrollNotice() {
				const len = this.noticeList.length;
				if (this.currentIndex === len - 1) {
					this.currentIndex = 0;
				} else {
					this.currentIndex++;
				}
				this.animateScroll();
			},
			// 动画滚动
			animateScroll() {
				const _this = this;
				let noticeHeight = 24; // 通知高度，根据实际情况调整
				// 获取通知高度
				uni.createSelectorQuery().select('.noticeBar .right').boundingClientRect((res) => {
					console.log('noticeBar', res)
					if (res) {
						noticeHeight = res.height;
					}
					else {
						if (this.timer) {
							clearInterval(this.timer);
						}
					}
				}).exec()
				const scrollTop = _this.currentIndex * noticeHeight;
				_this.scrollTop = scrollTop;
			},
		},
		destroyed() {
			if (this.timer) {
				clearInterval(this.timer);
			}
		},
	};
</script>

<style scoped>
	.notice-bar {
		/* 组件高度，根据实际情况调整 */
		height: 47rpx;
		overflow: hidden;
	}

	.notice-scroll {
		width: 100%;
		height: 100%;
	}

	.notice-content {
		display: flex;
		flex-direction: column;
	}

	.notice-item {
		/* 通知高度，根据实际情况调整 */
		height: 47rpx;
		/* 通知行高，根据实际情况调整 */
		line-height: 47rpx;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}
</style>
```

#### 99.2 使用

```vue
<view class="noticeBar" @click="goPath('/pages/my/message/index')">
    <image src="@/static/index/notice-icon.png" mode="" class="left"></image>
    <view class="right">
        <view class="con">
            <notice-scroll :notices="messageList" v-if="messageList && messageList.length != 0"></notice-scroll>
        </view>
        <image class="img" src="@/static/arrow-right.png" mode=""></image>
    </view>
</view>
```

```js
// 通知
userMessage() {
    this.$http('get', this.APIURL.userMessage, {
        messageType: 0,
        pageSize: this.pageSize,
        pageNo: this.pageNo
    }).then(res => {
        if (!res.success) {
            this.utils.showToast(res.message);
            return false;
        }
        if (res.data.rows && res.data.rows.length != 0) {
            this.messageList = res.data.rows
            console.log('messageList', this.messageList)
        }
    })
},
```

#### 99.3 效果

![image-20240103152458354](https://gitee.com/v876774538/my-img/raw/master/image-20240103152458354.png)

### 100.antd修改checkbox默认样式

```css
      // 鼠标hover
      /deep/.ant-checkbox-wrapper:hover .ant-checkbox-inner,
      /deep/.ant-checkbox:hover .ant-checkbox-inner,
      /deep/.ant-checkbox-input:focus + .ant-checkbox-inner
      {
        border-radius: 50% !important;
        border: 1px solid #013893 !important;
      }

      // 默认
      /deep/.ant-checkbox {
        .ant-checkbox-inner {
          border-radius: 50% !important;
          border: 1px solid #013893 !important;
        }
      }

      // 选中
      /deep/.ant-checkbox-checked .ant-checkbox-inner,
      /deep/.ant-checkbox-indeterminate .ant-checkbox-inner {
        border-radius: 50% !important;
        border: 1px solid #013893 !important;
        background: #013893;
      }
```

![image-20240105171529217](C:\Users\pc01\AppData\Roaming\Typora\typora-user-images\image-20240105171529217.png)

![image-20240105171534985](https://gitee.com/v876774538/my-img/raw/master/image-20240105171534985.png)

注意：有未解决的样式bug如下

![image-20240105171554175](https://gitee.com/v876774538/my-img/raw/master/image-20240105171554175.png)

### 101.css磨砂质感背景

```css
.main {
  min-width: 641px;
  width: 641px;
  margin: 0 auto;
  // border: 2px solid #ffffff;
  // background: url('~@/assets/login/loginMainBg.png') no-repeat;
  background-size: 100% 100%;
  padding: 92px 0 96px;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 40px;
  border: 2px solid #fff;
  box-shadow: 0px 10px 20px 1px #dee1ff;
  overflow: hidden;
  position: relative;
}

.main::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.3);
  backdrop-filter: blur(10px);
  z-index: 0;
}
```

![image-20240105175502318](https://gitee.com/v876774538/my-img/raw/master/image-20240105175502318.png)

### 102.js全局通用的数据类型判断方法

#### 102.1 方法

```js
function getType(obj) {
  let type = typeof obj
  if (type !== 'object') {
    // 先进行typeof判断，如果是基础数据类型，直接返回
    return type
  }
  // 对于typeof返回结果是object的，再进行如下的判断，正则返回结果
  return Object.prototype.toString.call(obj).replace(/^\[object (\S+)\]$/, '$1')
}
```

#### 102.2 使用

```js
getType([]) // "Array" typeof []是object，因此toString返回
getType('123') // "string" typeof 直接返回
getType(window) // "Window" toString返回
getType(null) // "Null"首字母大写，typeof null是object，需toString来判断
getType(undefined) // "undefined" typeof 直接返回
getType() // "undefined" typeof 直接返回
getType(function () {}) // "function" typeof能判断，因此首字母小写
getType(/123/g) //"RegExp" toString返回
```

### 103.npm install失败 使用淘宝镜像

```shell
npm install --registry=https://registry.npm.taobao.org
```

### 104.uniapp scroll-view报错

报错内容：`[Intervention]Ignored attempt to cancel a touchmove event with cancelable=false, for example because scrolling is in progress and cannot be interrupted`

原因：蒙版阻止默认的修饰符与`scroll-view`组件有冲突，如下图，因为[事件冒泡](https://so.csdn.net/so/search?q=事件冒泡&spm=1001.2101.3001.7020)，导致scroll-view组件的touchmove事件可以传递到模态框。

解决方法：给`scroll-view`标签触摸移动添加阻止冒泡`@touchmove.stop`。

![img](https://img-blog.csdnimg.cn/076bd9bd805a47609bb8a94f8ee4b53a.png)

### 105.IOS h5打包成桌面书签app，页面跳转就会出现“系统网页导航栏”

#### 105.1 问题

<img src="https://gitee.com/v876774538/my-img/raw/master/image-20240123092701616.png" alt="image-20240123092701616" style="zoom:25%;" />

<img src="https://gitee.com/v876774538/my-img/raw/master/image-20240123092713381.png" alt="image-20240123092713381" style="zoom:25%;" />

#### 105.2 解决

<img src="https://gitee.com/v876774538/my-img/raw/master/image-20240123093109803.png" alt="image-20240123093109803"  />

### 106.IOS低版本系统手机的h5网页启动白屏

> 参考：
>
> [iOS端uniapp 不支持正则零宽_mob649e81593bda的技术博客_51CTO博客](https://blog.51cto.com/u_16175453/7615739)
>
> [IOS&Safari不兼容零宽断言正则的坑_ios中不兼容哪些正则-CSDN博客](https://blog.csdn.net/weixin_44846945/article/details/134314031)

#### 106.1 问题

IOS低版本系统的手机，打开h5网页白屏，开发者模式查看不报错，请求为空。

#### 106.2 解决

IOS低版本系统不支持**零宽断言**正则，注释/更改方法即可。

正则表达式零宽断言有常见四种类型：

- 正向环视(Positive Lookahead)：用`?=pattern`表示，匹配在某个模式之前的位置；
- 负向环视(Negative Lookahead)：用`?!pattern`表示，匹配不在某个模式之前的位置；
- 正向回顾(Positive Lookbehid)：用`?=<pattern`表示，匹配在某个模式之后的位置；
- 负向回顾(Negative Lookbehid)：用`?<!pattern`表示，匹配不在某个模式之后的位置。

### 107.uniapp上传图片 h5正常 app真机测试无反应

#### 107.1 uni.uploadFile(OBJECT)说明

[uni.uploadFile(OBJECT) | uni-app官网 (dcloud.net.cn)](https://uniapp.dcloud.net.cn/api/request/network-file.html#uploadfile)

**OBJECT 参数说明**

| 参数名   | 类型     | 必填                        | 说明                                                         | 平台差异说明                                                 |
| :------- | :------- | :-------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| url      | String   | 是                          | 开发者服务器 url                                             |                                                              |
| files    | Array    | 是（files和filePath选其一） | 需要上传的文件列表。**使用 files 时，filePath 和 name 不生效。** | App、H5（ 2.6.15+）                                          |
| fileType | String   | 见平台差异说明              | 文件类型，image/video/audio                                  | 仅支付宝小程序，且必填。                                     |
| file     | File     | 否                          | 要上传的文件对象。                                           | 仅H5（2.6.15+）支持                                          |
| filePath | String   | 是（files和filePath选其一） | 要上传文件资源的路径。                                       |                                                              |
| name     | String   | 是                          | 文件对应的 key , 开发者在服务器端通过这个 key 可以获取到文件二进制内容 |                                                              |
| header   | Object   | 否                          | HTTP 请求 Header, header 中不能设置 Referer。                |                                                              |
| timeout  | Number   | 否                          | 超时时间，单位 ms                                            | H5(HBuilderX 2.9.9+)、APP(HBuilderX 2.9.9+)、微信小程序、支付宝小程序、抖音小程序、快手小程序 |
| formData | Object   | 否                          | HTTP 请求中其他额外的 form data                              |                                                              |
| success  | Function | 否                          | 接口调用成功的回调函数                                       |                                                              |
| fail     | Function | 否                          | 接口调用失败的回调函数                                       |                                                              |
| complete | Function | 否                          | 接口调用结束的回调函数（调用成功、失败都会执行）             |                                                              |

**files参数说明**

files 参数是一个 file 对象的数组，file 对象的结构如下：

| 参数名 | 类型   | 必填 | 说明                                        |
| :----- | :----- | :--- | :------------------------------------------ |
| name   | String | 否   | multipart 提交时，表单的项目名，默认为 file |
| file   | File   | 否   | 要上传的文件对象，仅H5（2.6.15+）支持       |
| uri    | String | 是   | 文件的本地地址                              |

#### 107.2 解决

真机使用`files`参数上传文件时，需要填写`uri`（h5貌似不填也能用）。

```js
function uploadIdCardInfoHttp(method, url, data) {
	return new Promise((resolve, reject) => {
		if (!method) {
			method = 'GET'
		}
		let shantongbaoObj = JSON.parse(des_decrypt(uni.getStorageSync('shantongbao'), 'E555F1E8'))
		// console.log('shantongbaoObj',shantongbaoObj)
		let getTime = new Date().getTime()
		let data1 = {
			"charset": "UTF-8",
			"sign": "",
			"sessionId": shantongbaoObj.sessionId,
			"reqTime": getTime,
			"version": "1.0.0",
			// "reqData": "",
			"encType": "01",
			"systemType": "ANDROID",
			"signType": "01",
			"pubKeyVersion": "1.0.0"
		}
		let reqData = {
			"phoneInfo": {
				"appVersion": "20230111",
				"systemVersion": "12",
				"phoneModel": "HUAWEI",
				"system": "H5"
			},
			"checkValue": "1234"
		}
		let _key = shantongbaoObj.privateKey
		let reqDataVal = Object.assign({}, reqData)
		let signVal =
			`charset=UTF-8&encType=01&pubKeyVersion=1.0.0&reqTime=${getTime}&sessionId=${shantongbaoObj.sessionId}&signType=01&systemType=ANDROID&version=1.0.0&key=${_key}`
		// data1.reqData = des_encrypt(JSON.stringify(reqDataVal),_key.substr(0, 8))
		data1.sign = this.utils.SHA256(signVal).toUpperCase()
		console.log('signVal', signVal)
		console.log('data', data)
		let files = []
		for (let key in data) {
			if ((/\d/.test(key)) == false) {
				files.push({
					name: key,
					file: data[key],
					uri: data[key].path
				})
			}
			
		}
		// let files = [
		// 	{
		// 		name: 'idFroPic',
		// 		file: data.idFroPic,
		// 		uri: data.idFroPic.path,
		// 	},
		// 	{
		// 		name: 'idConPic',
		// 		file: data.idConPic,
		// 		uri: data.idConPic.path,
		// 	},
		// 	{
		// 		name: 'cardFrontPic',
		// 		file: data.cardFrontPic,
		// 		uri: data.cardFrontPic.path,
		// 	},
		// 	{
		// 		name: 'doorHeadPic',
		// 		file: data.doorHeadPic,
		// 		uri: data.doorHeadPic.path,
		// 	},
		// 	{
		// 		name: 'cashierDeskPic',
		// 		file: data.cashierDeskPic,
		// 		uri: data.cashierDeskPic.path,
		// 	},
		// 	{
		// 		name: 'indoorSettingPic',
		// 		file: data.indoorSettingPic,
		// 		uri: data.indoorSettingPic.path,
		// 	},
		// ]
		console.log('files', files)
		uni.uploadFile({
			url: config.path + url,
			formData: data1,
			name: 'file',
			method: method,
			files: files,
			timeout: 30000,
			success: (res) => {
				console.log('res', JSON.parse(res.data).respData)
				uni.hideLoading()
				if (JSON.parse(res.data).respMsg == '参数解密失败') {
					this.utils.showToast('请重新登录')
					localStorage.removeItem('userInfo')
					uni.reLaunch({
						url: '/pages/login/login'
					})
					return;
				}
				if (JSON.parse(res.data).respCode != '0000') {
					this.utils.showToast(JSON.parse(res.data).respMsg)
					resolve(JSON.parse(des_decrypt(JSON.parse(res.data).respData, _key.substr(0,
						8))))
					return;
				}
				resolve(JSON.parse(des_decrypt(JSON.parse(res.data).respData, _key.substr(0, 8))))
			},
			fail: (res) => {
				console.log('error', res)
				this.utils.showToast("网络连接错误")
				reject(res)
			},
			complete: () => {
				console.log('结束')
			}
		})
	})
}
```

`files`数组如下：

```js
[
    {
        "name": "idFroPic",
        "file": {
            "path": "file:///storage/emulated/0/Pictures/QQ/Image_1705484402858.jpg",
            "size": 76899
        },
        "uri": "file:///storage/emulated/0/Pictures/QQ/Image_1705484402858.jpg"
    },
    {
        "name": "idConPic",
        "file": {
            "path": "file:///storage/emulated/0/Pictures/QQ/Image_1705484407005.jpg",
            "size": 80320
        },
        "uri": "file:///storage/emulated/0/Pictures/QQ/Image_1705484407005.jpg"
    },
    {
        "name": "cardFrontPic",
        "file": {
            "path": "file:///storage/emulated/0/Pictures/QQ/Image_1705484397211.jpg",
            "size": 65427
        },
        "uri": "file:///storage/emulated/0/Pictures/QQ/Image_1705484397211.jpg"
    }
]
```

### 108.uniapp仿微信红包打开动画效果

[uniapp仿微信红包打开动画效果_uniapp 领红包特效-CSDN博客](https://blog.csdn.net/yezi20189/article/details/125663967)

![在这里插入图片描述](https://img-blog.csdnimg.cn/19ab52f370f941e08fa3b64d86e8c50d.gif#pic_center)

```vue
<template>
	<view class="index">
		<uni-popup ref="popup">
			<view v-if="packerState != 3" class="packer-box flex-column">
				<view class="packer-bg anim-ease-in" :class="{ 'anim-fade-out': packerState == 2 }"></view>
				<view class="packer-bottom-box anim-ease-in" :class="{ 'anim-out-bottom': packerState == 2 }">
					<view class="arc-bottom-edge"></view>
					<view class="packer-bottom-bg"></view>
				</view>
				<view class="packer-top-box anim-ease-in" :class="{ 'anim-out-top': packerState == 2 }">
					<view class="flex-row sender-info">
						<image class="sender-avatar"></image>
						<view>{{'XXX'}}发出的红包</view>
					</view>
					<view class="packer-greeting double-text">{{'恭喜发财，大吉大利'}}</view>
					<view class="arc-edge"></view>
					<view v-if="packerState == 1" class="anim-rotate packer-btn-pos">
						<view class="packer-btn" style="transform: translateZ(-4px);">開</view>
						<view class="packer-btn-middle" v-for="(item, index) in 7" :key="index"
							:style="{transform: `translateZ(${index - 3}px)`}"></view>
						<view class="packer-btn packer-btn-front">開</view>
					</view>
					<view v-else class="packer-btn packer-btn-pos" @click="openPacker">開</view>
				</view>
			</view>
			<view v-else class="packer-box flex-column">
				<!-- 红包内容 -->
			</view>
		</uni-popup>
	</view>
</template>

<script>
	export default {
		name: "redPacket",
		data() {
			return {
				packerState: 0
			};
		},
		methods: {
			open() {
				this.$refs.popup.open('center')
			},
			close() {
				this.$refs.popup.close()
			},
			openPacker() {
				// 加载数据，触发硬币旋转动画
				this.packerState = 1;
				this.request(() => {
					// 调用抢红包接口成功，触发开红包动画
					this.packerState = 2;
					// 开红包动画结束后，移除相关节点，否则会阻挡其它下层节点
					setTimeout(() => {
						this.packerState = 3;
					}, 500);
				})

			},
			request(success) {
				setTimeout(() => {
					success()
				}, 3000);
			}
		}
	}
</script>

<style lang="less">
	.flex-row {
		display: flex;
		flex-direction: row;
		position: relative;
	}

	.flex-column {
		display: flex;
		flex-direction: column;
		position: relative;
	}

	.packer-box {
		position: fixed;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		z-index: 99;
		color: rgb(235, 205, 153);
		padding: 60rpx;
	}

	.packer-bg {
		position: absolute;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
	}

	.packer-top-box {
		width: 600rpx;
		background-color: rgb(244, 94, 77);
		text-align: center;
		margin: auto;
		transform: translateY(-160rpx);
		border-top-left-radius: 30rpx;
		border-top-right-radius: 30rpx;
		position: relative;
	}

	.sender-info {
		margin-top: 200rpx;
		justify-content: center;
		line-height: 60rpx;
		font-size: 36rpx;
	}

	.sender-avatar {
		width: 60rpx;
		height: 60rpx;
		border-radius: 10rpx;
		background-color: #fff;
		margin-right: 10rpx;
	}

	.packer-greeting {
		font-size: 48rpx;
		line-height: 60rpx;
		height: 120rpx;
		margin: 40rpx 30rpx 200rpx;
	}

	.arc-edge {
		position: relative;
	}

	.arc-edge::after {
		width: 100%;
		height: 200rpx;
		position: absolute;
		left: 0;
		top: -100rpx;
		z-index: 9;
		content: '';
		border-radius: 50%;
		background-color: rgb(244, 94, 77);
		box-shadow: 0 6rpx 6rpx 0 rgba(0, 0, 0, 0.1);
	}

	.packer-bottom-box {
		transform: translate(-50%, 0);
		width: 600rpx;
		height: 360rpx;
		border-bottom-left-radius: 30rpx;
		border-bottom-right-radius: 30rpx;
		overflow: hidden;
		position: absolute;
		bottom: calc(50% - 440rpx);
		left: 50%;
	}

	.anim-ease-in {
		animation-duration: 0.5s;
		animation-timing-function: ease-in;
		animation-fill-mode: forwards;
	}

	.anim-out-top {
		animation-name: slideOutTop;
	}

	.anim-out-bottom {
		animation-name: slideOutBottom;
	}

	.anim-fade-out {
		animation-name: fadeOut;
	}

	@keyframes fadeOut {
		from {
			opacity: 1;
		}

		to {
			opacity: 0;
		}
	}

	@keyframes slideOutTop {
		from {
			transform: translateY(-160rpx);
		}

		to {
			transform: translateY(-200%);
		}
	}

	@keyframes slideOutBottom {
		from {
			transform: translate(-50%, 0);
		}

		to {
			transform: translate(-50%, 200%);
		}
	}

	.arc-bottom-edge {
		position: relative;
	}

	.arc-bottom-edge::after {
		width: 120%;
		height: 200rpx;
		position: absolute;
		left: -10%;
		top: -100rpx;
		z-index: 8;
		content: '';
		border-radius: 50%;
		box-shadow: 0 60rpx 0 0 rgb(242, 85, 66);
	}

	.packer-bottom-bg {
		background-color: rgb(242, 85, 66);
		height: 280rpx;
		margin-top: 100rpx;
	}

	.packer-btn {
		border-radius: 50%;
		width: 200rpx;
		height: 200rpx;
		line-height: 200rpx;
		font-size: 80rpx;
		text-align: center;
		color: #333;
		background-color: rgb(235, 205, 153);
		box-shadow: 0 0 6rpx 0 rgba(0, 0, 0, 0.1);
	}

	.packer-btn-pos {
		transform: translateX(-50%);
		position: absolute;
		left: 50%;
		z-index: 10;
		bottom: -200rpx;
	}

	.packer-btn-front {
		position: absolute;
		top: 0;
		transform: translateZ(4px);
	}

	.packer-btn-middle {
		position: absolute;
		top: 0;
		border-radius: 50%;
		width: 200rpx;
		height: 200rpx;
		background-color: rgb(235, 180, 120);
	}

	.anim-rotate {
		margin-left: -100rpx;
		transform-style: preserve-3d;
		animation: rotate 1s linear infinite;
	}

	@keyframes rotate {
		0% {
			transform: rotateY(0deg);
		}

		100% {
			transform: rotateY(360deg);
		}
	}
</style>
```

### 109.Promise.all 等待多个请求完成后进行操作

```js
Promise.all([
    this.$http('post', this.APIURL.userCenter).then(res => {
        console.log('res1', res)
        this.userInfo = Object.assign(this.userInfo, res)
    }),
    this.$http('post', this.APIURL.userConfig).then(res => {
        console.log('res2', res)
        this.userInfo = Object.assign(this.userInfo, res)
    }),
]).then(() => {
    uni.hideLoading()
    console.log('promise all', this.userInfo)
    uni.setStorageSync('userInfo', this.userInfo)	// 合并两个接口的用户信息
})
```

需要使用遍历的情况

```js
modalList: [{
        label: '支付宝',
        val: 'ALI',
        info: '',
        iconUrl: require('@/static/my/withdraw/alipay.png'),
        url: '/pages/my/withdrawSettings/alipay',
        isActive: false,
    },
    {
        label: '银行卡',
        val: 'LG',
        info: '',
        iconUrl: require('@/static/my/withdraw/bankcard.png'),
        url: '/pages/my/withdrawSettings/bankcard',
        isActive: false,
    },
    {
        label: '对公转账',
        val: 'DG',
        info: '',
        iconUrl: require('@/static/my/withdraw/publicTransfer.png'),
        url: '/pages/my/withdrawSettings/publicTransfer',
        isActive: false,
    },
], // 渠道列表
```

```js
// 渠道配置
modalInit() {
    var ps = []
    this.modalList.forEach((item, index) => {
        var channel = item.val
        var p = this.cashConfig(item.val, (res) => {
            console.log(item.label, res)
            if (res) {
                item.isActive = true
                this.modalFlag = false
                if (item.label == '支付宝') {
                    item.info = this.userInfo.alipayAccount ? this.userInfo
                        .alipayAccount : ''
                } else if (item.label == '银行卡') {
                    item.info = this.userInfo.bankName && this.userInfo.bankNo ?
                        `${this.userInfo.bankName}(${this.userInfo.bankNo.slice(-4)})` :
                        ''
                } else if (item.label == '对公转账') {
                    item.info = this.corporateAccount.name ? this.corporateAccount
                        .name : ''
                }
            }
        })
        ps.push(p)
    })
    console.log('ps', ps)

    Promise.all(ps).then(() => {
        console.log('flag', this.modalFlag)
        // 未开通任何渠道
        if (this.modalFlag) {
            this.utils.showToast('提现渠道未配置，请联系管理员进行配置！')
            setTimeout(() => {
                uni.navigateBack(1)
            }, 2000)
        }
    })
},
// 提现规则
cashConfig(channel, callback) {
    // 这里需要return Promise
    return this.$http('get', this.APIURL.cashConfig, {
        type: this.type == 1 ? 'balance' : 'bounty',
        channel: channel == 'ALI' ? 'ZFB' : channel
    }).then(res => {
        if (!res.success) {
            this.utils.showToast(res.message);
            return false;
        }
        if (res.data && res.data.cashStatus == 1) {
            this.rule = res.data
            this.modalType = channel
        }
        if (callback) {
            callback(res.data.cashStatus == 1 ? true : false)
        }
    })
},
```

### 110.flex: spsace-evenly兼容问题

![image-20240228101430203](https://gitee.com/v876774538/my-img/raw/master/image-20240228101430203.png)

bug说明：[【报Bug】justify-content: space-evenly在部分机型上无效 - DCloud问答](https://ask.dcloud.net.cn/question/99604)

解决方案：利用伪元素在盒子前后都增加一个空的盒子。

```css
.container{  
      display: flex;  
      flex-flow: row nowrap;  
      align-items: center;  
      justify-content: space-between;  
       //justify-content: space-evenly;  
      &:before,  
      &:after {  
          content: '';  
          display: block;  
    }  
}  
```

### 111.uniapp 安卓系统软键盘顶起页面

#### 111.1 问题描述

安卓系统软键盘顶起页面，视口宽度变化，导致通过`calc(100vh - 固定rpx)`控制最大高度的`scroll-view`高度被压缩。

#### 111.2 解决方案

[uniapp中软键盘弹起导致页面或元素挤压解决_uni-search-bar键盘会挤压页面-CSDN博客](https://blog.csdn.net/weixin_43109722/article/details/128207803)

1. `page.json`中配置不允许软键盘顶起页面

   ```js
   {
       "path" : "pages/login/login", 	//聊天页
       "style" : {
   		"app-plus": {  // 在pages.json文件里面中配置
   		    "softinputMode": "adjustPan"
   		}
   	}
   }
   ```

   试验不知道为什么不生效。

2. `input`属性`:adjust-position="false"`

   ```vue
   <input type="text" placeholder="请输入终端SN" class="input" placeholder-class="input-placeholder" v-model="keyword" :adjust-position="false">
   ```

   试验不知道为什么不生效。

3. 通过`uni.getSystemInfoSync()`获取屏幕高度，计算获得`scroll-view`的最大高度

   ```js
   function getScreenHeight() {
   	// px转rpx
   	function pxToRpx(px) {
   		const screenWidth = uni.getSystemInfoSync().screenWidth
   		return (750 * Number.parseInt(px)) / screenWidth
   	}
   
   	return pxToRpx(uni.getSystemInfoSync().windowHeight)
   }
   ```

```vue
   <scroll-view scroll-y="true" class="scroll-Y" :style="`max-height: ${(utils.getScreenHeight() - 560)}rpx`">
   	...
   </scroll-view>
```

<img src="https://gitee.com/v876774538/my-img/raw/master/51607ffcf461ab4a57a60cd78e999877.jpg" alt="img" style="zoom:50%;" />

<img src="https://gitee.com/v876774538/my-img/raw/master/750484508d0fa358d22e1e30e21b6625.jpg" alt="img" style="zoom:50%;" />

### 112.日期格式化

格式化前：

![image-20240425174737849](https://gitee.com/v876774538/my-img/raw/master/image-20240425174737849.png)

格式化后：

![image-20240425174755489](https://gitee.com/v876774538/my-img/raw/master/image-20240425174755489.png)

```js
const formatDate = (data, type = "string") => {
	console.log(data, "@@@@@@@@@");
	let regex_list = [
		// # 2013年8月15日 22:46:21
		/\d{4}-\d{1,2}-\d{1,2} \d{1,2}:\d{1,2}:\d{1,2}/g,
		// # "2013年8月15日 22:46"
		/\d{4}-\d{1,2}-\d{1,2} \d{1,2}:\d{1,2}/g,
		// # "2014年5月11日"
		/\d{4}-\d{1,2}-\d{1,2}/g,
		// # "2014年5月"
		/\d{4}-\d{1,2}/g,
	]
	let text = data.replace(/年/g, "-").replace(/月/g, "-").replace(/日/g, " ").replace("/", "-").replace(/\./g, "-");
	console.log(text, "！！！！！！！！！！")
	let date = "";
	for (let i of regex_list) {
		date = text.match(i)
		if (!validateNull(date)) {
			break
		}
	}
	if (type == "string") {
		if (!validateNull(date)) {
			return date[0]
		} else {
			return ""
		}
	} else {
		console.log(data, '@@@@@');
		if (!validateNull(date)) {
			if (date.length == 1) {
				date.push(date[0])
			}
			return date
		} else {
			return []
		}
	}
}
```

### 113.图片上传裁剪

#### 113.1 效果

![image-20250102150029729](https://gitee.com/v876774538/my-img/raw/master/image-20250102150029729.png)

#### 113.2 实现

```html
<div class="shangmi-upload ui-upload" style="position: relative;">
  <div class="upload-view upload-list" v-if="form.touXiang" v-bind:style="{backgroundImage:'url(' + form.touXiang + ')'}"></div>
  <div class="upload-view upload-list empty" v-else ></div>
  <a-button v-if="type !== 'check'" type="primary" class="ui-btn" @click="showModal">上传员工照片</a-button>
</div>
```

```html
<a-modal v-model="visible" title="更换头像" ok-text="确认" cancel-text="取消" @ok="confirmModal" :destroy-on-close='true' :mask-closable='false'>
  <div>
    <label title="上传本地照片" for="chooseImg" class="touxiang-upload">
      <input type="file" accept="image/jpg,image/jpeg,image/png" name="file" id="chooseImg" class="hidden"
        @change="selectImg($event)">
      上传本地照片
    </label>
  </div>
  <div style="width:470px;height:300px;margin: 10px auto;">
    <img id="touxiangimage" :src="url" style="max-width: 100%;" crossOrigin="Anonymous">
  </div>
  <div class="dialog-ft shangmi-upload-btn">
    <div class="dialog-button" v-if="url!==''">
      <span @click="rotateFun(1)">↻</span>
      <span @click="rotateFun(-1)">↺</span>
      <span @click="zoom(0.1)">+</span>
      <span @click="zoom(-0.1)">-</span>
    </div>
  </div>
</a-modal>
```

```js
showModal(){
  this.visible = true;
  this.url = '';
  this.cropper = '';
  this.picDeg = 0;
  this.$nextTick(() => {
    this.uploadTouXiang()
  });
},
// 上传头像
uploadTouXiang: function () {
  //初始化这个裁剪框
    let self = this;
      let image = document.getElementById('touxiangimage');
    // @ts-ignore
    this.cropper = new Cropper(image, {
      viewMode: 1,
      aspectRatio: 5 / 7,
      crop(event) {
      },
      ready: function () {
        self.croppable = true;
      }
    });
    if (this.bendipic !== '') {
      self.cropper.replace(this.bendipic);
    }
},
```

#### 113.3 完整代码

```vue
<template>
  <div class="page">
    <a-row>
      <a-col :span="16">
        <a-form-model layout="inline" class="renyuanform" ref="ruleForm" :rules="rules" :model="form" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
          <a-form-model-item label="姓名" class="form-item" prop="name">
            <a-input type="text" id="name" v-model.trim="form.name" @change="zjmShow" :disabled="type==='check'" />
          </a-form-model-item>
          <a-form-model-item label="手机号" class="form-item" prop="phonenumber" :required="isAdmin">
            <a-input  type="text" v-model.trim="form.phonenumber" :disabled="type==='check'"/>
          </a-form-model-item>
          <a-form-model-item label="艺名" class="form-item" prop="stageName">
            <a-input type="text" id="stageName" v-model.trim="form.stageName" @change="ymZjmShow" :disabled="type==='check'" />
          </a-form-model-item>
          <a-form-model-item label="证件号" class="form-item" prop="idCard">
            <a-input type="text" v-model.trim="form.idCard" :disabled="type==='check'"/>
          </a-form-model-item>
          <a-form-model-item label="助记码" class="form-item" prop="inputCode">
            <a-input type="text" id="inputCode" v-model.trim="form.inputCode" :disabled="type==='check'"/>
          </a-form-model-item>
          <a-form-model-item label="授权密码" class="form-item" v-if="type==='add'">
            <a-input type="text" v-model.trim="form.shouQuanPassword" onkeyup="this.value=this.value.replace(/[^a-zA-Z0-9]/g,'')" @change="passWordChange" :disabled="type==='check'" />
          </a-form-model-item>
           <a-form-model-item label="授权密码" class="form-item" v-else>
            <a-input type="text" v-model.trim="form.shouQuanPassword" onkeyup="this.value=this.value.replace(/[^a-zA-Z0-9]/g,'')" @change="passWordChange" :disabled="type==='check'" />
          </a-form-model-item>
          <a-form-model-item label="艺名助记码" class="form-item" prop="stageZhuJiMa">
            <a-input type="text" id="stageZhuJiMa" v-model.trim="form.stageZhuJiMa" :disabled="type==='check'" />
          </a-form-model-item>
          <a-form-model-item label="工号" class="form-item" prop="clerkJobNum">
            <a-input type="text" v-model.trim="form.clerkJobNum" :disabled="type==='check'"/>
          </a-form-model-item>
          <a-form-model-item label="信息卡到期日" class="form-item" prop="xinXiKaDaoQiShiJian">
            <a-config-provider :locale="zhCN">
              <a-date-picker v-model="form.xinXiKaDaoQiShiJian" style="width: 100%" :disabled="type==='check'" :getCalendarContainer="triggerNode => { return triggerNode.parentNode || document.body; }"/>
            </a-config-provider>
          </a-form-model-item>
          <a-form-model-item label="部门" class="form-item" prop="departmentID">
            <a-tree-select
              v-model="form.departmentID"
              style="width: 100%"
              :dropdown-style="{ maxHeight: '300px', overflow: 'auto' }"
              :tree-data="treeData"
              :replace-fields="replaceFields"
              placeholder="请选择"
              tree-default-expand-all
              :getPopupContainer="triggerNode => { return triggerNode.parentNode || document.body; }"
              :disabled="type==='check'"
            >
            </a-tree-select>
          </a-form-model-item>
          <a-form-model-item label="暂住证到期日" class="form-item" prop="zanZhuZhengDaoQiRi">
            <a-config-provider :locale="zhCN">
              <a-date-picker v-model="form.zanZhuZhengDaoQiRi" style="width: 100%" :disabled="type==='check'" :getCalendarContainer="triggerNode => { return triggerNode.parentNode || document.body; }"/>
            </a-config-provider>
          </a-form-model-item>
          <a-form-model-item label="状态" class="form-item" prop="status">
            <a-select v-model="form.status" :getPopupContainer="triggerNode => { return triggerNode.parentNode || document.body; }" disabled>
              <a-select-option :value="1">在职</a-select-option>
              <a-select-option :value="2">离职</a-select-option>
              <a-select-option :value="4" v-if="isOnShangmi">停职</a-select-option>
            </a-select>
          </a-form-model-item>
          <a-form-model-item label="员工卡号" class="form-item" prop="clerkCardNum">
            <a-input type="text" v-model.trim="form.clerkCardNum" :disabled="type==='check'"/>
          </a-form-model-item>
          <br>
          <!-- <a-form-model-item label="指纹1" class="form-item-min" :label-col="{ span: 15 }" :wrapper-col="{ span: 5 }">
            <a-button type="primary" :disabled="type==='check'">添加</a-button>
          </a-form-model-item>
          <a-form-model-item label="指纹2" class="form-item-min" :label-col="{ span: 15 }" :wrapper-col="{ span: 5 }">
            <a-button type="primary" :disabled="type==='check'">添加</a-button>
          </a-form-model-item>
          <a-form-model-item label="指纹3" class="form-item-min" :label-col="{ span: 15 }" :wrapper-col="{ span: 5 }">
            <a-button type="primary" :disabled="type==='check'">添加</a-button>
          </a-form-model-item>
          <br> -->
          <a-form-model-item class="form-item" :wrapper-col="{ span: 8, offset: 2 }">
            <a-checkbox :checked="isOnShangmi" @change="onChange('isOnShangmi',$event)" :disabled="type==='check'">添加为商秘</a-checkbox>
          </a-form-model-item>
          <br>
          <template v-if="isOnShangmi">
          <template v-for="(fangAnItem, index) in huaDangList" >
            <a-form-model-item :label="fangAnItem.typeName + '方案'" :key="fangAnItem.typeId" class="form-item"
            :rules="{ required: true, message: `${fangAnItem.typeName}方案不能为空！`, trigger: ['blur', 'change'] }">
              <a-select placeholder="请选择" v-model="huaDangFangAnIdList[index]" :disabled="type==='check'" notFoundContent='暂无数据'
              :getPopupContainer="triggerNode => { return triggerNode.parentNode || document.body; }">
                <a-select-option v-for="item in fangAnItem.listData" :key="item.id" :value="item.id">
                  {{ item.name }}
                </a-select-option>
              </a-select>
            </a-form-model-item>
          </template>
          <a-form-model-item label="考勤方案" class="form-item" prop="kaoQinFangAnId">
            <a-select placeholder="请选择" v-model="form.kaoQinFangAnId" :disabled="type==='check'" notFoundContent='暂无数据' :getPopupContainer="triggerNode => { return triggerNode.parentNode || document.body; }">
              <a-select-option v-for="item in kaoQinAdminList" :key="item.id" :value="item.id">
                {{ item.name }}
              </a-select-option>
            </a-select>
          </a-form-model-item>
          <a-form-model-item label="台票方案" class="form-item" prop="taiPiaoFangAnId">
            <a-select placeholder="请选择" notFoundContent='暂无数据' v-model="form.taiPiaoFangAnId" :disabled="type==='check'" :getPopupContainer="triggerNode => { return triggerNode.parentNode || document.body; }">
              <a-select-option v-for="item in taiPiaoAdminList" :key="item.id" :value="item.id">
                {{ item.name }}
              </a-select-option>
            </a-select>
          </a-form-model-item>
          <!-- <a-form-model-item label="特饮方案" class="form-item" prop="teYinFangAnId">
            <a-select placeholder="请选择" notFoundContent='暂无数据' v-model="form.teYinFangAnId" :disabled="type==='check'" :getPopupContainer="triggerNode => { return triggerNode.parentNode || document.body; }">
              <a-select-option v-for="item in teYinAdminList" :key="item.id" :value="item.id">
                {{ item.name }}
              </a-select-option>
            </a-select>
          </a-form-model-item> -->
          <a-form-model-item v-if="isOnShangmi" label="押金" class="form-item" prop="yaJin">
            <a-input-number v-model.trim="form.yaJin" :min="0" style="width: 100%;" :disabled="type==='check'" />
          </a-form-model-item>
          <a-form-model-item v-else label="押金" class="form-item">
            <a-input-number v-model.trim="form.yaJin" :min="0" :disabled="type==='check'"/>
          </a-form-model-item>
          <a-form-model-item label="入职日期" class="form-item" prop="riZhiRiQi" :required="isOnShangmi">
            <a-config-provider :locale="zhCN">
              <a-date-picker v-model="form.riZhiRiQi" style="width: 100%" :allow-clear=false :disabled="type==='check'" :getCalendarContainer="triggerNode => { return triggerNode.parentNode || document.body; }"/>
            </a-config-provider>
          </a-form-model-item>
          <br>
         </template>
          <a-form-model-item class="form-item" :wrapper-col="{ span: 24, offset: 2 }">
            <a-checkbox :checked="platformNeedSync" @change="onChange('platformNeedSync',$event)" :disabled="type==='check'||isOnShangmi||(form.clerk&&!!form.clerk.platformUserId)">创建APP账号
              <span class="s" v-if="form.clerk&&(form.clerk.platformUserId||form.clerk.platformUserReason)">平台id：{{!!form.clerk.platformUserId?form.clerk.platformUserId:form.clerk.platformUserReason}}</span>
            </a-checkbox>
          </a-form-model-item>
          <br>
          <a-form-model-item class="form-item" :wrapper-col="{ span: 10, offset: 2 }">
            <a-checkbox :checked="isGuaZhang" @change="onChange('isGuaZhang', $event)" :disabled="type==='check'">
              开启挂账权限
            </a-checkbox>
          </a-form-model-item>
          <br>
          <template v-if="isGuaZhang">
          <a-form-model-item label="挂账月限额" class="form-item" prop="guaZhangYueXianE">
            <a-input-number v-model.trim="form.guaZhangYueXianE" :min="0" style="width: 100%;" onkeyup="this.value=this.value.replace(/[^1-9]/D*$/,'')" :disabled="type==='check'"/>
          </a-form-model-item>
          <a-form-model-item label="挂账日限额" class="form-item" prop="guaZhangRiXianE">
            <a-input-number v-model.trim="form.guaZhangRiXianE" :min="0" style="width: 100%;" onkeyup="this.value=this.value.replace(/[^1-9]/D*$/,'')" :disabled="type==='check'"/>
          </a-form-model-item>
          <a-form-model-item v-if="isPevGuaZhang" label="挂账月余额" class="form-item">
            <a-input-number v-model="form.guaZhangYueXianEYuE" style="width: 100%;" disabled />
          </a-form-model-item>
          <a-form-model-item v-if="isPevGuaZhang" label="挂账日余额" class="form-item">
            <a-input-number v-model="form.guaZhangRiXianEYuE" style="width: 100%;" disabled />
          </a-form-model-item>
          <br>
          </template>
          <a-form-model-item class="form-item" prop="openAdmin" :wrapper-col="{ span: 10, offset: 2 }">
            <a-checkbox :checked="isAdmin" @change="onChange('isAdmin', $event)" :disabled="type==='check' || noDelete || isAdminDis">
              添加为操作员
            </a-checkbox>
          </a-form-model-item>
          <br>
          <template v-if="isAdmin">
          <a-form-model-item label="账号" class="form-item" prop="loginName">
            <a-input type="text" v-model.trim="form.loginName" :disabled="type==='check' || noDelete || isAdminDis"/>
          </a-form-model-item>
          <a-form-model-item label="密码" class="form-item" v-if="type==='add'" prop="password">
            <a-input type="text" v-model.trim="form.password" :disabled="type==='check'"/>
          </a-form-model-item>
          <a-form-model-item label="密码" class="form-item" v-else>
            <a-input type="text" v-model.trim="form.password" :disabled="type==='check'"/>
          </a-form-model-item>
          <br>
          <a-form-model-item label="分配操作员角色" style="width: 800px;" :label-col="{ span: 5}" :wrapper-col="{ span: 19 }">
            <a-transfer
              :data-source="roleListL"
              :titles="['可选角色', '已选角色']"
              :target-keys="roleTargetKeys"
              :render="item => item.title"
              :locale="locale"
              @change="handleRoleChange"
              :disabled="type==='check' || noDelete"
            />
          </a-form-model-item>
          <br>
          </template>
          <br>
          <a-form-model-item label="手机APP角色" style="width: 800px;" :label-col="{ span: 5}" :wrapper-col="{ span: 19 }">
            <a-transfer
              :data-source="baseAppRoleList"
              :titles="['可选角色', '已选角色']"
              :target-keys="appRoleTargetKeys"
              :render="item => item.title"
              :locale="locale"
              @change="handleAppRoleChange"
              :disabled="type==='check'"
            />
          </a-form-model-item>
          <br>

          <a-form-model-item
            label="分配授权权限"
            style="width: 800px;margin-top: 20px;"
            :label-col="{ span: 5}"
            :wrapper-col="{ span: 19 }"
          >
            <a-transfer
              :data-source="authorityList"
              :titles="['可选权限', '已选权限']"
              :target-keys="authorityTargetKeys"
              :render="item => item.title"
              :locale="locale"
              @change="handleAuthorityChange"
              :disabled="type==='check'"
            />
          </a-form-model-item>
          <br>
        </a-form-model>
      </a-col>
      <a-col :span="6" v-if="isOnShangmi">
        <div class="shangmi-upload ui-upload" style="position: relative;">
          <div class="upload-view upload-list" v-if="form.touXiang" v-bind:style="{backgroundImage:'url(' + form.touXiang + ')'}"></div>
          <div class="upload-view upload-list empty" v-else ></div>
          <a-button v-if="type !== 'check'" type="primary" class="ui-btn" @click="showModal">上传员工照片</a-button>
        </div>
        <div class="code" v-if="type!=='add'">
          <img :src="qrCode"/>
          <p>场所花单收款码</p>
          <a-button type="primary" @click="daochu">导出商秘收款码</a-button>
        </div>
      </a-col>
    </a-row>
    <img id="noneimage">
    <a-modal v-model="visible" title="更换头像" ok-text="确认" cancel-text="取消" @ok="confirmModal" :destroy-on-close='true' :mask-closable='false'>
      <div>
        <label title="上传本地照片" for="chooseImg" class="touxiang-upload">
          <input type="file" accept="image/jpg,image/jpeg,image/png" name="file" id="chooseImg" class="hidden"
            @change="selectImg($event)">
          上传本地照片
        </label>
      </div>
      <div style="width:470px;height:300px;margin: 10px auto;">
        <img id="touxiangimage" :src="url" style="max-width: 100%;" crossOrigin="Anonymous">
      </div>
      <div class="dialog-ft shangmi-upload-btn">
        <div class="dialog-button" v-if="url!==''">
          <span @click="rotateFun(1)">↻</span>
          <span @click="rotateFun(-1)">↺</span>
          <span @click="zoom(0.1)">+</span>
          <span @click="zoom(-0.1)">-</span>
        </div>
      </div>
    </a-modal>
    <div class="footer">
      <a-button type="primary" v-if="type!== 'check'" @click="onSubmit('save')">保存</a-button>
      <a-button type="primary" v-if="type=== 'add'" @click="onSubmit('saveAdd')">保存并新增</a-button>
      <a-button @click="goBack">返回</a-button>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import { ACCESS_TOKEN } from '@/store/mutation-types'
import { clerkInitData, addClerk, checkClerk, getDelTree, upload } from "@/api/clerk/index";
import zhCN from 'ant-design-vue/es/locale-provider/zh_CN';
import moment from 'moment';
var pinyin = require("pinyin");
var Cropper = require("cropperjs");
const token = Vue.ls.get(ACCESS_TOKEN)
export default {
  data() {
    var isPhoneNumber=(rule, value, callback)=>{
      if (!this.isAdmin && !value) {
        callback();
      }else if(this.isAdmin && !value){
        callback(new Error('手机号不能为空！'));
      }
      const re = /^((13|14|17|15|16|18|19)+\d{9})$/;
      const rsCheck = re.test(value);
      if (!rsCheck) {
        callback(new Error('请输入正确的手机号格式！'));
      } else {
        callback();
      }
		}
    return {
      zhCN,
      type:"add",
      noDelete: false,
      isAdminDis: false,
      visible: false,
      qrCode:'',
      pic: '',
      url: '',
      cropper: '',
      picDeg: 0,//裁剪旋转角度
      bendipic:'',
      form: {
        status:1,
        inputCode: '',
        stageZhuJiMa: '',
        touXiang: ''
      },
      roleListL: [],
      roleTargetKeys: [],
      baseAppRoleList:[],
      appRoleTargetKeys:[],
      authorityList: [],
      authorityTargetKeys: [],
      locale: {
        itemUnit: "项",
        itemsUnit: "项",
        notFoundContent: "列表为空",
        searchPlaceholder: "请输入搜索内容",
      },
      isOnShangmi: false,
      pevStatus: '',
      isAdmin: false,
      isGuaZhang: false,
      isPevGuaZhang: false,
      platformNeedSync:false,
      huaDangList:[],
      huaDangFangAnIdList: [],
      taiPiaoAdminList:[],
      kaoQinAdminList: [],
      teYinAdminList:[],
      treeData: [], //部门树数据
      replaceFields: {
        children:'children',
        title: 'name',
        key: 'id',
        value: 'id'
      },
      rules: {
        name: [
          { required: true, message: '姓名不能为空！', trigger: 'blur' },
          { min: 2, max: 20, message: '限制长度为2-20个字', trigger: 'blur' },
        ],
        stageName: [
          { required: true, message: '艺名不能为空！', trigger: 'blur' },
          { min: 2, max: 20, message: '限制长度为2-20个字', trigger: 'blur' },
        ],
        inputCode: [
          { required: true, message: '助记码不能为空！', trigger: ['blur', 'change'] },
          { min: 2, max: 20, message: '限制长度为2-20个字', trigger: ['blur', 'change'] },
        ],
        stageZhuJiMa: [
          { required: true, message: '艺名助记码不能为空！', trigger: ['blur', 'change'] },
          { min: 2, max: 20, message: '限制长度为2-20个字', trigger: ['blur', 'change'] },
        ],
        departmentID: [
          { required: true, message: '部门不能为空！', trigger: 'change' },
        ],
        clerkJobNum: [
          { required: true, message: '工号不能为空！', trigger: 'blur' },
        ],
        status: [
          { required: true, message: '状态不能为空！', trigger: 'change' },
        ],
        phonenumber: [
          { validator: isPhoneNumber, trigger: 'blur' }
        ],
        kaoQinFangAnId: [
          { required: true, message: '考勤方案不能为空！', trigger: 'blur' },
        ],
        taiPiaoFangAnId: [
          { required: true, message: '台票方案不能为空！', trigger: 'blur' },
        ],
        // teYinFangAnId: [
        //   { required: true, message: '特饮方案不能为空！', trigger: 'blur' },
        // ],
        yaJin: [
          { required: true, message: '押金不能为空！', trigger: 'blur' },
        ],
        riZhiRiQi: [
          { required: true, message: '入职日期不能为空！', trigger: 'change' },
        ],
        guaZhangRiXianE: [
          { required: true, message: '挂账日限额不能为空！', trigger: 'blur' },
        ],
        guaZhangYueXianE: [
          { required: true, message: '挂账月限额不能为空！', trigger: 'blur' },
        ],
        loginName: [
          { required: true, message: '账号不能为空！', trigger: 'blur' },
        ],
        password: [
          { required: true, message: '密码不能为空！', trigger: 'blur' },
        ],
      },
    };
  },
  created() {
    this.type = this.$route.query.type;
    if(this.type === 'edit'){
      this.noDelete = this.$route.query.noDelete==='1' ? true : false;
    }
    this.getPageData();
    getDelTree().then((res) => {
      if (res.errorCode === 1) {
        this.handleData(res.result);
      } else {
        this.$message.error(res.errorMsg);
      }
    });
  },
  components: {},
  methods: {
    moment,
    //自动生成助记码
    zjmShow: function(){
        let name = pinyin(this.form.name, {
          style: pinyin.STYLE_FIRST_LETTER, // 设置拼音风格(首字母)
          // heteronym: true
        });
        this.form.inputCode = name.join('');
        document.getElementById('inputCode').focus();
        document.getElementById('name').focus();
    },
    ymZjmShow() {
      let ymname = pinyin(this.form.stageName, {
        style: pinyin.STYLE_FIRST_LETTER, // 设置拼音风格(首字母)
        // heteronym: true
      });
      this.form.stageZhuJiMa = ymname.join('');
      document.getElementById('stageZhuJiMa').focus();
      document.getElementById('stageName').focus();
    },
    passWordChange(){
      this.form.shouQuanPassword =  this.form.shouQuanPassword .replace(/[^a-zA-Z0-9]/g,'')
    },
    //部门树数据重构
    handleData(data) {
      let result = [];
      if (!Array.isArray(data)) {
          return result
      }
      let map = {};
      data.forEach(item => {
          map = Object.assign({},item.department);
          if (item.sub) {
              map.children = [];
              map.children = this.handleSub(item.sub);
          }
          result.push(map);
      });
      this.treeData = result;
    },
    //部门树子级数据重构
    handleSub(sub, mapSub = []) {
      sub.forEach((item,index) => {
          mapSub.push(item.department);
          if (item.sub) {
              mapSub[index].children = [];
              this.handleSub(item.sub, mapSub[index].children);
          }
      });
      return mapSub;
    },
    callBcak(res){
      return new Promise((resolve, reject) => {
        res.result.baseRoleList.forEach((item) => {
          item.title = item.name;
          item.key = item.id.toString();
        });

        res.result.baseConfirmauthorityList.forEach((item) => {
          item.title = item.name;
          item.key = item.id.toString();
        });
        res.result.baseAppRoleList.forEach((item) => {
          item.title = item.name;
          item.key = item.id.toString();
        });
        this.roleListL = res.result.baseRoleList;
        this.baseAppRoleList = res.result.baseAppRoleList;
        this.authorityList = res.result.baseConfirmauthorityList;
        this.huaDangList = res.result.huaDangList;
        this.taiPiaoAdminList = res.result.taiPiaoAdminList;
        this.teYinAdminList = res.result.teYinAdminList;
        this.kaoQinAdminList = res.result.kaoQinAdminList;
        resolve()
      })
    },
    getPageData() {
      let _this=this;
        if(this.$route.query.id){
          let paramData = {
            data:{id: this.$route.query.id}
          }
          checkClerk(paramData).then((res) => {
            _this.callBcak(res).then(()=>{
              this.form = Object.assign({}, res.result,{
                id: res.result.clerk.id,
                name: res.result.clerk.name,
                phonenumber: res.result.clerk.phonenumber,
                stageName: res.result.clerk.stageName,
                idCard: res.result.clerk.idCard,
                inputCode: res.result.clerk.inputCode,
                stageZhuJiMa: res.result.clerk.stageZhuJiMa,
                clerkJobNum: res.result.clerk.clerkJobNum,
                departmentID: res.result.clerk.departmentID,
                xinXiKaDaoQiShiJian: res.result.clerk.xinXiKaDaoQiShiJian && this.moment(res.result.clerk.xinXiKaDaoQiShiJian).format("YYYY-MM-DD"),
                zanZhuZhengDaoQiRi: res.result.clerk.zanZhuZhengDaoQiRi && this.moment(res.result.clerk.zanZhuZhengDaoQiRi).format("YYYY-MM-DD"),
                clerkCardNum: res.result.clerk.clerkCardNum,
                isShangMi: res.result.clerk.isShangMi,
                status: res.result.clerk.status,
                fingerprint1: res.result.clerk.fingerprint1,
                fingerprint2: res.result.clerk.fingerprint2,
                fingerprint3: res.result.clerk.fingerprint3,

                //huaDangFangAnStr: huaDangFangAnStr.slice(1),
                riZhiRiQi: res.result.riZhiRiQi && this.moment(res.result.riZhiRiQi).format("YYYY-MM-DD"),
                kaoQinFangAnId: res.result.kaoQinFangAnId,
                // teYinFangAnId: res.result.teYinFangAnId,
                taiPiaoFangAnId: res.result.taiPiaoFangAnId,
                touXiang: res.result.touXiang,
                yaJin: res.result.yaJin,

                canGuaZhangFlag: res.result.canGuaZhangFlag,
                guaZhangRiXianE: res.result.guaZhangRiXianE,
                guaZhangYueXianE: res.result.guaZhangYueXianE,
                guaZhangRiXianEYuE: res.result.guaZhangRiXianEYuE,
                guaZhangYueXianEYuE: res.result.guaZhangYueXianEYuE,

                openAdmin: res.result.openAdmin,
                hadAdminData: res.result.hadAdminData,
                shouQuanPassword: res.result.shouQuanPassword,
                loginName: res.result.loginName,
                // password: res.result.clerk.password,

              // roleIdList: res.result.selectRoleList,
              // confirmAuthorityList: res.result.authorityTargetKeys
              });
              this.isOnShangmi = res.result.isShangMi ===1 ? true : false;
              this.platformNeedSync= res.result.clerk.platformNeedSync ===1? true : false;
              this.isGuaZhang = res.result.canGuaZhangFlag ===1 ? true : false;
              this.isAdmin = res.result.openAdmin ===1 ? true : false;
              this.appRoleTargetKeys=!!res.result.clerk.rolesid?res.result.clerk.rolesid.split(','):[];
              _this.authorityTargetKeys=res.result.selectConfirmauthorityList.map(item =>item.id.toString())||[];
              _this.roleTargetKeys=res.result.selectRoleList.map(item =>item.id.toString())||[];
              this.huaDangFangAnIdList = [];
              res.result.huaDangList.map(item =>
                this.huaDangFangAnIdList.push(item.selectTypeValueId)
              );
              //原来开启添加商秘，则另存原状态
              this.pevStatus = this.isOnShangmi ? res.result.clerk.status :'';
              //原来有挂账权限，则另存原内容
              this.isPevGuaZhang = this.isGuaZhang;
              if(this.type==="edit" && res.result.openAdmin ===1){
                this.isAdminDis = true
              }
              _this.qrCode= res.result.qrCode;
            })
          })
        }else{
          clerkInitData().then((res) => {
            if (res.errorCode === 1) {
              _this.callBcak(res)
            } else {
              this.$message.error(res.errorMsg);
              this.goBack();
            }
          });
        }
    },
    onChange(type,e){
      if(type === 'isOnShangmi'){
        this.isOnShangmi = e.target.checked;
        if(e.target.checked){
          this.platformNeedSync =true;
          this.form.riZhiRiQi = null;
           this.$nextTick(function () {
             if(!this.appRoleTargetKeys.includes('-1')){
               this.appRoleTargetKeys.push('-1')
             }
            this.form = Object.assign({},this.form,{
              riZhiRiQi: this.moment().format("YYYY-MM-DD")
            },)
          });
          if(this.pevStatus){
            this.form.status = this.pevStatus;
          }
        }else{
          this.platformNeedSync =false;
          this.form.riZhiRiQi = '';
          this.form.status = this.form.status===4 ? '' :this.form.status;
        }
      }else if(type === 'isGuaZhang'){
        this.isGuaZhang = e.target.checked;
      }else if(type === 'platformNeedSync'){
        this.platformNeedSync = e.target.checked;
      }else{
        this.isAdmin = e.target.checked;
      }
    },
    showModal(){
      this.visible = true;
      this.url = '';
      this.cropper = '';
      this.picDeg = 0;
      this.$nextTick(() => {
        this.uploadTouXiang()
      });
    },
    // 上传头像
    uploadTouXiang: function () {
      //初始化这个裁剪框
        let self = this;
          let image = document.getElementById('touxiangimage');
        // @ts-ignore
        this.cropper = new Cropper(image, {
          viewMode: 1,
          aspectRatio: 5 / 7,
          crop(event) {
          },
          ready: function () {
            self.croppable = true;
          }
        });
        if (this.bendipic !== '') {
          self.cropper.replace(this.bendipic);
        }
    },
    //图片旋转
    rotateFun(num) {
      num === 1 ? this.picDeg += 45 : this.picDeg -= 45
      this.cropper.rotateTo(this.picDeg);
    },
    // 图片放大
    zoom(num) {
      this.cropper.zoom(num);
    },
    getObjectURL(file) {
      var url = null;
      if (window.createObjectURL != undefined) { // basic
        url = window.createObjectURL(file);
      } else if (window.URL != undefined) { // mozilla(firefox)
        url = window.URL.createObjectURL(file);
      } else if (window.webkitURL != undefined) { // webkit or chrome
        url = window.webkitURL.createObjectURL(file);
      }
      return url;
    },
    selectImg: function (file) {
      file = file.target.files;
      if (file[0].size/1024/1024>1){
        this.$message.info('文件上传过大,请选择小于1M得文件上传！');
        return false;
      }
      if (!file.length) return
      this.url = this.getObjectURL(file[0]);
      this.bendipic = this.url;
      //每次替换图片要重新得到新的url
      if (this.cropper) {
        this.cropper.replace(this.url);
      }
    },
    getRoundedCanvas: function (sourceCanvas) {
      var canvas = document.createElement('canvas');
      var context = canvas.getContext('2d');
      var width = sourceCanvas.width;
      var height = sourceCanvas.height;
      canvas.width = width;
      canvas.height = height;
      context.imageSmoothingEnabled = true;
      context.drawImage(sourceCanvas, 0, 0, width, height);
      context.globalCompositeOperation = 'destination-in';
      context.beginPath();
      // 下行代码改变图片变成圆形
      // context.arc(width / 2, height / 2, Math.min(width, height) / 2, 0, 2 * Math.PI, true);
      context.fill();
      return canvas;
    },
    postImg: function (url) {
      //这里对base64串进行操作，去掉url头，并转换为byte
      let bytes = window.atob(url.split(',')[1]);
      let array = [];
      for (let i = 0; i < bytes.length; i++) {
        array.push(bytes.charCodeAt(i));
      }
      let blob = new Blob([new Uint8Array(array)], { type: 'image/jpeg' });
      let formData = new FormData();
      formData.append('file', blob, Date.now() + '.jpg');
      formData.append('session',token)
      return new Promise((resolve, reject) => {
        let config = {
            headers: {'Content-Type': 'multipart/form-data'},
        };  //添加请求头
        axios.post(process.env.VUE_APP_API_BASE_URL+'base/file/upload', formData, config).then(res => {
          resolve(res);
          this.form.touXiang = res.data.result.thumbUrl;
          this.pic = res.data.result.url;
        })
      });
    },
    confirmModal() {
      let croppedCanvas;
      let roundedCanvas;
      if (!this.croppable) {
        return;
      }
      // Crop
      croppedCanvas = this.cropper.getCroppedCanvas();
      console.log(this.cropper)
      // Round
      roundedCanvas = this.getRoundedCanvas(croppedCanvas);
      this.headerImage = roundedCanvas.toDataURL();
      this.postImg(this.headerImage);
      this.hideModal();
    },
    hideModal() {
      this.visible = false;
    },
    goBack() {
      this.$router.go(-1);
    },
    handleAppRoleChange(nextTargetKeys, direction, moveKeys) {
      this.appRoleTargetKeys = nextTargetKeys;
    },
    handleRoleChange(nextTargetKeys, direction, moveKeys) {
      this.roleTargetKeys = nextTargetKeys;
    },
    handleAuthorityChange(nextTargetKeys, direction, moveKeys) {
      this.authorityTargetKeys = nextTargetKeys;
    },
    onSubmit(type) {
      this.$refs.ruleForm.validate(valid => {
        if (!valid) {
          return false;
        }else{
          let huaDangFangAnStr = '';
          this.huaDangList.forEach((item,index)=>{
            huaDangFangAnStr += ','+item.typeId+'-'+this.huaDangFangAnIdList[index];
          })
          this.huaDangFangAnIdList
          const updata = {
            data: Object.assign({},{
              flag: this.type === 'add' ? 'add' : 'editor',
              clerk: {
                id: this.$route.query.id ||'',
                platformNeedSync:this.platformNeedSync ? 1 : 0,
                name: this.form.name,
                phonenumber: this.form.phonenumber,
                stageName: this.form.stageName,
                idCard: this.form.idCard,
                inputCode: this.form.inputCode,
                stageZhuJiMa: this.form.stageZhuJiMa,
                clerkJobNum: this.form.clerkJobNum,
                departmentID: this.form.departmentID,
                xinXiKaDaoQiShiJian: this.form.xinXiKaDaoQiShiJian && this.moment(this.form.xinXiKaDaoQiShiJian).format("YYYY-MM-DD"),
                zanZhuZhengDaoQiRi: this.form.zanZhuZhengDaoQiRi && this.moment(this.form.zanZhuZhengDaoQiRi).format("YYYY-MM-DD"),
                clerkCardNum: this.form.clerkCardNum,
                isShangMi: this.isOnShangmi ? 1 : 0,
                status: this.form.status,
                fingerprint1: '',
                fingerprint2: '',
                fingerprint3: '',
                rolesid:this.appRoleTargetKeys.toString()
              },
              shangMiParam: {
                huaDangFangAnStr: this.isOnShangmi ? huaDangFangAnStr.slice(1) : '',
                riZhiRiQi: this.isOnShangmi ? this.form.riZhiRiQi && this.moment(this.form.riZhiRiQi).format("YYYY-MM-DD") : '',
                kaoQinFangAnId: this.isOnShangmi ? this.form.kaoQinFangAnId : '',
                // teYinFangAnId: this.isOnShangmi ? this.form.teYinFangAnId : '',
                taiPiaoFangAnId: this.isOnShangmi ? this.form.taiPiaoFangAnId : '',
                touXiang: this.form.touXiang,
                yaJin: this.isOnShangmi ? this.form.yaJin : '',
              },
              authorityInfo: {
                canGuaZhangFlag: this.isGuaZhang ? 1 : 0,
                guaZhangRiXianE: this.isGuaZhang ? this.form.guaZhangRiXianE : '',
                guaZhangYueXianE: this.isGuaZhang ? this.form.guaZhangYueXianE : '',
              },
              authorityinfoParam: {
                openAdmin: this.isAdmin ? 1 : 0,
                hadAdminData: this.form.hadAdminData || 0,
                shouQuanPassword: this.form.shouQuanPassword,
              },
              user: {
                id: this.form.userId ||'',
                loginName: this.isAdmin ? this.form.loginName : '',
                password: this.isAdmin ? this.form.password : '',
              },
              roleIdList: this.isAdmin ? this.roleTargetKeys : [],
              confirmAuthorityList: this.authorityTargetKeys
            })
          }
          addClerk(updata).then((res) => {
            if (res.errorCode === 1) {
              this.$message.success('人员保存成功！');
              if(type==='save'){
                this.$router.go(-1);
              }else{
                this.$refs.ruleForm.resetFields();
                this.form.touXiang = '';
                this.isOnShangmi = false;
                this.isGuaZhang = false;
                this.isAdmin = false;
                this.huaDangFangAnIdList = [];
                this.roleTargetKeys = [];
                this.authorityTargetKeys =[];
              }
            } else {
              this.$message.error(res.errorMsg)
            }
          })
        }
      });
    },
    daochu(){
      let image = new Image();
      // 解决跨域 Canvas 污染问题
      image.setAttribute("crossOrigin", "anonymous");
      image.onload = function() {
        let canvas = document.createElement("canvas");
        canvas.width = image.width;
        canvas.height = image.height;
        let context = canvas.getContext("2d");
        context.drawImage(image, 0, 0, image.width, image.height);
        let url = canvas.toDataURL("image/png"); //得到图片的base64编码数据
        let a = document.createElement("a"); // 生成一个a元素
        let event = new MouseEvent("click"); // 创建一个单击事件
        a.download = name || "photo"; // 设置图片名称
        a.href =url; // 将生成的URL设置为a.href属性
        a.dispatchEvent(event); // 触发a的单击事件
      };
      image.src = this.form.qrCode;
    },
  }
};
</script>

<style lang="scss">
.ant-col-6 .code{text-align: center;}
.s{margin-left: 5px;color: red;}
.renyuanform {
  max-width: 1200px;
  min-width: 900px;
  padding-left: 20px;
  .form-item {
    width: 40%;
    margin-bottom: 15px;
  }
  .form-item-min{
    width: 15%;
    margin-bottom: 15px;
  }
}
.footer {
  margin-top: 30px;
  text-align: center;
  .ant-btn {
    margin-right: 15px;
  }
}
.shangmi-upload {
  position: relative;
}

.shangmi-upload > input {
  position: absolute;
  top: -999em;
  left: -999em;
  opacity: 0;
}

.upload-view {
    background: center no-repeat;
    overflow: hidden;
    width: 210px;
    height: 300px;
    background-color: #EBEBEB;
    display: flex;
    justify-content: center;
    align-items: center;
    border: 1px solid #AAAAAA;
    background-size: cover;
    background-position: center;
    margin: 0 auto;
}
.upload-view.empty::after {
  width: 98px;
  height: 152px;
  content: '';
  background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 98 152"><image width="98" height="152" xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGIAAACYCAYAAAAfrDxxAAAACXBIWXMAAAsSAAALEgHS3X78AAAWGklEQVR4Xu2deXxU5bnHv+fMktkySxYgbEYJssiiVFS0QrUfoq1Le/3crvfaa23T6+1tb71ttXWpn9al/bj31lKVVuBTF1zSKotSUVBRDBABQUC2hIQEAmSdyUwyyZzl/jEMJjDJmTlzZknS758zz8yceX/nfZ73fd7nfY+gqiq5zp9/01AYCsjjWpsinlBAsne0SJaOVkmIhBWhJ6wAkGcXsdpE1VtkVr1Fll6n29RdPNba4XSbGm6+e7xf4yeyjpCLQtz1zf3iuLNt5zTV90zYtz3k7GiJCFqfGYyisVZlygXOYOEYS/3KZ07Ur22em3N/OqeEWPpAo/toXc/M7RsCvkCblFLjD0RRiVWddVl+S+Foy86KX0/o0rLPFDkhxPOPHvXu2hy8YMcHAZcUycz15NlELljg7pg+17Xtmz8pCWnZp5usCvHMfY2Wxprw3I/W+Qtjvj7TON0mLrzS06QqbLv7mUnZuQiyKMRTdx+eWPWPjplN9T2ilm0mOGe6Q76o3LP15rvGH9eyTQcZF+L+79UIiqJe/OGajmJFzuxva2GxClx2ja/xzsWTtmvZGk1GhVj6QGPejo2dC/ZUB/O0bLPJhVd4gtMudL5/4+3jJC1bo8iYEEseaHRtfL19fsOBsEnLNheYMscZueiLnvU33j6uV8vWCMxaBkaw5IFG1/sr2xccqQ3nRDxIhH3bQhZV4UogI2KkvWFeePyo7YPVQ0uEGPs/Dlm2rPNfuWFlW9p7cVob59mHjojVb/sXNB4ceiLE2LctZPn4/c7LtOxSJa0NVLO7+9LdW4JWLbtc5x8vNHs2v9UxWcsuFdImxKI76suq1rT7tOyGAlKvyvsr26cAbi1bvaRFiGW/PWLbsKJ9aoYGZBlhw8o2IdylzAHSkgNLixA1u7oubm9OLWOaa4S7FA7sCOUDZ2vZ6sFwIZbc3zhmy7qOtHXhbFK3txtgCmDTME0aw4XYtTk4S81a6iy9hAIyROdekzRMk8ZQIRbdUT9m16bOnE5fpILLc2o6UQoYOho0VIgjNT3TtWyGMqMnnrrHROCcQUyTxjAhnr6nwb5jY8CpZTdUMVsFZlyc3/elCRg4gjJMiM52aUqkdxiNV0/j8mt92J39mssGFA1gnjSGCVG/v3uMls1QRRDhaz8qiffW2Hgv6sEQIZ761WFLza4ui5bdUOW6746ibKYj3lvF8V7UgyFChLuUs6Rh6pbKZjmo+PWEgd62A4bERUOECAXkUVo2Q5GxpXnc++xk8myDNlPhYG8miiFCtBztNeSuyCXOnmbnkRVTKRqrOV3oN5TSizFCNEU0r3YoMf/6Av7vH9MTEQEMck2GLJW2Hu81RNBs4yk08+OHzmL+9QVapn1xaRkkQspCPPGLevtQD9R5NpEbbhnN139cgtOd9KpoQt1Gi5SFQE0tE2m2CvxLxWjWLm/B35ax6hUACsdYuO67o7j2plG4C3Q3he4P9iXlL5EiakpJvrlXeqj49QRuunM81W938O5rbVSv88cynYbjKTRz8UIvV9xQwAXz3YimlLMUAtFYm1LOOWUh7E4xpQu44obo6M9iFbj0yz4u/bIPWVL5dGuIXZs62bs1SM2ubo439Gh805mIJoExE61MnuVk2oUuZlziYvIsJ0IORrSUhejtUXXX/AgiXHjFmWtIJrPAjItdzLj4szjYHVI4friHE0d68bdE6OyQCQU+c2UWq4jVLuItNOMpNFM8zsrYUhtma8p3vBYqKfYGMEAIQST5W/Uk58524vImdgl2p0jpNDul0+xappnGkMCWcif98YNndZvM+u66WZcaMhfKNro9Ql9SFgKgqMSqq2tOnm3IXCjbBLUMEsEQIQrHWHTdFWWz4mY0hxqG7DYySoikL0YQYczElEa+uUKnlkEiGCJEvs98QsvmdIpKrJgt+mJLjtGqZZAIhggBHE52mOgtGhbrSN3kkmu69dHS3rKZjqTihI6cTi7SrGWQKIYIATD2bFtSmwAdLsN+Opsc0TJIFMNaw1tk3mvNS/zresJDO2MLhDEoPoCBQtxy38TwjEtcCe/k783SvmoDaSCa3jAEw4QAKJ1q361lE6OjJaJlksvIQK2WUTIYKsQt9088Nn2uK6xlB9B+YugKIUXUwxiU2ohhqBAA0+e6Pkkkxx/0y7QNQTG6gzLfuXDn6PLi6tFatslguBA/+M2EY3PmuwNadgCHdiccUnKGpb89QsvRXgdwUXlx9SXlxdWGZC4NFwLgnBmOzb5ii2Yg27XZkHxZxjj4SRerlvZLIhQDC8qLq2eUF1enNENNixDfv2d8eN7V3n1adtveS6jj5AQ93QoP/rAWWTrj/hKIbuf6YnlxdWl5cbW2X45DWoQAuPWx0gPzrva2DWazd2uQ5iOGxry08cTt9dRHt24NhAWYSbSHJF0TmzYhAMpmOqqmzHEO2NKqCuteMWxOlDbWPNfM2hdbtMxi5AOXlBdXzy0vrk54wSWtQtx4+zhlznz3exPPtQ9YkrFy6QlyuS7K39bDyqXHtMziMQb4Qnlx9fTy4mrN9eCMnE6jdSjKTx4p5Zr/SLo3p51IJEJnZyeKorL+5QAvPtZG0K8rI9AD7AUaBjrYMSNCQFSMqjUd8+v3dZ+RdvUUmlm6aWbChQSZICZC3/YJBRRefKyNdS8H0Llz1g/sXts89wx/nDEhAJ596Ih1+4bAgl2bg2dUB171rSJ+9oe07CVPmnA4TCg08DJD3Z4eltzbyoGPE0oixOMo8Ona5rmnJlIZFQLgxScOeVqOctnqpa2m04+Su+2PZ7PwG4ZtS0saVVUJhUL09CRWIbThtU5eeLgNf6uuqkQFqAEOrG2eK2dMiBXL6s15NuFzsy93jLLaBA7uiPD0nc001nx2V5ktAvcvP5c5CzJ/cIEkSQSDQWQ5uUbtDiq88kQ7a58LIOs7ozAsCMLejAjx2pL6qeddYptUMNrcL1hHelXeWBLk1adaOXW0tE3k7iWTuHihN+53GY2qqnR1dREO63YzADQe7GXpva3s2TLoXOMMBEEMOuxOIa1CvLTo0JjJ59vOP2uqddDpv79F4bWnArz9cjtSr4ogws13jedr/z3GiCLhuKiqSjgcpru7GyPboOqNIM892Ebbca0CQCFst9kliyXPBUTSIsTyPxxyjim1zJ05z56fTMFvoFXl7ReDrK/soLUpwtTPOfmfh0sH2tGpC1mW6enpIRwOGypAX3rCKq/+qZ3Xl/qJc7KzbLXkBW02u6fPfnljhXj20VpTwWjzBbMvt5fYU1iTVhX4dEsvH63rZus7nZTNdPCV74/m/M+7dVVyy7JMJBKhp6cHSdK6U43j2OEIy+5rZcf70cGRyWT2O+xOlyCIpw/hjRPilSfrJs+8zH5u8TizjqYanJajMrWfSHS2K5ScZaOoJA9PoRmX24y7IOr1VFVFVVUURUGWZRRFQZIkJElCUfQN+o1i+7u90qKf+iWTyTzQpp5IyjOo5x6vLZ4823bBlV/PT1vZXtFYE0Vj+95EvUAvERVaczhVZbFYcDqd2G2dZpMpNGhb6xZi2YM1tnGTrHPLv+326q0GH66YTCYcDgdWa3R73aq/aKf7kxZi8W8OCqMmWM6/4l/zx7m8aRrSDFEEQcBut2O3f7aHIxSIcHCHdqo/KSGW/+FQ6bxrXNPHnm0ZFmV6RpKXl4fD4UAU+4fInVWJLQcnJMRfH6ktOPs865zyf3Pn3HadbGM2m3E6nZjN8Zty9V8Se7zRoEKUF1eb5n3ZNeM/f1s8Mc/2Ty/UF1EUcTgc5OUNPEbpCkrs26rtlmAQIcqLq8cB06veCNqO1UX4zp2FTL0wpS3VwwJBELDZbNjtdgRh8Jtz9+bEC8XPmEeUF1d7gRlAv1OMBQEu+ZKLb/+8gKKxCXm0YYfVasXpdJ4RBwbinm81sGdzQpnczyZ05cXVNmAaMH6wT1htAtfe7OX6H3gZKe7KbDbjcDiwWBKvmAl3Sfz7jDotsxgRYWHRFpHoOaaTgYRHQwWjzXzr5wV8/jpDzgTJSURRxG63Y7Ml75K3bwjwwE0Jb6SKiPmKMg+YShIiALQdl1h02wnu+cYRanYm1P2GFDabDa/Xq0sEgNVLtCdxfRELFKVgvCQFraqqqzUP7OjhV984wpO/bKb9RHKLKrmIxWLB6/XidDo1g/FAhLsldmxIbn1DBDCBq0SW80bLst+k4zgDVY0uG/706gZee7qDSI8xicRMYjKZcLvduN1uTKaknMMZ7N+W3OIQnFbXZFNVz3hJUnyKEtBzL4S7FF56vI2fX9PA5jcTH7plE0EQcDqdeL3epILxYKz5a3JuCeIXmJndiuKeIEndTlXV1ZonGiV+/5Pj3HvjUer3JjahyQapxoF49IZlqt9KsUf0RQB7kSw7x0lSp1XVdwLNp9Vh7rihkT/f00ygLXfih8ViwePxJDUnSJR92xPLLZ2O5lWYIb9Eli2jZNkv6okfCqx/uZP/vaqB1Uv88aqpM4YoiuTn5+N2uwfMDaXKW8uTd0uQgBAnEeyq6pkgSbJXUXT9UlenwvMPtXLbtY1se0ffXaMXQRBwOBx4vd5TawTpINIr8+Hq5N0SJC5EDIvnZPxwqKqu1myqi/Dwfx3jd99vovGgLo+XFHl5eXi93oRyQ6lyYIeuJgGSFwIAEezFsuwYK8sBi6rq2gi384NufvmVIyy7v5VQIGmPp4nZbMbj8eByuQyPAwPx5nP6z0dJ6QotquoeK8um4mj8SNr5y7LKm8/5uXXhYd58PoBiQDwXRRGXy4XH40lbHIiHFFH4cHWGe8RpiI5o/Ih4dMaPoF9h2X0t/OIrjezcqM/HAtjtdrxe76BrBOmiZlcXqRTEGCFEDKs3Gj9CdlXV1ZqNB3v53feaeOSHxzhWn7jHs1qteL1eHA5H2uPAQLy1XL9bAjDNsX1vipZRMghgdaqqxaGqgbAgmBQh+ZKwpkMR1r3USTikUjY7D8sARxCZTCby8/Ox2+0ZiwPxkCIKj/3oRCo9Qknb1VtV1T1OlsUiWfYLOuKHFFFZ9UwHt17VwDuvdPb7k+lIS6RC3b5uUq1hS5sQJxGdJ+OHW1F09d1Aq8ziXzVzxw2N7Nsaxmaz4fP5DE1LpMq6F3X9tX6kWwgg6q58ipI/QZJCNlVNLj98ksN7I12P3BLoMol5WYsD8ZAlhXUvp75xPyNCxBDBOVqWbSXRdHui1cCRPKstkO/yOkQsjlXPtGvZZ5S6vd0oif6TQcioEDGs0XS7UKgo/kHubdVstvjzXV5TXp791BaiV37vJ9SZ+Igq3Wx4NXW3BFkS4iQml6J4JkhS2KUo/fq2KIqdLqc74rC7PMJpoy5Fgb//KTd6hSwrvPlc6m4JsisEAALYChXFNV6SgnnQabc7Qy6nJ18UTQNm51Y8HSDQnv48lRaH93cjGdQ5sy5EDBO4CkSzZDFbEzo2Yfmjgx7zkRHe+7sxvQFySIhkeeuFIO3NuuodDEFRVNY+/08hAFh2f/Z2qTTWdNNr4EmdQ1qIjau6aGnKTq9471XjegMMcSEAnr7LsMOIE0ZRVNYsM2bYGmPIC7H93TBH63Qle3XTVB821C3BMBAC4Ok7Ez7UyhDeX2Fsb4BhIsTuTT3U79O/OpYMqqLy+pJ/CjEgT/4yM72i6XCY7qCxbgmGkRAHd/RyYIeuwsSk2LQmPb8xbIQAePKOlrSdrwEQ6WhlxWJdy/KaDCshDu+N8OlHxo7vAZTeMPIbi2ld+iQhfWf6aTKshABYdFsrimJMr1AVBWn7OsSHb8T00Ro21c3S+ohuMlf4kyGOH5b45MMgsz+f2pHdUsM+TH9/FLM/OmFUTRZWvVem8Sn9DDshAJ74WQuLP3TpOnRLDrQhrHgC86GP+73e7JyBP5C+utlhKURHs8xH6wNctNCjZXoKJdKL+u6LmKpejfv+pvr0uSUYpkIALLq9lc9V52PSOD5KVVXkXR9gXvVHkOIvNqmimZXvnBv3PaMYtkKE/Aob3/Az//p++/b7IR2twfS3RzC3D37kdJtrGh1pdEswjIUAWHxnG5d+yYPZ0r9XyEE/wupFmPdXD/DJ/mxunK1lkjLDbvjal3CXyrpXPis0UKQI8rsvYXrsu4gJiqCKZla8M1XLLGWGdY8AWHZvB1/4aj6mwx9jfu1x6E2uvq3dNYXW9rRXl6vDXohIr8rau9dwnXeZlmlcth5L72gJaAL2DHshAJ5dNZ2FPxyPrbNRy7Q/osir66dpWeklAOyqrC1rhWEeI2IossCqmqu0zM6g3TWVEy2GH9rWC+wENsREgBEiBMAra6YQcif3WITtJ2ZqmSRD7HT89ZW1ZfWVtWX9EmIjRghFFfjbniR6hSCw4j3D3NJx4N3K2rI9lbVlcWsDR4wQACvfnkTAndgM2Z9/LkeaEio6HIxOYFNlbdmWytqyQVeURpQQAMu3JdYrtp1IaRIXAXYB71XWliVU7zMiRk19eeuDiXx9znR8gT2DWAm8vlGXW1KBemDvQC5oIEacEABLN17NT2cOLESnexJ1DUkfkdcM7K6sLdNV4jEihfhwawk3Xjqb4s4dcd//uPX8uK8PQAjYU1lbputhdTFGXIyIsXj91fR5kEYfBFZsOC/O62cgAXuIjoZSEgFGaI8A2L67iKNXzGVscEu/10Pu0kTc0mGiccCwCugR2yMAnl77RU5/RMvOjkHdUhvRGfEOI0WAEdwjAHbvL6Bu4TxKQxtPvTaAW+omGgeOxnvTCEZ0jwB46vUrUMXo/Rhyl3Kwrt86t0z0GaPvpFMEiPaIY0SfNDsiOVjn4aD1ciaH32FPoF/KuxH4tLK2LLkFDJ2If26fVw1sIjodH5E8uWo+qjmPVRtnALQDH1TWlm3PlAjQ57T8Cl+VAJxF9HjqrJw00mu1tYec+QOv9qeRm776ibzstZk7K2vLkly0MIYzHltQ4auyAFOAUuIPtNNGloQ49fDWytoyA85Q08eAz6Gr8FW5gPOAUXEN0kAWhDhKNA5kZpfLIGg+ELDCVzWaqCAp54S1yKAQfqJ5oeztDz4NTSEAKnxVIlFXdS5pjB8ZEOLUI+9PXyHLNgkJEaPCV2UlGswnkob4kUYhFOAQsL+ytsyAQ32MJykhYlT4qtxEn0NUqGWbDGkS4hjRWXF69lwZhC4hYlT4qkqA6YAhzzk2WIhOonEgoRWybJOSEHAqfkwCykgxd2WQEBGiceCMSolcJmUhYlT4qmxE48cELduBSFEIFagD9iW7TJkLGCZEjApfVdzn2CVCCkKktEyZCxguRIwKX9U4ovEj4XNBdQgRIirAcS3DXCdtQgBU+KpMRGNHGQmk3JMQQgL2AXWVtWXp2W+bYdIqRIwKX5Wd6FMfxw1ml4AQKtFlyn1Gr5Blm4wIEaPCV1VANH7E3WWoIUQr0erp9Gz9zzIZFQJOpdvHE+0h/XaADCBEF9EJWRPDmIwLEaPCV2Um+nzUczgZP04TQgYOADXDJQ4MRtaEiFHhq3IQze6O6SNEA9FylYytkGWbrAsRo8JXVdSTZy/pcrgaKmvLOrTshxv/D+QnT5d323nyAAAAAElFTkSuQmCC" style="opacity:0.30000001192092896;isolation:isolate"/></svg>') no-repeat center;
  background-size: contain;
  margin-right: 10px;
}

.shangmi-upload > button {
  margin: 30px auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
.upload-button::before{
  content: '';
  width: 17px;
  height: 14px;
  display: inline-block;
  background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 17 14"><path d="M15.3,2A1.72,1.72,0,0,1,17,3.77v8.5A1.72,1.72,0,0,1,15.3,14H1.7A1.72,1.72,0,0,1,0,12.27V3.77A1.72,1.72,0,0,1,1.7,2H3.5A1.93,1.93,0,0,1,5.2,0h6.6a1.93,1.93,0,0,1,1.7,2ZM5.2.89A1.08,1.08,0,0,0,4.37,2h8.25A1.07,1.07,0,0,0,11.79.89ZM16.12,12.27V3.77a.84.84,0,0,0-.83-.84H1.7a.84.84,0,0,0-.83.84h0v8.5a.84.84,0,0,0,.83.84H15.3a.84.84,0,0,0,.83-.84h0ZM12.31,7.89A3.81,3.81,0,1,1,8.5,4a3.85,3.85,0,0,1,3.81,3.88Zm-3.81,3a3,3,0,1,0-2.94-3v0a3,3,0,0,0,2.94,3Z" style="fill:#fff"/></svg>') no-repeat center;
  background-size: contain;
  margin-right: 10px;
}
.shangmi-upload-btn { border-left: none; border-right: none; border-bottom: none; }
.shangmi-upload-btn span { border: 1px solid #96c; font-size: 18px; margin: .0 1rem 0 0; color: #96c; width: 2rem; text-align: center; height: 2rem; line-height: 2rem; display: inline-block; cursor: pointer; }
.touxiang-upload { background-color: #9966cc; border-color: #714998; color: #fff; padding:6px 10px; margin-bottom: 10rem;}
.touxiang-upload input { opacity: 0; position: absolute; width: inherit;left: 0;}
/* 头像上传 */
.cropper-container {
  direction: ltr;
  font-size: 0;
  line-height: 0;
  position: relative;
  -ms-touch-action: none;
  touch-action: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.cropper-container img {
  display: block;
  height: 100%;
  image-orientation: 0deg;
  max-height: none !important;
  max-width: none !important;
  min-height: 0 !important;
  min-width: 0 !important;
  width: 100%;
}

.cropper-wrap-box,
.cropper-canvas,
.cropper-drag-box,
.cropper-crop-box,
.cropper-modal {
  bottom: 0;
  left: 0;
  position: absolute;
  right: 0;
  top: 0;
}

.cropper-wrap-box,
.cropper-canvas {
  overflow: hidden;
}

.cropper-drag-box {
  background-color: #fff;
  opacity: 0;
}

.cropper-modal {
  background-color: #000;
  opacity: 0.5;
}

.cropper-view-box {
  display: block;
  height: 100%;
  outline: 1px solid #39f;
  outline-color: rgba(51, 153, 255, 0.75);
  overflow: hidden;
  width: 100%;
}

.cropper-dashed {
  border: 0 dashed #eee;
  display: block;
  opacity: 0.5;
  position: absolute;
}

.cropper-dashed.dashed-h {
  border-bottom-width: 1px;
  border-top-width: 1px;
  height: calc(100% / 3);
  left: 0;
  top: calc(100% / 3);
  width: 100%;
}

.cropper-dashed.dashed-v {
  border-left-width: 1px;
  border-right-width: 1px;
  height: 100%;
  left: calc(100% / 3);
  top: 0;
  width: calc(100% / 3);
}

.cropper-center {
  display: block;
  height: 0;
  left: 50%;
  opacity: 0.75;
  position: absolute;
  top: 50%;
  width: 0;
}

.cropper-center::before,
.cropper-center::after {
  background-color: #eee;
  content: ' ';
  display: block;
  position: absolute;
}

.cropper-center::before {
  height: 1px;
  left: -3px;
  top: 0;
  width: 7px;
}

.cropper-center::after {
  height: 7px;
  left: 0;
  top: -3px;
  width: 1px;
}

.cropper-face,
.cropper-line,
.cropper-point {
  display: block;
  height: 100%;
  opacity: 0.1;
  position: absolute;
  width: 100%;
}

.cropper-face {
  background-color: #fff;
  left: 0;
  top: 0;
}

.cropper-line {
  background-color: #39f;
}

.cropper-line.line-e {
  cursor: ew-resize;
  right: -3px;
  top: 0;
  width: 5px;
}

.cropper-line.line-n {
  cursor: ns-resize;
  height: 5px;
  left: 0;
  top: -3px;
}

.cropper-line.line-w {
  cursor: ew-resize;
  left: -3px;
  top: 0;
  width: 5px;
}

.cropper-line.line-s {
  bottom: -3px;
  cursor: ns-resize;
  height: 5px;
  left: 0;
}

.cropper-point {
  background-color: #39f;
  height: 5px;
  opacity: 0.75;
  width: 5px;
}

.cropper-point.point-e {
  cursor: ew-resize;
  margin-top: -3px;
  right: -3px;
  top: 50%;
}

.cropper-point.point-n {
  cursor: ns-resize;
  left: 50%;
  margin-left: -3px;
  top: -3px;
}

.cropper-point.point-w {
  cursor: ew-resize;
  left: -3px;
  margin-top: -3px;
  top: 50%;
}

.cropper-point.point-s {
  bottom: -3px;
  cursor: s-resize;
  left: 50%;
  margin-left: -3px;
}

.cropper-point.point-ne {
  cursor: nesw-resize;
  right: -3px;
  top: -3px;
}

.cropper-point.point-nw {
  cursor: nwse-resize;
  left: -3px;
  top: -3px;
}

.cropper-point.point-sw {
  bottom: -3px;
  cursor: nesw-resize;
  left: -3px;
}

.cropper-point.point-se {
  bottom: -3px;
  cursor: nwse-resize;
  height: 20px;
  opacity: 1;
  right: -3px;
  width: 20px;
}

@media (min-width: 768px) {
  .cropper-point.point-se {
    height: 15px;
    width: 15px;
  }
}

@media (min-width: 992px) {
  .cropper-point.point-se {
    height: 10px;
    width: 10px;
  }
}

@media (min-width: 1200px) {
  .cropper-point.point-se {
    height: 5px;
    opacity: 0.75;
    width: 5px;
  }
}

.cropper-point.point-se::before {
  background-color: #39f;
  bottom: -50%;
  content: ' ';
  display: block;
  height: 200%;
  opacity: 0;
  position: absolute;
  right: -50%;
  width: 200%;
}

.cropper-invisible {opacity: 0;}
.cropper-bg {
  background-image: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQAQMAAAAlPW0iAAAAA3NCSVQICAjb4U/gAAAABlBMVEXMzMz////TjRV2AAAACXBIWXMAAArrAAAK6wGCiw1aAAAAHHRFWHRTb2Z0d2FyZQBBZG9iZSBGaXJld29ya3MgQ1M26LyyjAAAABFJREFUCJlj+M/AgBVhF/0PAH6/D/HkDxOGAAAAAElFTkSuQmCC');
}
.cropper-hide {display: block;height: 0;position: absolute;width: 0;}
.cropper-hidden {display: none !important;}
.cropper-move {cursor: move;}
.cropper-crop {cursor: crosshair;}
.cropper-disabled .cropper-drag-box,
.cropper-disabled .cropper-face,
.cropper-disabled .cropper-line,
.cropper-disabled .cropper-point {
  cursor: not-allowed;
}
</style>

```

### 114.flex布局 space-between 一行三个 不足三个补齐

![image-20250220105127308](https://gitee.com/v876774538/my-img/raw/master/image-20250220105127308.png)

![image-20250220105359968](https://gitee.com/v876774538/my-img/raw/master/image-20250220105359968.png)

效果：

![image-20250220105447007](https://gitee.com/v876774538/my-img/raw/master/image-20250220105447007.png)

完整代码：

```vue
<!-- 选择续费方式 -->
<cmp-popup show="{{ isShowRecharge }}" locked="{{ locked }}" content-align="bottom">
  <view class="equity-popup-container">
    <view class="equity-header">
      <text>选择续费方式</text>
      <view class="icon cuIcon-close" bind:tap="closeRechargePopup"></view>
    </view>
    <view class="equity-content">
      <view class="equity-box" wx:for="{{ currentRightInfo.payment_set.sub }}" wx:key="index" wx:for-item="item" bind:tap="handleMemberLevelPay" data-type="{{ item.type}}">
        <view class="equity-border">
          <view class="price">
            <text>￥</text>
            <text class="em">
              {{ currentRightInfo.pay_type == '1' ? item.open_fee : item.renew_fee }}
            </text>
          </view>
          <view class="name">{{ tools.subTypeFilter(item.type) }}卡</view>
          <view class="btn">{{ currentRightInfo.pay_type == '1' ? '去开通' : '去续费' }}</view>
        </view>
      </view>
    </view>
  </view>
</cmp-popup>
```

```less
.equity-popup-container {
  background: #fff;
  border-radius: 24rpx 24rpx 0 0;
  overflow: hidden;

  .equity-header {
    height: 120rpx;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: PingFangSC, PingFang SC;
    font-weight: 500;
    font-size: 32rpx;
    color: #333333;
    line-height: 32rpx;
    position: relative;

    .icon {
      font-size: 32rpx;
      color: #333;
      position: absolute;
      right: 24rpx;
    }
  }

  .equity-content {
    padding: 0 32rpx 99rpx;
    box-sizing: border-box;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;

    .equity-box {
      width: 210rpx;
      height: 240rpx;
      background: linear-gradient(46deg, #e2a964 0%, #f1cd98 49%, #e1a662 100%);
      border-radius: 10rpx;
      padding: 5rpx;
      box-sizing: border-box;

      .equity-border {
        height: 100%;
        border: 1px solid #fff;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding-top: 34rpx;
        border-radius: 10rpx;

        .price {
          font-family: PingFangSC, PingFang SC;
          font-weight: 600;
          font-size: 24rpx;
          line-height: 23rpx;
          color: #513327;
          margin-bottom: 12rpx;

          .em {
            font-size: 54rpx;
            display: inline-block;
          }
        }

        .name {
          font-family: PingFangSC, PingFang SC;
          font-weight: 400;
          font-size: 32rpx;
          color: #513327;
          line-height: 48rpx;
          margin-bottom: 21rpx;
        }

        .btn {
          width: 130rpx;
          height: 44rpx;
          line-height: 44rpx;
          text-align: center;
          background: linear-gradient(142deg, #613b28 0%, #2f1e17 100%);
          border-radius: 10rpx;
          font-family: PingFangSC, PingFang SC;
          font-weight: 600;
          font-size: 28rpx;
          color: #eabc8e;
        }
      }
    }

    &:after {
      content:"";
      width:210rpx; // 这里的宽度，更改为自己子元素的宽度
    }
  }
}
```

### 115.微信小程序使用canvas

在微信小程序中，**Canvas**组件提供了一个强大的绘图界面，可以在其上进行任意绘制。Canvas组件支持两种类型：**2D**和**WebGL**。以下是如何在微信小程序中使用Canvas的详细步骤。

基础使用

#### 115.1 在WXML中添加Canvas组件

首先需要在WXML文件中添加Canvas组件，并指定其类型和唯一标识符。例如：

```html
<canvas id="myCanvas" type="2d" style="border: 1px solid; width: 300px; height: 150px;"></canvas>
```

在这里，我们指定了id为*myCanvas*，类型为*2d*。

#### 115.2 获取Canvas对象和渲染上下文

在JavaScript文件中，通过*wx.createSelectorQuery()*选择Canvas组件，并获取Canvas对象和渲染上下文：

```js
wx.createSelectorQuery()
.select('#myCanvas')
.fields({ node: true, size: true })
.exec((res) => {
	const canvas = res[0].node;
	const ctx = canvas.getContext('2d');
});
```

通过*Canvas.getContext*方法，我们可以获取到渲染上下文*RenderingContext*。

#### 115.3 初始化Canvas

初始化Canvas的宽高，并根据设备的像素比进行缩放：

```js
wx.createSelectorQuery()
.select('#myCanvas')
.fields({ node: true, size: true })
.exec((res) => {
    const canvas = res[0].node;
    const ctx = canvas.getContext('2d');
    const dpr = wx.getSystemInfoSync().pixelRatio;
    canvas.width = res[0].width * dpr;
    canvas.height = res[0].height * dpr;
    ctx.scale(dpr, dpr);
});
```

#### 115.4 进行绘制

在Canvas上进行绘制操作，例如绘制一个红色的矩形：

```js
ctx.clearRect(0, 0, width, height);
ctx.fillStyle = 'rgb(200, 0, 0)';
ctx.fillRect(10, 10, 50, 50);
```

**进阶使用**

绘制图片

可以通过*Canvas.createImage*方法创建图片对象，并在图片加载完成后将其绘制到Canvas上：

```js
const image = canvas.createImage();
image.onload = () => {
	ctx.drawImage(image, 0, 0);
};
image.src = 'https://example.com/image.png';
```

生成图片

通过*wx.canvasToTempFilePath*接口，可以将Canvas上的内容生成图片临时文件：

```js
wx.canvasToTempFilePath({
	canvas,
	success: res => {
		const tempFilePath = res.tempFilePath;
	},
});
```

帧动画

通过*Canvas.requestAnimationFrame*方法，可以注册动画帧回调，在回调内进行动画的逐帧绘制：

```js
const startTime = Date.now();
	const draw = () => {
	const time = Date.now();
	const elapsed = time - startTime;
	const x = (width - 50) * (elapsed % 2000) / 2000;	
	ctx.clearRect(0, 0, width, height);
	ctx.fillStyle = 'rgb(200, 0, 0)';
	ctx.fillRect(x, height / 2 - 25, 50, 50);
	canvas.requestAnimationFrame(draw);
};

draw();
```

#### 115.6 项目应用

![image-20250225110242151](https://gitee.com/v876774538/my-img/raw/master/image-20250225110242151.png)

```js
// 重新生成二维码 覆盖门店logo到二维码中央
createQrcode() {
  this.getRoomInfo(); // 获取房间信息

  const storeLogo = this.data.roomInfo.store_logo
    ? this.data.roomInfo.store_logo
    : ""; // 门店logourl
  const qrcode = this.data.qrcodeData.qrcode; // 原二维码

  wx.createSelectorQuery()
    .in(this)
    .select("#myCanvas")
    .fields({ node: true, size: true })
    .exec((res) => {
      // 初始化canvas
      const canvas = res[0].node;
      const ctx = canvas.getContext("2d");

      // 设置canvas宽高
      canvas.width = 430;
      canvas.height = 430;

      // 绘制
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.beginPath();

      // 加载背景
      const bg = canvas.createImage();
      bg.src = qrcode;
      bg.onload = () => {
        ctx.drawImage(bg, 0, 0, canvas.width, canvas.height);

        // 加载logo
        const logo = canvas.createImage();
        logo.src = storeLogo;
        logo.onload = () => {
          ctx.drawImage(logo, 167, 167, 100, 100);

          // canvas转图片
          wx.canvasToTempFilePath(
            {
              canvas,
              fileType: "png",
              quality: 1,
              success: (res) => {
                this.setData({
                  qrcodeUrl: res.tempFilePath,
                });
              },
            },
            this
          );
        };
      };
    });
},
```

完整代码：

`index.wxml`

```html
<!-- components/enterpriseWechat/index.wxml -->
<cmp-popup show="{{ show }}" locked="{{ true }}" content-align="center">
    <view class="enterprise-wechat-container">
        <view class="enterprise-wechat-main" wx:if="{{ qrcodeData.qrcode_bg }}" style="{{ qrcodeData.qrcode_bg ? 'background: url(' + qrcodeData.qrcode_bg + ') no-repeat; background-size: 100% 100%;' : ''}}">
            <view class="enterprise-wechat-title"></view>
            <!-- <image class="enterprise-wechat-qrcode" src="{{ qrcodeData.qrcode }}" show-menu-by-longpress="{{ true }}"></image> -->
            <image class="enterprise-wechat-qrcode" src="{{ qrcodeUrl }}" show-menu-by-longpress="{{ true }}"></image>
            <view class="enterprise-wechat-desc"></view>
        </view>
        <view class="enterprise-wechat-main" wx:else>
            <view class="enterprise-wechat-title">
                <span>长按识别二维码</span>
            </view>
            <image class="enterprise-wechat-qrcode" src="{{ qrcodeData.qrcode }}" show-menu-by-longpress="{{ true }}"></image>
            <view class="enterprise-wechat-desc">
                <span>①添加好友</span>
                <span>②点击链接下单</span>
            </view>
        </view>
        <view class="enterprise-wechat-close">
            <image class="close-icon" catch:tap="handleClose" src="{{ iconClose }}" />
        </view>
    </view>
    <canvas type="2d" id="myCanvas" class="myCanvas"></canvas>
</cmp-popup>
```

`index.js`

```index.js
// components/enterpriseWechat/index.js
import { getQrcodeContactMe } from "../../http/api/roomServe";

let app = getApp();

Component({
  /**
   * 组件的属性列表
   */
  properties: {
    roomId: {
      type: String,
      value: "",
    },
  },

  /**
   * 组件的初始数据
   */
  data: {
    show: false,
    iconClose: "",
    qrcodeData: {},
    roomInfo: {},

    qrcodeUrl: "", // 生成qrcode
  },
  lifetimes: {
    attached: function () {
      this.setData({
        iconClose: app.getIconUrl("wx-channel/icon_close_w@2x"),
      });
    },
  },

  /**
   * 组件的方法列表
   */
  methods: {
    // 获取房台信息
    getRoomInfo() {
      if (wx.getStorageSync("roomInfo")) {
        this.setData({
          roomInfo: wx.getStorageSync("roomInfo"),
        });
      }
    },
    getContactMeQrcode() {
      getQrcodeContactMe({ roomId: this.data.roomId })
        .then((res) => {
          if (res.code == 0) {
            this.setData({
              qrcodeData: res.data,
            });
            this.handleOpen();
            // 生成二维码
            this.createQrcode();
          } else {
            this.handleTriggerEvent("continue");
          }
        })
        .catch((err) => {
          this.handleTriggerEvent("continue");
        });
    },
    // 重新生成二维码 覆盖门店logo到二维码中央
    createQrcode() {
      this.getRoomInfo(); // 获取房间信息

      const storeLogo = this.data.roomInfo.store_logo
        ? this.data.roomInfo.store_logo
        : ""; // 门店logourl
      const qrcode = this.data.qrcodeData.qrcode; // 原二维码

      wx.createSelectorQuery()
        .in(this)
        .select("#myCanvas")
        .fields({ node: true, size: true })
        .exec((res) => {
          // 初始化canvas
          const canvas = res[0].node;
          const ctx = canvas.getContext("2d");

          // 设置canvas宽高
          canvas.width = 430;
          canvas.height = 430;

          // 绘制
          ctx.clearRect(0, 0, canvas.width, canvas.height);
          ctx.beginPath();

          // 加载背景
          const bg = canvas.createImage();
          bg.src = qrcode;
          bg.onload = () => {
            ctx.drawImage(bg, 0, 0, canvas.width, canvas.height);

            // 加载logo
            const logo = canvas.createImage();
            logo.src = storeLogo;
            logo.onload = () => {
              ctx.drawImage(logo, 167, 167, 100, 100);

              // canvas转图片
              wx.canvasToTempFilePath(
                {
                  canvas,
                  fileType: "png",
                  quality: 1,
                  success: (res) => {
                    this.setData({
                      qrcodeUrl: res.tempFilePath,
                    });
                  },
                },
                this
              );
            };
          };
        });
    },
    handleOpen() {
      this.setData({ show: true });
    },
    handleClose() {
      this.setData({ show: false });
    },
    handleTriggerEvent(event, data) {
      this.triggerEvent(event, data);
    },
  },
});

```

`index.less`

```less
.enterprise-wechat-container {
  display: flex;
  flex-direction: column;
  align-items: center;

  .enterprise-wechat-main {
    width: 600rpx;
    height: 720rpx;
    background: url("data:image/png;base64,................")
      no-repeat;
    background-size: 100% 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 40rpx 0 45rpx;
    box-sizing: border-box;
    border-radius: 45rpx;
    overflow: hidden;

    .enterprise-wechat-title {
      font-family: PingFangSC, PingFang SC;
      font-weight: 500;
      font-size: 45rpx;
      color: #351400;
      line-height: 63rpx;
      min-height: 63rpx;
      margin-bottom: 47rpx;
    }

    .enterprise-wechat-qrcode {
      width: 430rpx;
      height: 430rpx;
      margin-bottom: 50rpx;
    }

    .enterprise-wechat-desc {
      font-family: PingFangSC, PingFang SC;
      font-weight: 600;
      font-size: 32rpx;
      color: #ffffff;
      line-height: 45rpx;
      min-height: 45rpx;
      width: 430rpx;
      display: flex;
      justify-content: space-between;
    }
  }

  .enterprise-wechat-close {
    margin-top: 70rpx;

    .close-icon {
      width: 48rpx;
      height: 48rpx;
    }
  }
}

.myCanvas {
  position: absolute;
  top: 0;
  width: 430rpx;
  height: 430rpx;
  overflow:hidden;
  opacity: 0;
  visibility: hidden;
  display: none;
  z-index: -1000;
  transform: scaleY(0)
}

```

### 116.vue后台 前端根据文本生成二维码

```vue
<template>
    <div class="qrcode-main">
        <!-- 生成二维码 -->
        <div class="qrcode-box" v-show="showCode">
            <img src="@/assets/logo.png" alt="" v-show="false" ref="logoImg">
            <div class="qrcode-canvas">
                <canvas ref="qrcodeCanvas"></canvas>
            </div>
        </div>
    </div>
</template>

<script>
import QRCode from "qrcode"

export default {
    data() {
        return {
            showCode: false,    //是否显示二维码
            link:'', // 存放小程序二维码信息
        }
    },
    created() {
        this.generateQrcode();
    },
    methods: {
        // 图片转canvas,
        imgToCanvas() {
            const canvas = document.createElement('canvas');
            const { logoImg } = this.$refs;
            const ctx = canvas.getContext('2d');
            ctx.fillStyle = '#FFFFFF';
            ctx.fillRect(0, 0, 80, 80);		//先画一个80*80的正方形，颜色#ffffff，此处因为logo图片四周没有留白
            ctx.drawImage(logoImg, 4, 4, 64, 64);		//将 64*64 的 logoImg 画到 canvas 上
            return canvas;
        },
        // 生成的logo canvas与二维码canvas合并
        mergeCanvas(generateCanvas) {		//生成的二维码 canvas	
            const { qrcodeCanvas } = this.$refs;
            const logoCavans = this.imgToCanvas();		//第2步里面的转换后的canvas
            const canvas = document.createElement('canvas');
            canvas.width = generateCanvas.width;
            canvas.height = generateCanvas.height;
            canvas.getContext('2d').drawImage(generateCanvas, 0, 0);	//将 generateCanvas 画到 canvas 上，坐标 0，0
            canvas.getContext('2d').drawImage(logoCavans, 160, 160);	//将 logoCavans 画到 canvas 上，坐标 80，80
            qrcodeCanvas.width = canvas.width;
            qrcodeCanvas.height = canvas.height;
            qrcodeCanvas.getContext('2d').drawImage(canvas, 0, 0);
        },
        // 生成二维码
        generateQrcode() {
            const options = {
                width: 400,
                height: 400,
            };
            QRCode.toCanvas(this.link, options)
                .then((el) => {
                    this.showCode = true;		//showCode 决定是否显示二维码
                    this.mergeCanvas(el);		//生成二维码后，合并二维码
                })
                .catch((err) => {
                    this.showCode = false;
                });
        },
        // 保存生成的二维码
        handleDownloadCode() {
            const { qrcodeCanvas } = this.$refs;
            const url = qrcodeCanvas.toDataURL('image/png');

            var aEle = document.createElement('a');
            aEle.download = '门店小程序码'
            aEle.href = url;
            document.body.appendChild(aEle);
            aEle.click();
            document.body.removeChild(aEle);
        },
        // 复制链接
        handleCopy(copy) {
            var input = document.createElement('input');
            input.value = copy;
            document.body.appendChild(input);
            input.select();
            document.execCommand("copy")
            document.body.removeChild(input)
            this.$message.success("链接已复制到剪贴板！");
        }
    }
}
</script>

<style lang="less" scoped>
.qrcode-main {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    .qrcode {
        width: 250px;
        height: 250px;
    }
}
</style>
```

### 117.微信小程序API兼容性处理

> ### Object wx.getSystemInfoSync()
>
> 从基础库 [2.20.1](https://developers.weixin.qq.com/miniprogram/analysis/experience/compatibility.html) 开始，本接口停止维护，请使用 [wx.getSystemSetting](https://developers.weixin.qq.com/miniprogram/dev/api/base/system/wx.getSystemSetting.html)、[wx.getAppAuthorizeSetting](https://developers.weixin.qq.com/miniprogram/dev/api/base/system/wx.getAppAuthorizeSetting.html)、[wx.getDeviceInfo](https://developers.weixin.qq.com/miniprogram/dev/api/base/system/wx.getDeviceInfo.html)、[wx.getWindowInfo](https://developers.weixin.qq.com/miniprogram/dev/api/base/system/wx.getWindowInfo.html)、[wx.getAppBaseInfo](https://developers.weixin.qq.com/miniprogram/dev/api/base/system/wx.getAppBaseInfo.html) 代替

```js
let systemInfo = {}

if (wx.canIUse('getSystemInfoSync')) {
    systemInfo = wx.getSystemInfoSync();
}
else {
    systemInfo = Object.assign(wx.getDeviceInfo(), wx.getWindowInfo())
}
```

### 118.微信小程序获取图片主色

`utils/colorThief.js`

```js
const colorThief = {
  makeRGB: function (name) {
    return ["rgb(", name, ")"].join("");
  },

  mapPalette: function (palette) {
    var arr = [];
    for (var prop in palette) {
      arr.push(this.frmtPobj(prop, palette[prop]));
    }
    arr.sort(function (a, b) {
      return b.count - a.count;
    });
    return arr;
  },

  fitPalette: function (arr, fitSize) {
    if (arr.length > fitSize) {
      return arr.slice(0, fitSize);
    } else {
      for (var i = arr.length - 1; i < fitSize - 1; i++) {
        arr.push(this.frmtPobj("0,0,0", 0));
      }
      return arr;
    }
  },

  frmtPobj: function (a, b) {
    return { name: this.makeRGB(a), count: b };
  },

  PALETTESIZE: 10,
  RGBaster: {},
  canvasId: "",
  imagePath: "",
  options: {},
  retrySum: 100, // enough? too much? It needs more experiences.

  /**
   * 获取主色调
   * @imagePath 路径
   * @canvasId canvas ID
   * @opts {success: 成功回调, width: 宽, height: 高}
   */
  colors: function (imagePath, canvasId, opts) {
    this.canvasId = canvasId;
    this.imagePath = imagePath;
    this.options = opts;

    var data,
      width = opts.width || 150,
      height = opts.height || 100;
    const ctx = wx.createCanvasContext(canvasId);
    ctx.drawImage(imagePath, 0, 0, width, height);
    ctx.draw();

    setTimeout(
      function () {
        const u = this;
        wx.canvasGetImageData({
          canvasId: canvasId,
          x: 0,
          y: 0,
          width: width,
          height: height,
          success(res) {
            // console.log(res.width);
            // console.log(res.height);
            // console.log(res.data instanceof Uint8ClampedArray);
            // console.log(res.data.length); // res.width * res.height * 4
            u.calculate(res.data, opts);
          },
          fail() {
            console.log("fail");
          },
        });
      }.bind(this),
      50
    );
  },

  calculate: function (data, opts) {
    opts = opts || {};
    var exclude = opts.exclude || [],
      paletteSize = opts.paletteSize || this.PALETTESIZE;
    // for example, to exclude white and black:  [ '0,0,0', '255,255,255' ]
    var colorCounts = {},
      rgbString = "",
      rgb = [],
      colors = {
        dominant: { name: "", count: 0 },
        palette: [],
      };

    var i = 0;
    for (; i < data.length; i += 4) {
      rgb[0] = data[i];
      rgb[1] = data[i + 1];
      rgb[2] = data[i + 2];
      rgbString = rgb.join(",");

      // skip undefined data and transparent pixels
      if (rgb.indexOf(undefined) !== -1 || data[i + 3] === 0) {
        continue;
      }

      // Ignore those colors in the exclude list.
      if (exclude.indexOf(this.makeRGB(rgbString)) === -1) {
        if (rgbString in colorCounts) {
          colorCounts[rgbString] = colorCounts[rgbString] + 1;
        } else {
          colorCounts[rgbString] = 1;
        }
      }
    }

    if (opts.success) {
      var palette = this.fitPalette(
        this.mapPalette(colorCounts),
        paletteSize + 1
      );

      //图片未加载完
      //合理？
      if (
        palette[0].name == palette[1].name &&
        palette[1].name == "rgb(0,0,0)"
      ) {
        if (this.retrySum-- <= 0) {
          console.log("retrySum: " + this.retrySum);
          palette.length = 0;
          palette.push(this.frmtPobj("0,0,0", 0));
          palette.push(this.frmtPobj("0,0,0", 1));
        } else {
          this.colors(this.imagePath, this.canvasId, this.options);
          return;
        }
      }

      opts.success({
        dominant: palette[0].name,
        secondary: palette[1].name,
        palette: palette
          .map(function (c) {
            return c.name;
          })
          .slice(1),
      });
    }
  },

  /**
   * invert color
   * @oldColor rgb(0,0,0)
   */
  invertColor: function (oldColor) {
    const tempArr = oldColor.slice(4, oldColor.length - 1).split(",");
    return (
      "rgb(" +
      (255 - tempArr[0]) +
      "," +
      (255 - tempArr[1]) +
      "," +
      (255 - tempArr[2]) +
      ")"
    );
  },

  /**
   * rgb转16进制
   */
  rgbToHex: function (rgb) {
    // rgb(x, y, z)
    var color = rgb.toString().match(/\d+/g); // 把 x,y,z 推送到 color 数组里
    var hex = "#";

    for (var i = 0; i < 3; i++) {
      // 'Number.toString(16)' 是JS默认能实现转换成16进制数的方法.
      // 'color[i]' 是数组，要转换成字符串.
      // 如果结果是一位数，就在前面补零。例如： A变成0A
      hex += ("0" + Number(color[i]).toString(16)).slice(-2);
    }
    return hex;
  },

  /**
   * 明暗色调
   */
  isLight: function (rgb) {
    var color = rgb.toString().match(/\d+/g);
    console.log("color: " + color);
    return 0.213 * color[0] + 0.715 * color[1] + 0.072 * color[2] > 255 / 2;
  },

  /**
   * hex转rgb
   * @param {string} str  色值，如：#409EFF
   * @returns rgb数组[64, 158, 255]
   */
  hexToRgb: function (str) {
    let hexs = null;
    let reg = /^\#?[0-9A-Fa-f]{6}$/;
    if (!reg.test(str)) {
      console.log("色值不正确");
      return false;
    }
    str = str.replace("#", ""); // 去掉#
    hexs = str.match(/../g); // 切割成数组 409EFF => ['40','9E','FF']
    // 将切割的色值转换为16进制
    for (let i = 0; i < hexs.length; i++) hexs[i] = parseInt(hexs[i], 16);
    return hexs; // 返回rgb色值[64, 158, 255]
  },

  /**
   * 颜色减淡
   * @param {string} color  色值，如：##409EFF
   * @param {number} level 调整幅度，0~1之间
   * @returns {array} 最终颜色减淡的rgb数组
   */
  getLightColor: function (color, level) {
    let reg = /^\#?[0-9A-Fa-f]{6}$/;
    if (!reg.test(color)) {
      console.log("色值不正确");
      return false;
    }
    let rgb = colorThief.hexToRgb(color);
    // 循环对色值进行调整
    for (let i = 0; i < 3; i++) {
      rgb[i] = Math.floor((255 - rgb[i]) * level + rgb[i]); // 始终保持在0-255之间
    }
    return rgb; // [159, 206, 255]
  },
};

module.exports.colorThief = colorThief;
```

使用：`home.js`片段

```js
import { colorThief } from "../../utils/colorThief.js";

// 获取图片主色
getImageColor(src) {
const canvasId = "myCanvas";
let that = this
wx.getImageInfo({
  src,
  success: (imgInfo) => {
    const { path, height, width } = imgInfo;
    colorThief.colors(path, canvasId, {
      success: function (res) {
        console.log("dominant: " + res.dominant);

        that.setData({
          dominant: colorThief.rgbToHex(res.dominant),
          lightDominant: colorThief.rgbToHex(colorThief.getLightColor(colorThief.rgbToHex(res.dominant), 0.6))
        })
      },
      width: width,
      height: height,
    });
  }
})
},
```

使用：`home.wxml`片段

```html
<!-- 会员模块 -->
<canvas canvas-id="myCanvas" style="position: absolute; left: -1000px;"></canvas>
<view class="member-card-wrap" wx:if="{{ memberInfo && memberInfo.nickname != '' }}">
    <view class="member-card-content">
        <image src="{{ memberInfo.avatar }}" class="avatar" mode="widthFix" catch:tap="goUserInfo" style="border: 3rpx solid {{ dominant }};"/>
        <view class="info">
            <!-- 会员昵称 -->
            <view class="title">
                {{ memberInfo.nickname ? memberInfo.nickname : '' }}
            </view>
            <!-- 会员等级 -->
            <view class="date" style="background: {{ lightDominant }};">
                <image src="{{ memberInfo.level_logo ? memberInfo.level_logo : levelIcon }}" class="logo" mode="widthFix" />
                <text class="ellipsis">{{ memberInfo.level_name }}</text>
            </view>
        </view>
    </view>
    <!-- 缴费升级 -->
    <!-- operate 0-不显示 1-立即升级 2-去缴费 3-查看 -->
    <button class="btn" bind:tap="goMember" wx:if="{{ memberInfo.operate && memberInfo.operate != '0'}}">
        <view>
            {{ memberInfo.operate == '1' ? '立即升级' : (memberInfo.operate == '2' ? '立即续费' : '查看') }}
        </view>
        <image src="{{ baseUrl }}upfile/icon/wx/home/buttonArrow.png" class="arrow" />
    </button>
</view>
```

![image-20250318135544243](https://gitee.com/v876774538/my-img/raw/master/image-20250318135544243.png)

参考地址：[javascript - hex和rgb色值转换-色彩加深减淡 - 兔子先森的博客 - SegmentFault 思否](https://segmentfault.com/a/1190000044493429)

### 119.富文本编辑器 WangEditor使用（vue3 element-ui）

#### 119.1 使用

**子组件封装**：

![image-20250331115554567](https://gitee.com/v876774538/my-img/raw/master/image-20250331115554567.png)

```vue
<template>
  <div style="border: 1px solid #ccc">
    <Toolbar style="border-bottom: 1px solid #ccc" :editor="editorRef" :defaultConfig="toolbarConfig" mode="default" />
    <Editor
      style="height: 200px; overflow-y: hidden"
      v-model="valueHtml"
      :defaultConfig="editorConfig"
      mode="default"
      @onCreated="handleCreated"
      @customPaste="customPaste"
      @onChange="handleChanged"
    />
  </div>
</template>
<script setup>
// 富文本编辑器文档链接: https://www.wangeditor.com/v5/getting-started.html
// 引入富文本编辑器CSS
import "@wangeditor/editor/dist/css/style.css"
import { onBeforeUnmount, ref, shallowRef } from "vue"
// 导入富文本编辑器的组件
import { Editor, Toolbar } from "@wangeditor/editor-for-vue"
import { uploadImg } from "@/api/public"
import { ElMessage } from "element-plus"

const emit = defineEmits(["change"])

// 编辑器实例，必须用 shallowRef
const editorRef = shallowRef()

// 内容 HTML
// const valueHtml = ref("<p>hello <strong>hello world</strong></p>")
const valueHtml = ref("")
const toolbarConfig = {}
const editorConfig = ref({ placeholder: "请输入内容...", MENU_CONF: {} })

// // 自定义图片上传
// editorConfig.value.MENU_CONF["uploadImage"] = {
//   async customUpload(file, insertFn) {
//     console.log("上传图片", file)
//     // 将上传的file图片转换为base64
//     const base64 = URL.createObjectURL(file)

//     // 这里的file为上传的图片对象,insertFn传入
//     insertFn(base64, "img")
//   }
// }

// 图片上传限制
const handleBeforeUpload = (uploadFile, limit) => {
  if (limit && limit.size) {
    if (uploadFile.size / 1024 > limit.size) {
      ElMessage.error(`图片大小不能超过${limit.size}K`)
      return false
    } else if (limit.type && !uploadFile.raw.type.includes(limit.type)) {
      ElMessage.error(`图片格式不正确，请上传${limit.type}格式图片`)
      return false
    }
  }
  return true
}

// 自定义图片上传
editorConfig.value.MENU_CONF["uploadImage"] = {
  async customUpload(file, insertFn) {
    if (handleBeforeUpload(file)) {
      uploadImg({ file })
        .then((res) => {
          if (res.code == 0) {
            insertFn(res.data.domain + res.data.image, "img")
          } else {
            ElMessage.error(res.msg)
          }
        })
        .catch((err) => {
          ElMessage.error(err.msg)
        })
    }
  }
}

// 自定义视频上传
editorConfig.value.MENU_CONF["uploadVideo"] = {
  async customUpload(file, insertFn) {
    console.log("上传视频", file)
  }
}

// 富文本编辑器生成后触发
const handleCreated = (editor) => {
  editorRef.value = editor // 记录 editor 实例，重要！
  console.log(editorConfig.value.MENU_CONF, "editorConfig.value")
}

// 监听富文本编辑器粘贴行为
const customPaste = (editor, event, callback) => {
  // 获取粘贴的纯文本
  const text = event.clipboardData.getData("text/plain")
  if (text) {
    editor.insertText(text)
    event.preventDefault()
    callback(false)
  }
}

// 获取富文本html内容
// const getEditorHTML = () => {
//   console.log(editorRef.value.getHtml())
// }

// 富文本编辑器内容改变时触发
const handleChanged = (editor) => {
  console.log(editor.getHtml())
  // 通知父组件
  emit("change", editor.getHtml())
}

// 组件销毁时，也及时销毁编辑器
onBeforeUnmount(() => {
  const editor = editorRef.value
  if (editor == null) return
  editor.destroy()
})
</script>
```

**父组件**：

```vue
  <wang-editor ref="wangEditor" @change="handleEditorChanged" />
```

```js
// 富文本 活动详情
const handleEditorChanged = (e) => {
  editForm.value.activity_detail = e	// 赋值
}
```

### 120.关闭commitlint配置

![image-20250402120810626](https://gitee.com/v876774538/my-img/raw/master/image-20250402120810626.png)

### 121.uniapp vue3 自适应scroll-view组件

组件：`components/m-scroll-view/index.vue`

```vue
<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationBarTitleText: '',
  },
}
</route>

<template>
  <view id="top" />
  <scroll-view :style="{ height: scrollH + 'px' }" scroll-y>
    <slot></slot>
  </scroll-view>
</template>

<script lang="ts" setup>
import { ref, getCurrentInstance, watchEffect } from 'vue'

defineOptions({
  name: 'mScrollView',
})

const props = defineProps({
  offset: {
    type: Number,
    default: 0,
  }, // 偏移量
})

/** Hooks 动态计算scrollList滑动区域高度
 * @param {Number} offset 可选 -offset偏移量 手动微调scroll高度
 * */
const useScrollHeight = (offset?: number): any => {
  const scrollHeight = ref<number>(0) // scroll组件高度
  const topHeight = ref<number>(0) // 组件上方占用高度
  const currentInstance = getCurrentInstance() // vue3绑定this
  const safeAreaInsets = uni.getSystemInfoSync().safeAreaInsets // 屏幕边界到安全区域距离
  const height = uni.getSystemInfoSync().windowHeight // 获取页面高度
  const topEl = uni.createSelectorQuery().in(currentInstance).select('#top') // 获取#top元素
  topEl
    .boundingClientRect((data) => {
      // 获取顶部高度
      topHeight.value = (data as any).top
      scrollHeight.value = height - safeAreaInsets?.top - topHeight.value - (offset || 0) // 计算剩余高度 offset 偏移量
    })
    .exec()
  return scrollHeight
}

const scrollH = ref(0) // scroll-view组件高度

onReady(() => {
  const scrollHeight = useScrollHeight(props.offset)
  watchEffect(() => {
    scrollH.value = scrollHeight.value
  })
})
</script>

<style lang="less" scoped></style>

```

使用：

```vue
<m-scroll-view class="card-content">
  <view class="card-item" v-for="(item, index) in list" :key="index">
    <view class="left">
      <view class="label">日期</view>
      <view class="value">{{ item.date }}</view>
    </view>
    <view class="right">
      <view class="label">收益</view>
      <view class="value ellipsis">￥{{ formatPrice(item.earnings) }}</view>
    </view>
  </view>
  // 填充内容...
</m-scroll-view>
```

![image-20250403140836872](https://gitee.com/v876774538/my-img/raw/master/image-20250403140836872.png)

### 122.uniapp vue3 微信小程序使用qiun图表

`total-chart.vue`组件

```vue
<template>
  <view class="charts-box">
    <qiun-data-charts
      type="column"
      :chartData="chartData"
      :opts="options"
      :ontouch="true"
      canvasId="myCanvasId"
      :canvas2d="true"
      :tooltipShow="false"
      :disableScroll="true"
    />
    <!-- canvas2d=true canvasId 解决渲染层级过高问题（开启后模拟器异常无需理会） -->
  </view>
</template>

<script setup lang="ts">
const props = defineProps({
    // 图表数据
  data: {
    type: Object,
    default: () => {},
  },
})

const options = reactive({
  color: ['#3376ff'], // 主题颜色
  padding: [20, 0, 0, 0], // 画布填充边距，顺序为上右下左，例如[10,15,25,15]
  enableScroll: true, // 开启滚动条，X轴配置里需要配置itemCount单屏幕数据点数量
  // scrollPosition: 'right', // 连续更新数据时，滚动条的位置。可选值："current"当前位置,"left"左对齐,"right"右对齐
  // update: true, // 开启连续更新数据的方法
  legend: {
    show: false, // 不显示图例
  },
  dataLabel: true, // 是否显示图表区域内数据点上方的数据文案
  fontSize: 10, // 全局默认字体大小
  fontColor: '#999999', // 全局默认字体颜色
  xAxis: {
    disableGrid: true,
    itemCount: 8,
    axisLineColor: '#ECEDEE', // 坐标轴线颜色
    scrollColor: '#ECECEC', // 滚动条颜色
    scrollBackgroundColor: '#FFFFFF', // 滚动条背景颜色
    fontSize: 10, // 字体大小
    fontColor: '#999999', // 字体颜色
    scrollShow: true, // 滚动条显示
    scrollAlign: 'right', // 滚动条初始位置
  },
  yAxis: {
    data: [
      {
        min: 0,
        formatter: (value) => {
          if (value) {
            return `￥${value}`
          } else {
            return '0'
          }
        },
      },
    ],
    gridColor: '#ECEDEE',
  },
  extra: {
    column: {
      type: 'group',
      width: 10,
      activeBgColor: '#000000',
      activeBgOpacity: 0.08,
      linearType: 'custom',
      seriesGap: 5,
      //   linearOpacity: 0.5,
      barBorderCircle: true,
      customColor: ['#3376ff'],
    },
  },
})
const chartData = ref({})

const getServerData = (data) => {
  if (data) {
    const res = {
      categories: [],
      series: [
        {
          name: '收益',
          data: [],
          color: '#3376FF',
        },
      ],
    }
    data.forEach((item, index) => {
      // 截掉年份部分，只保留月份和日期
      const dateParts = item.date.split('-')
      const monthDay = `${dateParts[1]}-${dateParts[2]}`
      res.categories.push(monthDay)
      res.series[0].data.push(item.profit ? item.profit : '') // 0值为''不显示dataLabel
      // res.series[0].data.push(index ? item.profit + index * 100 : '') // 假数据
    })
    chartData.value = JSON.parse(JSON.stringify(res))
  }
}

watch(
  () => props.data,
  (newVal) => {
    getServerData(newVal)
  },
)
</script>

<style lang="less" scoped>
.charts-box {
  width: 629rpx;
  height: 100%;
  z-index: 0;
  // position: relative;
}
</style>
```

使用：

```vue
<view class="chart-main">
  <total-chart :data="summaryData.list"></total-chart>
</view>
```

效果：

![image-20250415093852030](https://gitee.com/v876774538/my-img/raw/master/image-20250415093852030.png)
