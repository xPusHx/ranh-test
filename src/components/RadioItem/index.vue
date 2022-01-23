<template>
    <div class="form-check" :class="`-${type}`">
        <label class="form-check__label form-check-label" :for="(id !== '') ? id : null">
            <input
                class="form-check__input form-check-input"
                :type="type"
                :value="value"
                :name="name"
                :id="id"
                v-model="stateChecked"
                :disabled="disabled"
                @change="change">
            <span class="form-check__content form-check-content">
                <slot></slot>
            </span>
        </label>
    </div>
</template>

<script>
export default {
    name: 'RadioItem',

    model: {
        prop: 'checked',
        event: 'change'
    },

    props: {
        type: {
            type: String,
            default: 'radio'
        },
        name: {
            type: String,
            default: ''
        },
        value: {
            type: String,
            default: ''
        },
        checked: {
            type: String,
            default: ''
        },
        id: {
            type: String,
            default: ''
        },
        disabled: {
            type: Boolean,
            default: false
        },
    },

    computed: {
        stateChecked: {
            get() {
                return this.checked;
            },
            set() {
                //
            }
        },
        stateDisabled() {
            return this.disabled;
        }
    },

    watch: {
        stateChecked() {
            this.$emit('change', this.stateChecked);
            this.$parent.$emit('input', this.stateChecked);
        }
    },

    methods: {
        change() {
            this.$emit('change', this.value);
            this.$parent.$emit('input', this.value);
        }
    }
};
</script>

<style lang="scss">
$color-primary: #2f76d6;
$input-check-size: 16px;

.form-check{
    position: relative;
    display: block;
    font-size: 14px;
    line-height: 1.1;
    padding-left: 0;
    &-input{
        position: absolute;
        top: 0;
        left: 0;
        width: $input-check-size;
        height: $input-check-size;
        opacity: 0;
        margin: 0;
        outline: none !important;
        -webkit-appearance: none;
        -moz-appearance: none;
        &:disabled,
        &.disabled{
            ~ .form-check-content{
                cursor: default !important;
                opacity: .2 !important;
                user-select: none;
                pointer-events: none;
            }
        }
        &:not(:disabled):not(.disabled){
            ~ .form-check-content{
                &:hover,
                &:focus{
                    &::before{
                        border-color: $color-primary;
                    }
                }
            }
            ~ .form-check-label{
                &:hover,
                &:focus{
                    ~ .form-check-content{
                        &::before{
                            border-color: $color-primary;
                        }
                    }
                }
            }
        }
        &:focus{
            ~ .form-check-content{
                &::before{
                    border-color: $color-primary;
                }
            }
        }
        &:checked{
            ~ .form-check-content{
                &::after{
                    border-width: 5px !important;
                }
            }
        }
    }

    &-label{
        position: relative;
        display: block;
        margin: 0;
        padding: 0;
    }

    &-content{
        position: relative;
        display: block;
        padding: 6px 0 6px $input-check-size + 12;
        cursor: pointer;
        &::before,
        &::after{
            content: '';
            position: absolute;
            transition-duration: .25s;
            transition-timing-function: ease-in-out;
        }
        &::before{
            top: 6px;
            left: 0;
            width: $input-check-size;
            height: $input-check-size;
            border: 1px solid #dce4ed;
        }
        &::after{
            transition-property: top, height, border-width, opacity;
        }
        &:empty{
            width: $input-check-size;
            height: $input-check-size;
            padding: 0;
            &::before{
                top: 0;
            }
        }
    }

    &.-checkbox{
        .form-check{
            &-content{
                &::before{
                    border-radius: 2px;
                    transition-property: border-color;
                }
                &::after{
                    top: 6px;
                    left: 3px;
                    width: 10px;
                    height: 10px;
                    margin-top: 3px;
                    border: 0 solid $color-primary;
                    border-radius: 2px;
                }
                &:empty{
                    &::after{
                        top: 0;
                    }
                }
            }
            &-icon{
                svg{
                    margin-bottom: 2px;
                }
            }
        }
    }

    &.-radio{
        .form-check{
            &-input{
                &:checked{
                    ~ .form-check-content{
                        &::before{
                            border-color: $color-primary;
                            background: $color-primary;
                        }
                        &::after{
                            border-width: 3px !important;
                        }
                    }
                }
            }
            &-content{
                &::before{
                    border-radius: 50%;
                    transition-property: border-color, background;
                }
                &::after{
                    top: 6px + 5;
                    left: 5px;
                    border: 0 solid #fff;
                    width: 6px;
                    height: 6px;
                    border-radius: 50%;
                }
                &:empty{
                    &::after{
                        top: 5px;
                    }
                }
            }
        }
    }
}
</style>