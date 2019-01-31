<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1> Builtin Directives</h1>
                <p v-text="'Aman'"></p>
                <p v-html="'<strong>Strong texts</strong>'"></p>
            </div>
        </div>
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Custom Directives</h1>

                <p v-text="'Aman'"></p>

                <p v-highlight>Highlighted text</p>

                <p v-makeHighlightColor="'red'">Highlighted text 2</p>

                <p v-makeHighlight:background="'blue'">Highlighted  background text 3</p>

                <p v-makeHighlight:background.delayed="'blue'">Delayed Highlighted background text 3</p>

                <p v-makeHighlight="'yellow'">Highlighted text 4</p>

                <p v-makeHighlight.delayed="'yellow'">Delayed Highlighted text 4</p>

                <p v-local-highlight="'lightsalmon'">Local Highlighted text 5</p>

                <p v-local-highlight.blink="'lightsalmon'">Local Highlighted text 6</p>

                <p v-local-highlight:background.blink="'red'">Local Highlighted blink text 7</p>

                <p v-local-highlight:background.blink.delayed="'red'">Local Highlighted blink delayed text 8</p>

            </div>
        </div>
    </div>
</template>

<script>
    export default {
        directives: {
            'local-highlight': {
                bind(el, binding, vnode) {

                    var delay = 0;
                    if (binding.modifiers['delayed']) {
                        delay = 3000;
                    }
                    if(binding.modifiers['blink']){
                        let mainColor=binding.value;
                        let secondColor='blue';
                        let currentColor=mainColor;

                        setTimeout(() => {

                            setInterval(()=>{
                                currentColor==secondColor ? currentColor=mainColor : currentColor=secondColor;

                                if (binding.arg == 'background') {
                                    el.style.backgroundColor = currentColor;
                                } else {
                                    el.style.color = currentColor;
                                }

                            }, 1000);

                        }, delay);
                    }
                    setTimeout(() => {

                        if (binding.arg == 'background') {
                            el.style.backgroundColor = binding.value;
                        } else {
                            el.style.color = binding.value;
                        }
                     }, delay);
                }
            }
        }
    }
</script>

<style>
.c{color: lightsalmon}
</style>
