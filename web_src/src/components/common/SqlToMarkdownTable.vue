<template>
  <div>
    <el-dialog
      :title="$t('sql_to_markdown_table')"
      :visible.sync="dialogFormVisible"
      :close-on-click-modal="false"
      @close="callback()"
    >
      <el-form>
        <el-input
          type="textarea"
          class="dialoContent"
          :placeholder="$t('sql_to_markdown_table_description')"
          :rows="10"
          v-model="content"
        ></el-input>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="callback()">{{ $t('cancel') }}</el-button>
        <el-button type="primary" @click="transform">{{
          $t('confirm')
        }}</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: 'SqlToMarkdownTable',
  props: {
    formLabelWidth: '120px',
    callback: ''
  },
  data() {
    return {
      content: '',
      json_table_data: '',
      dialogFormVisible: true
    }
  },
  methods: {
    transform() {
      this.request('/api/page/sqlToMarkdownTable', {
        sql: this.content
      }).then(res => {
        this.callback(res.data.markdown)
      })
      this.dialogFormVisible = false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
