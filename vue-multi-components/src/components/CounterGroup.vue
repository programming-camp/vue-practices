<template>
    <div class="counter-group">
        <h2>
            Counter Number:
            <span>{{counterNumber}}</span>
        </h2>
        <div class="counters">
            <Counter
                    v-for="(counter,index) in counters"
                    :index="index"
                    :value="counter.value"
                    :key="index"
                    @update="handleValueChange"
            />
        </div>
        <CounterSum :counterSum="counterSum"></CounterSum>
    </div>
</template>

<script>
    import Counter from './Counter.vue'
    import CounterSum from './CounterSum.vue'

    export default {
        name: 'counter-group',
        components: {
            Counter,
            CounterSum
        },
        props: {
            counterNumber: Number
        },
        computed: {
            counterSum: function () {
                let sum = 0;
                this.counters.forEach(element => {
                    sum = sum + element.value;
                });
                return sum;
            }
        },
        created: function () {
            // 根据 counterNumber 生成 counter 数据和组件
            for (let i = 0; i < this.counterNumber; i++) {
                this.counters.push({
                    value: 0
                });
            }
        },
        methods: {
            handleValueChange: function (index, value,) {
                this.counters[index].value = value;
            }
        },
        data: function () {
            return {
                counters: []
            }
        }
    }
</script>
