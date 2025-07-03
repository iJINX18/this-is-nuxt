<template>
    <div class = 'summaryColor'>
        <b>Tasks Summary</b>
        <p>To do: {{ statusSummary['To do'] || 0 }}</p>
        <p>On going: {{ statusSummary['On going'] || 0 }}</p>
        <p>Completed: {{ statusSummary['Completed'] || 0 }}</p>
    </div>
</template>
<script setup>
const props = defineProps({
statusSummary : Number
})
</script>
<style scoped>
.summaryColor{
    background-color:aquamarine;
    text-align: left;
}
</style>