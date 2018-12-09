<template>
  <div>
    <v-btn @click="test">테스트</v-btn>
    <v-data-table
      v-model="selected"
      :headers="headers"
      :items="desserts"
      :pagination.sync="pagination"
      select-all
      item-key="id"
      class="elevation-1"
    >
      <template slot="headers" slot-scope="props">
        <tr>
          <th>
            <v-checkbox
              :input-value="props.all"
              :indeterminate="props.indeterminate"
              primary
              hide-details
              @click="toggleAll"
            ></v-checkbox>
          </th>
          <th
            v-for="header in props.headers"
            :key="header.text"
            :class="[
              'column sortable',
              pagination.descending ? 'desc' : 'asc',
              header.value === pagination.sortBy ? 'active' : ''
            ]"
            @click="changeSort(header.value)"
          >
            <i class="fas fa-arrows-alt-v"></i> {{ header.text }}
          </th>
        </tr>
      </template>
      <template slot="items" slot-scope="props">
        <tr :active="props.selected" @click="props.selected = !props.selected">
          <td>
            <v-checkbox
              :input-value="props.selected"
              primary
              hide-details
            ></v-checkbox>
          </td>
          <td>{{ props.item.id }}</td>
          <td class="text-xs-right">{{ props.item.title }}</td>
          <td class="text-xs-right">{{ props.item.body }}</td>
          <td class="text-xs-right">{{ props.item.author }}</td>
          <td class="text-xs-right">{{ props.item.category_id }}</td>
          <td class="text-xs-right">{{ props.item.category_name }}</td>
        </tr>
      </template>
    </v-data-table>

    <!-- <v-card
            class="pa-3"
            v-for="(data, index) in data"
            :key="index"
        >
            <p>{{ data.id }}</p>
        </v-card> -->

    <!-- {{ data.id }}
            {{ data.title }}
            {{ data.body }}
            {{ data.author }}
            {{ data.category_id }}
            {{ data.category_name }} -->
  </div>
</template>

<script>
//import axios from "@plugins/axios";

export default {
  data: () => ({
    pagination: {
      sortBy: "id"
    },
    selected: [],
    headers: [
      {
        text: "번호",
        align: "left",
        sortable: false,
        value: "id"
      },
      { text: "타이틀", value: "title" },
      { text: "내용", value: "body" },
      { text: "지은이", value: "author" },
      { text: "카테고리아이디", value: "category_id" },
      { text: "카테고리이름", value: "category_name" }
    ],
    desserts: []
  }),
  methods: {
    test() {
      axios
        .get("http://118.47.88.185/php-rest-api/api/post/read.php")
        .then(res => {
          //접속성공
          console.log(res);
          this.desserts = res.data;
        })
        .catch(err => {
          //접속실패
          console.log(err);
        })
        .then(() => {
          //항상실행
          console.log("항상실행");
        });
    },
    toggleAll() {
      if (this.selected.length) this.selected = [];
      else this.selected = this.desserts.slice();
    },
    changeSort(column) {
      if (this.pagination.sortBy === column) {
        this.pagination.descending = !this.pagination.descending;
      } else {
        this.pagination.sortBy = column;
        this.pagination.descending = false;
      }
    }
  }
};
</script>