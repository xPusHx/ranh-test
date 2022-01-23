<template>
    <fieldset class="check-group -radio" :disabled="stateDisabled">
        <RadioItem
            v-for="(item, index) in items"
            :value="item.value"
            :checked="item.value"
            :name="name"
            :id="item.id || `${name}-${index}`"
            :disabled="stateDisabled"
            :key="item.value"
            @input="input">{{item.content}}</RadioItem>

        <slot></slot>
    </fieldset>
</template>

<script>
import RadioItem from '@/components/RadioItem';

export default {
    name: 'RadioGroup',

    components: {
        RadioItem
    },

    props: {
        name: {
            type: String,
            required: true
        },
        legend: {
            type: String,
            default: ''
        },
        items: {
            type: Array,
            default() {
                return [];
            }
        },
        value: {
            type: String,
            default: ''
        },
        disabled: {
            type: Boolean,
            default: false
        }
    },

    data() {
        return {
            stateValue: this.value
        };
    },

    computed: {
        stateDisabled() {
            return this.disabled;
        }
    },

    methods: {
        input(value) {
            this.stateValue = value;
            this.$emit('input', value);
        }
    }
};
</script>

<style lang="scss">
.check-group{
    padding: 20px 30px;
    border-radius: 20px;
    border: 1px solid #f0f3f7;
    margin-top: 20px;
}
</style>