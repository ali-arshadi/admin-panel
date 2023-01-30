<template>
  <div class="table-container">
    <table>
      <thead>
        <tr>
          <th class="first-head-element"></th>
          <th v-for="(header, index) in tableHeaders" :key="index">
            {{ header }}
          </th>
          <th class="operation-element"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(bodyData, index) in tableData" :key="index">
          <td>1</td>
          <td v-for="data in bodyData" :key="data">
            {{ data }}
          </td>
          <td class="operation-element">
            <div class="operation">
              <DotIcon />
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
//! it can not be used for now
<script lang="ts">
import Vue from 'vue';
export default Vue.extend({
  data() {
    return {
      tableHeaders: [] as any,
      tableBody: [] as any,
    };
  },
  props: {
    tableData: {
      type: Array,
      default: () => [],
    },
  },
  components: {
    DotIcon: () => import('@/components/icons/icon-dot.vue'),
  },
  mounted() {
    if (this.tableData && this.tableData.length > 0) {
      //* getting the the names of the object properties
      //* that we receive from the the component

      const element = this.tableData[0];

      const objectPropertyName = Object.getOwnPropertyNames(element);

      objectPropertyName.pop();

      this.tableHeaders = objectPropertyName;
    } else {
      console.log('add data to the table component');
    }
  },
});
</script>

<style lang="scss" scoped>
@import '@/assets/scss/helpers/variables';
table {
  border-collapse: collapse;
  border: 4px solid $black;
  background-color: $anti-flash-white;
  width: 100%;
}
th,
td {
  border: 1px solid $black;
  padding: 18px;
  text-align: center;
}
thead th {
  width: 25%;
}
.first-head-element {
  width: fit-content;
}
.operation-element {
  width: fit-content;
}
.red {
  background-color: white;
  color: red;
}
</style>
