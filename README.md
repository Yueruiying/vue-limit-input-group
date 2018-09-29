# 分组 最大值，最小值 控制组件

## 依赖

`element-ui/el-input-number`

## 安装

`yarn add vue-limit-input-group`

or

`npm i vue-limit-input-group -S`

## 简述
limit-input-number 基于 element-ui 的 el-input-number 控件基础改造, 所以本组件依赖 element-ui
limit-input-number 可直接替换 el-input-number

## 属性
max: 所有input总和最大值
min: 所有input总和最低值

## 事件 
greaterThan(newVal, overVal, maxVal): 当控件总和超过最大值
lessThan(newVal, overVal, minVal): 当控件总和小于最小值

### 参数解释
newVal: 当前输入的值
overVal: 剩余能输入的数值
maxVal: 最大数值
minVal: 最小数值

## 使用方式

```html
<limit-input-group max="12" min="5" @greaterThan="(newVal, ) => { alert('不能大于12') }">
    <limit-input-number v-model="num1"/>
    <limit-input-number v-model="num2"/>
    <limit-input-number v-model="num3"/>
</limit-input-group>
```

### 注意事项

limit-input-number 一定要是 limit-input-group 子组件，支持多层嵌套

limit-input-group 只监管 limit-input-number 不监管 el-input-number

```html
<el-form label-width="80px">
    <limit-input-group :max="25" :min="10" @greaterThan="greaterThan" @lessThan="lessThan">
      <el-form-item label="值0">
          <el-col :span="4">
              <el-input-number v-model="num0" :min="1" :max="10"/>
          </el-col>
          <el-col :span="2">
              <el-alert title="我不算" type="warning" class="no-pd" :closable="false"/>
          </el-col>
      </el-form-item>
      <el-form-item label="值2">
          <limit-input-number v-model="num1"/>
      </el-form-item>
      <el-form-item label="值3">
          <limit-input-number v-model="num2"/>
      </el-form-item>
      <el-form-item label="值4">
          <limit-input-number v-model="num3"/>
      </el-form-item>
      <el-form-item label="值5">
          <limit-input-number v-model="num4"/>
      </el-form-item>
      <el-form-item label="值6">
          <limit-input-number v-model="num5"/>
      </el-form-item>
      <el-form-item label="值6">
          <limit-input-number v-model="num6"/>
      </el-form-item>
    </limit-input-group>
</el-form>
```
```javascript
import {LimitInputGroup, LimitInputNumber} from '../src/packages';

export default {
    components: {
        LimitInputGroup,
        LimitInputNumber
    },
    methods: {
        lessThan(newVal, overMinVal, minVal) {
            this.$message.warning('不能小于' + minVal)
        },
        greaterThan(newVal, overMaxVal, max) {
            this.$message.warning('不能超过' + max)
        }
    },
    data() {
        return {
            num0: 0,
            num1: 1,
            num2: 0,
            num3: 0,
            num4: 0,
            num5: 0,
            num6: 0
        }
    }
}
```