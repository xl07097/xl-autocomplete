<template>
    <div class="about">
        <div class="xl-warpper">
            <input
                    class="xl-input"
                    v-model.trim="v"
                    @focus="focus"
                    :placeholder="placeholder"
                    @blur="blur"
                    @input="input"
                    :maxLength="maxlength"
                    autocomplete="off"
            >
            <input type="hidden" :value="value">
            <ul class="xl-list" :class="{active:flag}">
                <li
                        v-for="(item, index) of data"
                        :key="index"
                        @click="selected(item, index)"
                >{{item[label]}}</li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        name: "XlAutocomplete",
        props: {
            data: {
                type: Array,
                default: function() {
                    return [];
                }
            },
            label: {
                type: String,
                default: "name"
            },
            placeholder: {
                type: String,
                default: "请输入"
            },
            maxlength: {
                type: Number,
                default: 20
            }
        },
        data() {
            return {
                v: "",
                flag: false,
                value: ""
            };
        },
        methods: {
            input() {
                this.$emit("input", this.v);
                this.$emit("query", this.v);
            },
            focus() {
                this.flag = true;
            },
            blur() {
                setTimeout(() => {
                    this.flag = false;
                }, 150);
            },
            selected(val, index) {
                this.v = val.name;
                this.value = index;
                this.$emit("input", val.name);
                this.$emit("select", val);
            }
        },
        watch: {
            data: {
                handler(newVal, oldVal) {
                    if (Array.isArray(newVal)) {
                    } else {
                        return [];
                    }
                },
                deep: true
            }
        }
    }
</script>


<style scoped>
    .about {
        text-align: center;
    }
    .xl-warpper {
        position: relative;
        display: inline-block;
        text-align: left;
    }
    .xl-list {
        position: absolute;
        display: none;
        margin-top: 5px;
        padding: 8px 0;
        width: 100%;
        max-height: 220px;
        overflow: auto;
        transition: opacity 0.6s;
        list-style-type: none;
        border-radius: 4px;
        box-shadow: 0 1px 6px rgba(0, 0, 0, 0.2);
        box-sizing: border-box;
        opacity: 0;
    }
    .xl-list li {
        padding: 7px 16px;
        font-size: 12px;
        cursor: pointer;
    }
    .xl-list li:hover {
        background: #f3f3f3;
    }
    .xl-list.active {
        display: block;
        opacity: 1;
    }
    .xl-input {
        height: 34px;
        padding: 6px 8px;
        line-height: 20px;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
    }
    .xl-input::-webkit-input-placeholder {
        color: #ccc;
    }
    .xl-input:-moz-placeholder {
        /* Firefox 18- */
        color: #ccc;
    }
    .xl-input::-moz-placeholder {
        /* Firefox 19+ */
        color: #ccc;
    }
    .xl-input:-ms-input-placeholder {
        color: #ccc;
    }
</style>


