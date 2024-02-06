
<template>
    <div>
        <button :id="'dropdownButton' + dropKey" :data-dropdown-toggle="'dropdown' + dropKey"
            class="bg-teddy-brow text-white font-medium rounded-lg text-sm px-5 py-2.5 text-center inline-flex items-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
            type="button">
            <i :class="iconClass"></i>
            <span class="px-4">{{ label }} </span>
        </button>

        <div :id="'dropdown' + dropKey" class="z-10 hidden bg-yellow-50 divide-y divide-gray-100 rounded-lg shadow w-44 dark:bg-gray-700">
            <ul class="py-2 text-sm text-gray-700 dark:text-gray-200" aria-labelledby="dropdownDefaultButton">
                <li v-for="(item, index) in list" :key="dropKey + index">
                    <a :href="item.link"
                        class="block px-4 py-2 hover:bg-yellow-100">
                        {{ item.name }}
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
    props: {
        label: "",
        iconClass: "",
        list: []
    }
}
</script>