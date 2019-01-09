<template>
    <div id="app">
        <xl-autocomplete :data="lists" v-model="lp" @select="select" @query="query"></xl-autocomplete>
    </div>
</template>

<script>
    import XlAutocomplete from "./XlAutocomplete";

    export default {
        name: "App",
        components: {
            XlAutocomplete
        },
        data() {
            return {
                lp: "",
                lists: [
                    {
                        id: 1,
                        name: "tom"
                    },
                    {
                        id: 2,
                        name: "jack"
                    }
                ]
            };
        },
        methods: {
            gets() {
                alert(this.lp);
            },
            select(val) {
                console.log(val);
            },
            query(val) {
                if (!val) {
                    this.lists = [];
                    return;
                }
                let r = ~~(Math.random() * 10), arr = [];
                for (let i = 0; i < r; i++) {
                    arr.push({
                        id: ~~(Math.random() * 100),
                        name: this.lp + ~~(Math.random() * 100)
                    })
                }
                this.lists = arr;
            }
        }
    }
</script>

<style scoped>

</style>

