<script setup lang="ts">
export interface Props {
  label?: string
  id?: string
  modelValue: string,
  hint?: string,
  options?: Array<{ value: string, name: string }>
}

withDefaults(defineProps<Props>(), {
  label: "Select values",
  id: "select",
  modelValue: "",
  options: () => [{ value: "sam", name: "test" }, { value: "mwas", name: "audi"}]
})

defineEmits<{ (e: "update:modelValue", value: string): void }>();
</script>

<template>
  <div class="form-input grid">
    <label :for="id">{{ label }}</label>
    <small v-if="hint">{{ hint }}</small>
    <select :value="modelValue" :name="id" :id="id" @change="(event) => $emit('update:modelValue', ((event.target) as HTMLInputElement).value)" class="select select-accent w-full max-w-xs">
      <option value="- select -">- select -</option>
      <option v-for="(option, index) in options" :key="index" :value="option.value">{{ option.name }}</option>
    </select>
  </div>
</template>