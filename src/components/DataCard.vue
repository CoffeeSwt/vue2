<template>
  <div>
    <el-descriptions border>
      <template v-for="(item, index) in pureAttr">
        <el-descriptions-item
          :label="item.key"
          :span="1"
          v-if="item.key != 'dateReleased'"
          >{{ item.value }}</el-descriptions-item
        >
        <el-descriptions-item
          :label="item.key"
          :span="2"
          v-if="item.key == 'dateReleased'"
          >{{ item.value }}</el-descriptions-item
        >
      </template>
      <template v-for="(item, index) in deepAttr">
        <el-descriptions-item :span="3" :label="item.key">
          <template v-if="item?.value[0]">
            <div>id:{{ item?.value[0]?.id }}</div>
            <div>createdAt:{{ item?.value[0]?.createdAt }}</div>
            <div>updatedAt:{{ item?.value[0]?.updatedAt }}</div>
          </template>

          <template v-for="i in item?.value[0]?.data || []">
            <PersonInfoCard :data="i"></PersonInfoCard>
          </template>
        </el-descriptions-item>
        <el-descriptions-item :span="3" label="data" v-if="item.key == 'data'">
          <div>
            <el-card
              ><div>
                <span>信息</span>
              </div>
              <el-image
                style="width: 100px; height: 100px"
                :src="item.value[0].poster"
                fit="fill"
              ></el-image>
              <template
                v-for="(i, index) in Object.entries(item.value[0] || {})"
              >
                <div v-if="i[0] != 'poster'">{{ i[0] }}:{{ i[1] }}</div>
              </template>
            </el-card>
          </div>
          <div>
            <el-card>
              <div>
                <span>Info</span>
              </div>
              <el-image
                style="width: 100px; height: 100px"
                :src="item.value[1].poster"
                fit="fill"
              ></el-image>
              <template
                v-for="(i, index) in Object.entries(item.value[1] || {})"
              >
                <div v-if="i[0] != 'poster'">{{ i[0] }}:{{ i[1] }}</div>
              </template>
            </el-card>
          </div>
        </el-descriptions-item>
      </template>
    </el-descriptions>
  </div>
</template>

<script>
import PersonInfoCard from "./PersonInfoCard.vue";
export default {
  components: {
    PersonInfoCard,
  },
  props: {
    data: Object,
  },
  data() {
    return {};
  },
  computed: {
    pureAttr: function () {
      if (!this.data) return [];
      return Object.entries(this.data)
        .filter((val) => typeof val[1] != "object")
        .map((i) => {
          return {
            key: i[0],
            value: i[1],
          };
        });
    },
    deepAttr: function () {
      if (!this.data) return [];
      return Object.entries(this.data)
        .filter((val) => typeof val[1] == "object")
        .map((i) => {
          return {
            key: i[0],
            value: i[1],
          };
        });
    },
  },
  methods: {},
  mounted() {},
};
</script>

<style scoped></style>
