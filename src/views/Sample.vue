<template>
    <div class="vuex">
        <h1>Sample 화면 입니다.</h1>
        totalItems : {{ totalItems }} <br />
        totalPages : {{ totalPages }} <br />
        <ul>
            <li v-for="(row, i) in items" :key="'result_table_' + i">{{ row }}</li>
        </ul>
    </div>
</template>

<script>
import http from "../http"

export default {
    name: "Vuex",
    components: {},
    data() {
        return {
            items: [],
            totalItems: 0,
            totalPages: 0,
        }
    },
    methods: {
        delete(id) {
            http
                .delete("/api/sample/sample/" + id)
                .then(response => {
                    const { data } = response
                    console.log(data)
                })
                .catch(error => {
                    alert(error)
                })
        },
        create(id, params) {
            http
                .post("/api/sample/sample/", params)
                .then(response => {
                    const { data } = response
                    console.log(data)
                })
                .catch(error => {
                    alert(error)
                })
        },
        update(id, params) {
            http
                .put("/api/sample/sample/" + id, {
                    params: params,
                })
                .then(response => {
                    const { data } = response
                    console.log(data)
                })
                .catch(error => {
                    alert(error)
                })
        },
        read() {
            let params = {}
            http
                .get("/api/sample/sample", {
                    params: params,
                })
                .then(response => {
                    const { data } = response
                    console.log(data)
                    this.items = data.items
                    this.totalItems = data.totalItems
                    this.totalPages = data.totalPages
                })
                .catch(error => {
                    alert(error)
                })
        },
    },
    created() {
        console.log(http)
        this.read()
    },
}
</script>

<style scoped>
.main {
    border: solid 5px #000;
    padding: 100px;
}
</style>