<script setup lang="ts">
import { ref } from 'vue';
import FormInput from './FormInput.vue';
import FormSelect from './FormSelect.vue';

const inputFieldMap = {
  input: FormInput,
  select: FormSelect
} 

const data = {
  'some-table-control-question-id': [
    {
      question1: 'answer1',
    },
    {
      question2: 'answer2',
    }
  ]
}

// const stuff = [{questiondid: "sjdfdsjkfjksf", question2: "value",....}, {questiondid: "sjdfdsjkfjksf", question2: "value",....}]

const backendComponents = ref(
  [
    { 
      components: [{ component: 'input' , value: '', name: 'name'}, { component: 'select', value: '', name: 'vehicle'}]
    },
    { 
      components: [{ component: 'input' , value: '', name: 'name'}, { component: 'select', value: '', name: 'vehicle'}]
    }
  ]
)

function addItem () {
  backendComponents.value.push({ components: [ { component: 'input' , value: '', name: 'name'}, { component: 'select', value: '', name: 'vehicle'}] })
}

function moveItemUp (components: any) {
  const index = backendComponents.value.indexOf(components)
  if (index > 0 ) {
    backendComponents.value.splice(index, 1);
    backendComponents.value.splice(index - 1, 0, components)
  }
}

function moveItemDown (components: any) {
  const index = backendComponents.value.indexOf(components)
  if (index < backendComponents.value.length - 1) {
    backendComponents.value.splice(index, 1);
    backendComponents.value.splice(index + 1, 0, components); 
  }
}

function removeItem (components: any) {
  const index = backendComponents.value.indexOf(components)
  backendComponents.value.splice(index, 1);
}
</script>

<template>
  <div v-for="(components, index) in backendComponents" :key="index" class="mb-8">
    <div v-for="(componentList, i) in components.components" :key="i" class="mb-4">
      <component :is="inputFieldMap[componentList.component as keyof typeof inputFieldMap]" v-model="componentList.value" />
    </div>
    <button class="btn btn-primary" @click="moveItemUp(components)">&#8593;</button>
    <button class="btn btn-secondary mr-4 ml-4" @click="removeItem(components)">Remove Element </button>
    <button class="btn btn-primary" @click="moveItemDown(components)">&#8595;</button>
  </div>

  <button class="btn btn-accent" @click="addItem()">Add Element </button>

</template>
