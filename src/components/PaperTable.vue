<template>
  <table class="table" :class="tableClass">
    <thead>
    <slot name="columns">
      <th v-for="(item, index) in columns" :key="index">{{columnNames[index]}}</th>
    </slot>
    </thead>
    <tbody>
    <tr v-for="(item, index) in data" :key="index">
      <slot :row="item">
        <td v-for="(column, index) in columns"
            :key="index"
            v-if="hasValue(item, column)">
          {{itemValue(item, column)}}
        </td>
      </slot>
    </tr>
    </tbody>
  </table>
</template>
<script>
export default {
  name: 'paper-table',
  props: {
    columns: Array,
    data: Array,
    type: {
      type: String, // striped | hover
      default: "striped"
    },
    title: {
      type: String,
      default: ""
    },
    subTitle: {
      type: String,
      default: ""
    },
    columnNames: Array
  },
  computed: {
    tableClass() {
      return `table-${this.type}`;
    }
  },
  methods: {
    hasValue(item, column) {
      console.log('hasValue' + item[column.toLowerCase()]);
      //return item[column.toLowerCase()] !== "undefined";
      return item[column] !== "undefined";
    },
    itemValue(item, column) {
      console.log('itemValue' + item[column.toLowerCase()]);
      //var val = item[column.toLowerCase()];
      var val = item[column];
      //if(val.length == 0) {
      //  val = "-";
      //}
      return val;
    }
  }
};
</script>
<style>
</style>
