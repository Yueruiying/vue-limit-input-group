<template>
    <div id="container">
        <el-alert title="除第一个组件外的所有组件之和 >= 10 && <= 25" type="info"/>
        <el-form label-width="80px">
            <limit-input-group :max="25" :min="10" @greaterThan="greaterThan" @lessThan="lessThan">
                <el-form-item label="值0">
                    <el-col :span="4">
                        <el-input-number v-model="num0" :min="0" :max="10"/>
                    </el-col>
                    <el-col :span="2">
                        <el-alert title="我不算" type="warning" class="no-pd" :closable="false"/>
                    </el-col>
                </el-form-item>
                <el-form-item label="值2">
                    <limit-input-number :min="0" v-model="num1"/>
                </el-form-item>
                <el-form-item label="值3">
                    <limit-input-number :min="0" v-model="num2"/>
                </el-form-item>
                <el-form-item label="值4">
                    <limit-input-number :min="0" v-model="num3"/>
                </el-form-item>
                <el-form-item label="值5">
                    <limit-input-number :min="0" v-model="num4"/>
                </el-form-item>
                <el-form-item label="值6">
                    <limit-input-number :min="0" v-model="num5"/>
                </el-form-item>
                <el-form-item label="值6">
                    <limit-input-number :min="0" v-model="num6"/>
                </el-form-item>
            </limit-input-group>
        </el-form>
    </div>
</template>
<script>
	/* eslint-disable */
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
</script>
<style>
    .no-pd {
        padding: 0 !important;
    }
</style>