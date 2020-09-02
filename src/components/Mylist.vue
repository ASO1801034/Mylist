<template>
    <div class="Mylist">
        <h1>{{ title }}</h1>
        <p>{{ message  }}</p>
        <div><textarea v-model="fomula"
            cols="40" rows="1"></textarea></div>
        <div><button v-on:click="doAction">クリック</button></div>
    </div>
</template>

<script>
export default {
    name: 'Mylist',
    props {
        title: String,
    },
    data:function(){
        return {
            message: 'Enter expression',
        };
    },
    method:{
        doAction: function() {
            var arr = this.fomula.trim().split('\n');
            var last = arr.pop();
            var fn = '';
            for(var n in arr){
                if(arr[n].trim() != ''){
                    fn += 'var' + arr[n] + ';';
                }
            }
            fn += 'return ' + last + ';';
            var exp = 'function f(){' + fn + '} f();';
            var ans= eval(exp);
            var re = arr.join(';').trim();
            if (re != ''){ re += ';' }
            re += last;
            this.$emit('result-event',re);
        }
    }
}