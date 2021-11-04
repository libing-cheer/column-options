# column-options

应用 element 中的 table 组件，自定义设置显示列。

## 安装依赖

```bash
yarn install
```

## 运行命令 ✅

```bash
yarn run serve
```

## 编译打包命令 📦

```bash
yarn run build
```

### 效果图

![效果图](https://raw.githubusercontent.com/libing-cheer/table-header-tips/master/src/assets/tooltip.png)

### 引用 element-ui

```bash
npm install element-ui
```

在 main.js 中引入

```javascript
import Vue from "vue";
import ElementUI from "element-ui";
import "element-ui/lib/theme-chalk/index.css";
Vue.use(ElementUI);
```

### column-options 组件 自定义设置列 checkedTableColumns

```html
<template>
  <div class="column-options">
    <div class="operate-btn">
      <el-popover placement="bottom">
        <el-button slot="reference" size="mini" type="primary">
          显示列设置
        </el-button>
        <div class="column-display">
          <el-checkbox-group v-model="checkedTableColumns">
            <el-checkbox
              v-for="column in columns"
              :key="column.label"
              :label="column.prop"
            >
              {{ column.label }}
            </el-checkbox>
          </el-checkbox-group>
        </div>
      </el-popover>
    </div>
    <el-table ref="table" :data="tableData" style="width: 100%" stripe border>
      <el-table-column
        align="center"
        type="selection"
        min-width="50"
      ></el-table-column>
      <el-table-column
        label="序号"
        align="center"
        type="index"
        width="60"
        fixed
      ></el-table-column>
      <el-table-column
        v-for="item in bindTableColumns"
        :key="item.label"
        align="center"
        :label="item.label"
        :prop="item.prop"
        :min-width="item.width || 100"
        show-overflow-tooltip
      ></el-table-column>
    </el-table>
  </div>
</template>

<script>
  export default {
    name: "coulmnOptions",
    data() {
      return {
        columns: [
          { label: "姓名", prop: "name", width: 100, show: true },
          { label: "性别", prop: "sex", width: 150, show: true },
          { label: "年龄", prop: "age", width: 100, show: true },
          { label: "身高", prop: "height", width: 100, show: true },
          { label: "体重", prop: "weight", width: 100, show: true },
          { label: "发色", prop: "color", width: 100, show: true },
          { label: "国籍", prop: "nation", width: 100, show: true },
          { label: "故乡", prop: "home", width: 150, show: true },
        ],
        tableData: [
          {
            name: "王小虎",
            sex: "男",
            age: 23,
            height: 175,
            weight: 100,
            color: "黑色",
            nation: "中国",
            home: "北京",
          },
          {
            name: "李小虎",
            sex: "男",
            age: 24,
            height: 189,
            weight: 190,
            color: "绿色",
            nation: "中国",
            home: "南京",
          },
          {
            name: "赵小虎",
            sex: "男",
            age: 18,
            height: 178,
            weight: 200,
            color: "红色",
            nation: "中国",
            home: "重庆",
          },
          {
            name: "上官小虎",
            sex: "男",
            age: 34,
            height: 170,
            weight: 120,
            color: "紫色",
            nation: "中国",
            home: "成都",
          },
          {
            name: "公孙小虎",
            sex: "男",
            age: 25,
            height: 200,
            weight: 190,
            color: "蓝色",
            nation: "中国",
            home: "安徽",
          },
          {
            name: "百里小虎",
            sex: "男",
            age: 56,
            height: 210,
            weight: 200,
            color: "灰色",
            nation: "中国",
            home: "天津",
          },
        ],
      };
    },
    computed: {
      bindTableColumns() {
        return this.columns.filter((column) => column.show);
      },
      checkedTableColumns: {
        get() {
          return this.bindTableColumns.map((column) => column.prop);
        },
        set(checked) {
          // 设置表格列的显示与隐藏
          this.columns.forEach((column) => {
            // 如果选中，则设置列显示
            if (checked.includes(column.prop)) {
              column.show = true;
            } else {
              // 如果未选中，则设置列隐藏
              column.show = false;
            }
          });
        },
      },
    },
    beforeUpdate() {
      this.$nextTick(() => {
        // 在数据加载完，重新渲染表格
        this.$refs.table.doLayout();
      });
    },
    methods: {},
  };
</script>
<style>
  .column-options {
    width: 1500px;
    margin: 50px auto;
  }
  .column-display {
    width: 180px;
  }
  .operate-btn {
    padding: 15px 0;
    text-align: right;
  }
</style>
```
