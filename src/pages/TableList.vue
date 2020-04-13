<template>
    <div class="row">
      <div class="col-12">
        <card :title="table1.title" :subTitle="table1.subTitle">
          <div slot="raw-content" class="table-responsive">
            <paper-table :data="table1.data" :columns="table1.columns" :columnNames="table1.columnNames">

            </paper-table>
          </div>
        </card>
      </div>
<!--
      <div class="col-12">
        <card class="card-plain">
          <div class="table-full-width table-responsive">
            <paper-table type="hover" :title="table2.title" :sub-title="table2.subTitle" :data="table2.data"
                         :columns="table2.columns">

            </paper-table>
          </div>
        </card>
      </div>
-->
    </div>
</template>

<script>
import api from "./backend-api";
import { PaperTable } from "@/components";
const tableColumns = ["seq", "server_name", "wait_cnt", "create_date"];
const columnNames = ["Id", "서버명", "대기수", "마지막업데이트"];
/*
const columnNames = {
    seq: "Id",
    server_name: "서버명",
    wait_cnt: "대기자",
    create_date: "업데이트"
  }*/
const tableData = [
  {
    id: 1,
    서버명: "주작",
    대기자: "323",
    업데이트: "2020.04.10 13:00"
  },
  {
    id: 2,
    서버명: "백호",
    대기자: "133",
    업데이트: "2020.04.10 13:00"
  },
  {
    id: 3,
    서버명: "청룡",
    대기자: "122",
    업데이트: "2020.04.10 13:00"
  },
  {
    id: 4,
    서버명: "봉황",
    대기자: "-",
    업데이트: "2020.04.10 13:00"
  },
  {
    id: 5,
    서버명: "신구",
    대기자: "-",
    업데이트: "2020.04.10 13:00"
  }
];

export default {
  components: {
    PaperTable
  },
  data() {
    return {
      table1: {
        title: "거상 대기열 정보",
        subTitle: "1시간 마다 업데이트",
        columns: [...tableColumns],
        columnNames: [...columnNames],
        data: []
      }
    };
  },
  mounted(){
    this.waitCntList();
  },
  methods: {
      // Fetches posts when the component is created.
    waitCntList () {
        api.waitCntList().then(response => {
            this.table1.data = response.data;
            console.log(response.data)
            return response.data;
        })
        .catch(error => {
          this.errors.push(error)
        })
    }
  }
};
</script>
<style>
</style>
