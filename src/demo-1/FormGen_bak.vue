<script setup>
import { reactive, ref, inject } from "vue";
import { FORM_MODEL } from "./constants.js";
import useParsedSchema from "./useParsedSchema.js";
import FormField from "./FormField.vue";
import FieldRow from "./FieldRow.vue";

const props = defineProps(["schema"]);
const emits = defineEmits([
  "update:modelValue",
  "update:formValue",
]);
const formData = inject(FORM_MODEL);
const { parsedSchema } = useParsedSchema(
  props.schema
);
function removeField(fieldName) {
  delete formData.value[fieldName];
}

function doSomething(x, y, z) {
  console.log({ x, y, z });
}
</script>
<template>
  <FieldRow
    v-for="row in parsedSchema"
    :row="row"
    @update:modelValue="doSomething"
  />
</template>

<style>
.schema-row {
  display: flex;
}
</style>
