
<template>
    <div>
        <button v-if="type == 'default'" :id="'dropdownButton' + dropKey" :data-dropdown-toggle="'dropdown' + dropKey"
            class="bg-teddy-brow text-white font-medium rounded-lg text-sm px-5 py-2.5 text-center inline-flex items-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
            type="button">
            <i :class="iconClass"></i>
            <span class="px-4">{{ newLabel }} </span>
        </button>

        <button style="width: 300px; text-wrap: nowrap; overflow: hidden;" v-if="type == 'thin'" :id="'dropdownButton' + dropKey"
            :data-dropdown-toggle="'dropdown' + dropKey"
            class="border-teddy-brow text-teddy-brow font-medium rounded-lg text-sm px-10 py-1 text-center inline-flex items-center"
            type="button">
            <i :class="iconClass"></i>
            <span class="px-4">{{ newLabel }} </span>
        </button>

        <!-- Dropdown content-->
        <div v-if="dropType==1" :id="'dropdown' + dropKey"
            class="z-10 hidden bg-yellow-50 divide-y divide-gray-100 rounded-lg shadow w-44 dark:bg-gray-700">
            <ul class="py-2 text-sm text-gray-700 dark:text-gray-200" aria-labelledby="dropdownDefaultButton">
                <li v-for="(item, index) in list" :key="'drop1' + dropKey + index">
                    <a :href="'?subject=' + item.code" @click="setLabel(item.name)"
                        class="block px-4 py-2 hover:bg-yellow-100">
                        {{ item.name }}
                    </a>
                </li>
            </ul>
        </div>
        <div v-if="dropType==2" :id="'dropdown' + dropKey"
            style="width: 300px;"
            class="z-10 hidden bg-yellow-50 divide-y divide-gray-100 rounded-lg shadow w-44 dark:bg-gray-700">
            <ul class="py-2 text-sm text-gray-700 dark:text-gray-200" aria-labelledby="dropdownDefaultButton">
                <li v-for="(item, index) in list" :key="'drop2' + dropKey + index">
                    <a @click="setLabel(item.content)"
                       class="block px-4 py-2 hover:bg-yellow-100">
                       {{ item.content }}
                    </a>
                </li>
            </ul>
        </div>

    </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';

export default {
    name: "DropdownComp",
    computed: {
        dropKey() {
            return uuidv4();
        }
    },
    data() {
        return {
            newLabel: ""
        }
    },
    props: {
        label: "",
        iconClass: "",
        list: [],
        type: {
            type: String,
            default: "default"
        },
        dropType: {
            type: Number,
            default: 1
        },
        toLink: true,
    },
    mounted() {
        this.newLabel = this.label
    },
    methods: {
        setLabel(str) {
            this.newLabel = str;
            this.$emit("change_value", str);
        }
    }
}
</script>