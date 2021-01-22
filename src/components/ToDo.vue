<template>
<li>{{todo.text}}</li>
</template>

<script>
export default {
    name: 'ToDo',
    props: {
        todo: {
            type: Object,
            default: () => {
                return {}
            }
        }
    }
}
</script>

<style langs="scss" scoped>
</style>
