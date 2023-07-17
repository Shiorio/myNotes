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

### 11.上传图片

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

### 20.上传图片

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

### 41.富文本编辑器 QuillEditor使用

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

#### 54.1 安装依赖插件

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
        else {	// 不存在
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

### 72.a-upload 限制上传的文件类型/校验上传的文件类型

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

