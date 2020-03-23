<template>
    <div id="quiz">
        <div id="question">Question</div>
        <div id="options">Options</div>
    </div>
</template>
<script>
export default {
    name: "Quiz"
}
</script>
<style scoped lang="scss">
    #quiz{
        background: red;
        width: 100vw;
        height: 100vh;
        display: flex;
        flex-direction: column;;
        justify-content: center;
        align-items: center;
    }
    #question{
        background: lime;
        width: 50vw;
        height: 30vh;
    }
    #options{
        background: purple;
        width: 50vw;
        height: 20vh;
    }
</style>