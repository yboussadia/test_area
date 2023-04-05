<script lang="ts" setup>
    const props = defineProps({
        id: Number,
        name: String,
        imageSrc: String
    })
</script>

<template>
    <RouterLink :to="`/shows/${props.id}`" class="show-item" >
        <img :src="props.imageSrc? `https://image.tmdb.org/t/p/original${props.imageSrc}` : `https://www.themoviedb.org/assets/2/v4/glyphicons/basic/glyphicons-basic-38-picture-grey-c2ebdbb057f2a7614185931650f8cee23fa137b93812ccb132b9df511df1cfac.svg`" :alt="`${props.name} cover`"/>
    </RouterLink>
</template>

<style lang="scss">
    .show-item {
        min-width: 140px;
        max-width: 140px;
        height: 197px;
        margin-right: var(--spacing);
        position: relative;

        img {
            /* Absolute for the popout effect on hover */
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 8px;
            transition: transform 0.2s;
        }

        &:hover {
            cursor: pointer;
            z-index: 100;
            box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px;

            img {
                transform: scale(1.1);
            }
        }

        @media screen and (min-width: 900px) {
            min-width: 200px;
            max-width: 200px;
            height: 280px;
        }
    }
</style>