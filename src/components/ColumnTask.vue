<template>
  <AppDrop @drop="moveTaskOrColumn">
    <app-drag
      class="task"
      :transferData="{
        type: 'task',
        fromColumnIndex: columnIndex,
        fromTaskIndex: taskIndex,
      }"
      @click="goToTask(task)"
    >
      <span class="w-full flex-no-shrink font-bold">
        {{ task.name }}
      </span>
      <p v-if="task.description" class="w-full flex-no-shrink mt-1 text-sm">
        {{ task.description }}
      </p>
    </app-drag>
  </AppDrop>
</template>

<script>
import movingTasksAndColumnMixin from "@/mixins/movingTasksAndColumnMixin.js";
import AppDrag from "./AppDrag.vue";
import AppDrop from "./AppDrop.vue";
export default {
  components: { AppDrag, AppDrop },
  mixins: [movingTasksAndColumnMixin],
  props: {
    task: {
      type: Object,
      required: true,
    },
    taskIndex: {
      type: Number,
      required: true,
    },
  },
  methods: {
    goToTask(task) {
      this.$router.push({ name: "task", params: { id: task.id } });
    },
  },
};
</script>

<style lang="css" scoped>
.task {
  @apply flex items-center flex-wrap shadow mb-2 py-2 px-2 rounded bg-white text-grey-darkest no-underline;
}
</style>
