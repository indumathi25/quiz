<template>
    <div>
        <b-nav tabs>
            <b-nav-item disabled>Fancy Quiz App</b-nav-item>
            <b-nav-item disabled>Counter: {{numCorrect}}/{{numTottal}}</b-nav-item>
        </b-nav>
    </div>
</template>


<script>
export default {
    props: [
        'numCorrect',
        'numTottal'
    ]
}
</script>