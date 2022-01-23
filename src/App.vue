<template>
    <div id="app">
        <div class="container">
            <form action="">
                <RadioGroup name="GROUP_1" legend="Группа 1" :items="group1" v-model="value1"/>

                <RadioGroup name="GROUP_2" :items="group2" v-model="value2">
                    <RadioItem name="GROUP_2" value="4" v-model="value2">Значение 4</RadioItem>
                </RadioGroup>

                <RadioGroup name="GROUP_3" :items="group3" v-model="value3" :disabled="!group3Active"/>
                <b-button class="mt-3" variant="primary" size="sm" @click="toggleGroup3" style="margin-left: 30px">{{group3Active ? 'Деактивировать' : 'Активировать'}} группу 3</b-button>

                <fieldset class="check-group -radio">
                    <RadioItem name="GROUP_4" value="1" v-model="value4">Значение 1</RadioItem>
                    <RadioItem name="GROUP_4" value="2" :checked="true" v-model="value4">Значение 2</RadioItem>
                </fieldset>

                <fieldset class="check-group">
                    <div>Значение группы 1: <strong>{{value1}}</strong></div>
                    <div>Значение группы 2: <strong>{{value2}}</strong></div>
                    <div>Значение группы 3: <strong>{{value3}}</strong></div>
                    <div>Значение группы 4: <strong>{{value4}}</strong></div>
                </fieldset>
            </form>
        </div>
    </div>
</template>

<script>
import RadioGroup from '@/components/RadioGroup';
import RadioItem from '@/components/RadioItem';

export default {
    name: 'App',

    components: {
        RadioGroup,
        RadioItem
    },

    data() {
        return {
            value1: '',
            value2: '',
            value3: '',
            value4: '2',

            group1: [
                {
                    content: 'Значение 1',
                    value: '1'
                },
                {
                    content: 'Значение 2',
                    value: '2'
                },
                {
                    content: 'Значение 3',
                    value: '3'
                }
            ],
            group2: [
                {
                    content: 'Значение 1',
                    value: '1'
                },
                {
                    content: 'Значение 2',
                    value: '2'
                },
                {
                    content: 'Значение 3',
                    value: '3'
                }
            ],
            group3: [
                {
                    content: 'Значение 1',
                    value: '1'
                },
                {
                    content: 'Значение 2',
                    value: '2'
                },
                {
                    content: 'Значение 3',
                    value: '3'
                }
            ],

            group3Active: false
        };
    },

    created() {
        this.value1 = this.group1[0].value;
        this.value2 = this.group2[1].value;
        this.value3 = this.group3[2].value;
    },

    methods: {
        toggleGroup3() {
            this.group3Active = !this.group3Active;
        }
    }
};
</script>

<style lang="scss">
*,
*::before,
*::after{
    box-sizing: border-box;
}
html,
body{
    min-height: 100vh;
}
body{
    margin: 0;
}

#app{
    width: 100%;
    min-height: 100vh;
    padding: 10px 0 40px;
}

.container{
    max-width: 1366px;
    padding: 0 20px;
}

.disabled{
    pointer-events: none;
    cursor: default;
    opacity: .65;
}
.loading{
    min-width: 100%;
    text-align: center;
}
</style>
