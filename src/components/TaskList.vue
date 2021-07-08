<template>
    <draggable
            v-bind="dragOptions"
            v-model="tasks"
            tag="transition-group"
            :component-data="{
                tag: 'ul',
                type: 'transition-group',
                name: !drag ? 'flip-list' : null
            }"
            item-key="id"
            @start="drag = true"
            @end="drag = false"
        >
            <template #item="{element}">
                <li class="text-gray-700 list-group-item py-2 w-36 bg-yellow-400 pl-2 my-1 rounded">
                    {{ element.title }}
                </li>
            </template>
        </draggable>
</template>
<script>
import draggable from 'vuedraggable';

const tasks = [    
    {title: 'task 1', id: 1},
    {title: 'task 2', id: 2},
    {title: 'task 3', id: 3},
    {title: 'task 4', id: 4},
    {title: 'task 5', id: 5}
];

export default ({
    display: "Transitions",
    id: 6,
    data() {
        return {
            tasks: tasks,
            drag: false
        }
    },
    components: {
        draggable
    },
    computed: {
        dragOptions() {
            return {
                animation: 200,
                group: "description",
                disabled: false,
                ghostClass: "ghost"
            };
        }
    }
})
</script>
<style scoped>
.flip-list-move {
    transition: transform 0.5s;
}
.no-move {
    transition: transform 0s;
}
.ghost {
    opacity: 0.5;
    background: #c8ebfb;
}
.list-group {
    min-height: 20px;
}
.list-group-item {
    cursor: move;
}
</style>