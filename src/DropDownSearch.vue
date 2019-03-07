<template>
    <div v-bind:id="rootId" class="drop-down-block mb-3">
        <div class="input-group mb-3">
            <div class="input-group-prepend">
                <button class="btn btn-outline-secondary dropdown-toggle drop-down-block__button"
                        type="button" aria-haspopup="true" aria-expanded="false"
                        v-on:click="showList"
                >
                    {{ title }}
                </button>
            </div>
            <input type="text" class="form-control drop-down-block__input" placeholder="Search"
                   v-model="searchInput"
                   v-on:keyup="dNone = false"
            >
        </div>

        <div class="list-group drop-down-block__list drop-down-block__list_single"
             v-bind:class="{'d-none': dNone}"
             v-if="isMultiple == 'true'"
        >
            <button class="list-group-item list-group-item-action drop-down-block__item"
                    type="button"
                    v-for="channel in data"
                    v-on:click="$set(channel, 'selected', !channel.selected)"
                    v-bind:class="{active:channel.selected, 'd-none': match(channel.name)}"
                    v-bind:data-list-val="channel.code"
            >
                {{channel.name}}
            </button>
        </div>

        <div class="list-group drop-down-block__list drop-down-block__list_single"
             v-bind:class="{'d-none': dNone}"
             v-else
        >
            <button class="list-group-item list-group-item-action drop-down-block__item"
                    type="button"
                    v-for="channel in data"
                    v-on:click="activeClass = channel.code"
                    v-bind:class="{active:channel.code == activeClass, 'd-none': match(channel.name)}"
                    v-bind:data-list-val="channel.code"
            >
                {{channel.name}}
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "SomeTest",
        props: ['input', 'title', 'isMultiple', 'rootId'],

        data: function () {

            return {
                searchInput: '',
                data: this.input,
                dNone: true,
                activeClass: undefined,
                typing: ''
            }
        },

        methods: {
            showList: function () {
                this.dNone = !this.dNone;
            },
            match: function (targetString) {

                targetString = targetString.toLowerCase();

                var input = this.searchInput;

                input = input.toLowerCase();

                if (targetString.indexOf(input) >= 0) {

                    return false;
                } else {

                    return true;
                }
            },
        },

        watch: {
            typing: function () {
                console.log(this.searchInput);
            }
        },

        mounted() {

        }
    }
</script>

<style scoped>

</style>