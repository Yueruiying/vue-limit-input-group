<script>
	/* eslint-disable */
	import {InputNumber} from 'element-ui';

	function isNumber(val) {
		return Object.prototype.toString.call(val) === '[object Number]'
	}

	function isNumberElse(val, defaultVal) {
		return isNumber(val) ? val : defaultVal
	}

	function recursiveChildren(children) {
		let childList = []
		for ( let child of children ) {
			if ( child.$vnode.tag.includes("limit-input-number") ) {
				childList.push(child)
            } else {
                childList = childList.concat(recursiveChildren(child.$children))
            }
        }
        return childList;
    }

	export default {
		name: 'limit-input-number',
		inject: ['groupMax', 'groupMin', 'inputGroup'],
		extends: InputNumber,
		methods: {
			sumOther() {
				const children = recursiveChildren(this.inputGroup.$children)
				let sum = 0
				for (let input of children) {
					if (input !== this) {
						sum += input.currentValue || 0
					}
				}
				return sum
			},
			setCurrentValue(newVal) {
				const maxVal = isNumberElse(this.groupMax, this.max)
				const minVal = isNumberElse(this.groupMin, this.min);
				// 此次能填写的最大值(值余额) = 全部最大值 - 其他值得和
				const overMaxVal = maxVal - this.sumOther()
				const overMinVal = minVal - this.sumOther()
				// 以下是 el-input-number 的源码，对 max 做了改动，覆盖了原有的 setCurrentValue 方法
				const oldVal = this.currentValue;
				if (typeof newVal === 'number' && this.precision !== undefined) {
					newVal = this.toPrecision(newVal, this.precision);
				}
				// 下面两个逻辑是共享最大值的逻辑
				if (newVal >= overMaxVal) {
					newVal = overMaxVal
					this.inputGroup.$emit('greaterThan', newVal, overMaxVal, maxVal)
				}
				if (newVal <= overMinVal) {
					newVal = overMinVal
					this.inputGroup.$emit('lessThan', newVal, overMinVal, minVal)
				}
				if (oldVal === newVal) {
					this.$refs.input.setCurrentValue(this.currentInputValue);
					return;
				}
				this.$emit('input', newVal);
				this.$emit('change', newVal, oldVal);
				this.currentValue = newVal;
			}
		}
	}
</script>