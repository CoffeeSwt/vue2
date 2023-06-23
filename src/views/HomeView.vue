<template>
  <div>
    <DataCard :data="tableData[0]"></DataCard>
  </div>
</template>

<script>
import DataCard from "../components/DataCard.vue";
import ldata from "../assets/data.json";
export default {
  components: {
    DataCard,
  },
  data() {
    return {
      tableData: [],
    };
  },
  methods: {
    async init() {
      this.tableData = await this.getData();
    },
    async getData() {
      const res = [ldata];
      return res;
    },
  },
  mounted() {
    this.init();
    console.log(ldata);
  },
};
</script>
