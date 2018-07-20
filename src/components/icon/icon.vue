<template>
    <i :class="classes" :style="styles" @click="handleClick"></i>
</template>
<script>
    const prefixCls = 'ivu-icon';

    export default {
        name: 'Icon',
        props: {
            env: {
                type: String,
                validator(value) {
                    if (['ios', 'md'].includes(value)) {
                        return true;
                    }
                    console.warn('Icon组件只具有ios和md两种env');
                    return false;
                },
                default: 'ios'
            },
            type: {
                type: String,
                default: ''
            },
            size: [Number, String],
            color: String,
            custom: {
                type: String,
                default: ''
            }
        },
        computed: {
            classes() {
                return [
                    `${prefixCls}`,
                    {
                        [`${prefixCls}-${this.env}-${this.type}`]: this.type !== '',
                        [`${this.custom}`]: this.custom !== '',
                    }
                ];
            },
            styles() {
                let style = {};

                if (this.size) {
                    style['font-size'] = `${this.size}px`;
                }

                if (this.color) {
                    style.color = this.color;
                }

                return style;
            }
        },
        methods: {
            handleClick(event) {
                this.$emit('click', event);
            }
        }
    };
</script>
