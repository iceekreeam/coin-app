<template>
    <section>
        <ul class="details">
            <li>Ask:{{ask}}</li>
            <li>Change:{{calculatedVal}}%</li>
        </ul>
    </section>
</template>

<script>
export default {
    props :['ask', 'calculatedVal']
}
</script>


<style scoped>
.details{
list-style-type: none;
}
</style>