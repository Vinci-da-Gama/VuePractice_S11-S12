<template>
    <ul>
        <li :class="{ active: modelValue === ratings[0] }">
            <button type="button" class="rating-btn" @click="activeRating(ratings[0])">Poor</button>
        </li>
        <li :class="{ active: modelValue === ratings[1] }">
            <button type="button" class="rating-btn" @click="activeRating(ratings[1])">Average</button>
        </li>
        <li :class="{ active: modelValue === ratings[2] }">
            <button type="button" class="rating-btn" @click="activeRating(ratings[2])">Great</button>
        </li>
    </ul>
</template>

<script>
    export default {
        props: {
            modelValue: {
                type: String,
                default: null
            },
        },
        emits: ['update:modelValue'],
        data() {
            return {
                ratings: ['poor', 'average', 'great'],
                activeOption: this.modelValue
            }
        },
        methods: {
            activeRating(opt) {
                // this.activeOption = opt;
                this.$emit('update:modelValue', opt);
            }
        },
    }
</script>

<style lang="scss" scoped>
ul {
    list-style: none;
    margin: 0.5rem 0;
    padding: 0;
    display: flex;
    > li {
        margin: 0 1rem;
        padding: 1rem;
        border: 1px solid #ccc;
        display: flex;
        justify-content: center;
        align-items: center;
    }
}
.rating-btn {
    font: inherit;
    border: none;
    background-color: transparent;
    cursor: pointer;
}
.active {
    border-color: #a00078;
    .rating-btn {
        color: #a00078;
    }
}
</style>