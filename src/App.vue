<script>
import { ref } from "vue";
import url from "./http";

export default {
  // 반응형 상태
  data() {
    return {
      count: "test",
      users: []
    }
  },

  // methods는 속성 값을 변경하고 업데이트 할 수 있는 함수
  methods: {
    /* fetchData() {
      console.log("fetch Data")

      this.$axios.get(url + "/posts/1")
        .then((response) => {
          console.log(response.data);
          this.count = response.data;
        })
        .then((err) => {
          console.log(err);
        })

    }, */
    read() {
      let params = {}
      let postNumber = 2
      this.$axios.get(`${url}/posts`, {
          params: params,
        })
        .then(response => {
          const { data } = response
          this.users = data
        })
        .catch(error => {
          alert(error)
        })
    },
  },

  // 수명 주기 훅
  mounted() {
    console.log(`숫자 세기의 초기값은 ${this.count} 입니다.`)
    // this.fetchData()
  },
  created() {
    console.log(this.$axios);
    console.log(this.$foo); // bar
    console.log(url)
    this.read()
    // this.fetchData()
  }
}
</script>

<template>
  <table>
    <thead>
      <tr>
        <th>유저 id</th>
        <th>유저 이름</th>
        <th>유저 데이터</th>
      </tr>
    </thead>
    <tbody v-for="user in users">
      <tr>
        <td>{{ user.id }}</td>
        <td>{{ user.title }}</td>
        <td>{{ user.body }}</td>
      </tr>
    </tbody>
  </table>
</template>

<style>
table {
  border: 1px #a39485 solid;
  font-size: .9em;
  box-shadow: 0 2px 5px rgba(0, 0, 0, .25);
  width: 100%;
  border-collapse: collapse;
  border-radius: 5px;
  overflow: hidden;
}

th {
  text-align: left;
}

thead {
  font-weight: bold;
  color: #fff;
  background: #73685d;
}

td,
th {
  padding: 1em .5em;
  vertical-align: middle;
}

td {
  border-bottom: 1px solid rgba(0, 0, 0, .1);
  background: #fff;
}

a {
  color: #73685d;
}
</style>