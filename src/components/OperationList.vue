<template>
  <div class="operation-list">
    <operation-list-item
      v-for="ope in operations"
      v-ref:operations
      :operation="ope" :index="$index"
      @on-key-enter="onItemKeyEnter" @on-key-delete="onItemKeyDelete"
      @on-key-up="onItemKeyUp" @on-key-down="onItemKeyDown"
      @on-focus="onItemFocus" @on-blur="onItemBlur">
    </operation-list-item>
  </div>
</template>

<script>
  import OperationListItem from './OperationListItem'

  export default {
    components: { OperationListItem },

    data () {
      return {
        operations: [
          { source: 'goto "index"' },
          { source: 'fill "#name", "foo"' },
          { source: '' }
        ],

        selectionIndex: -1
      }
    },

    ready () {
      this.selectionIndex = 0
    },

    watch: {
      selectionIndex (newIndex, oldIndex) {
        const oldOpe = this.operations[oldIndex]

        if (oldOpe && oldOpe.source === '' && oldIndex !== this.operations.length - 1) {
          if (newIndex > oldIndex) {
            this.$set('selectionIndex', this.selectionIndex - 1)
          }

          this.operations.$remove(oldOpe)
        }

        this.$nextTick(() => this.$refs.operations[this.selectionIndex].focus())
      }
    },

    computed: {
      selectionOpe () {
        this.selectionIndex
        return this.operations[this.selectionIndex]
      }
    },

    methods: {
      removeEmptyItems () {
        this.newOpeIndexes.forEach((i) => {
          this.operations.splice(i, 1)
        })
      },

      selectPrev () {
        if (this.selectionIndex !== 0) {
          this.selectionIndex--
        }
      },

      selectNext () {
        if (this.operations.length - 1 > this.selectionIndex) {
          this.selectionIndex++
        }
      },

      insert (originItem, operation) {
        this.operations.splice(originItem.index + 1, 0, operation)
      },

      insertEmpty (originItem) {
        if (originItem.operation.source === '' || originItem.index + 1 === this.operations.length - 1) return false

        this.insert(originItem, { source: '' })
        return true
      },

      onItemKeyEnter (item, e) {
        if (e.shiftKey) {
          this.insertEmpty(item)
          this.selectNext()
        } else {
          if (this.operations.length - 1 === this.selectionIndex && item.operation.source !== '') {
            // 新規追加用のボックスの場合
            this.operations.push({ source: '' })
          }

          this.selectNext()
        }
      },

      onItemKeyDelete (item, e) {
        if (item.index === this.operations.length - 1 || item.operation.source !== '') return
        if (item.index === 0) {
          this.selectNext()
        } else {
          this.selectPrev()
        }
      },

      onItemKeyUp () {
        this.selectPrev()
      },

      onItemKeyDown () {
        this.selectNext()
      },

      onItemFocus (item) {
        this.selectionIndex = item.index
      },

      onItemBlur (item, e) {
        // if (item.operation.source === '' && item.index !== this.operations.length - 1) {
        //   this.operations.$remove(item.operation)
        // }
      }
    }
  }
</script>

<style scoped>

</style>
