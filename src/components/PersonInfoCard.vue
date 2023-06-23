<template>
  <div>
    <el-card>
      <el-descriptions border>
        <template v-for="item in Object.entries(data)">
          <el-descriptions-item :label="item[0]">{{
            item[1]
          }}</el-descriptions-item></template
        >
      </el-descriptions>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    data: Object,
  },
  methods: {},
  mounted() {},
};
</script>
