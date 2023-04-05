<script lang="ts" setup>
import { defineProps } from 'vue';
import ShowItem from './ShowItem.vue';

interface Movie {
  id: number;
  title: string;
  poster_path: string;
  // Add any other properties you need here
}


const props = defineProps({ items: Array})
console.log(props.items)
</script>

<template>
    <div class="show-list">
        <slot></slot>

        <div class="items">
            <ShowItem 
                v-for="item in props.items"
                :key="item.id"
                :id="item.id"
                :name="item.title"
                :image-src="item.poster_path"
            />
        </div>
        <p class="scroll-hint">Scroll for more &rarr;</p>
    </div>
</template>

<style lang="scss">
.shows-list {
  margin-bottom: calc(var(--spacing) * 3);
}
.items {
  display: flex;
  overflow-x: auto;
  padding: calc(var(--spacing) * 3) var(--spacing);
  margin-left: -8px;
}
.items::-webkit-scrollbar {
  display: none;
}
.scroll-hint {
  text-align: right;
}
</style>