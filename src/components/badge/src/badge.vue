<template>
    <span class="yd-badge" :class="typesClass"
          :style="{backgroundColor: bgcolor, color: color, transform: 'scale('+scale+')'}" @click='click'>
        <slot></slot>
    </span>
</template>

<script type="text/babel">
    import {isColor} from '../../../utils/assist';

    export default {
        name: 'yd-badge',
        props: {
            type: {
                validator(value) {
                    return ['primary', 'danger', 'warning', 'hollow'].indexOf(value) > -1;
                }
            },
            shape: {
                validator(value) {
                    return ['circle', 'square'].indexOf(value) > -1;
                }
            },
            color: {
                validator(value) {
                    if(!value) return true;
                    return isColor(value);
                }
            },
            bgcolor: {
                validator(value) {
                    if(!value) return true;
                    return isColor(value);
                }
            },
            scale: {
                validator(val) {
                    return /^(\d*(.\d+)?)$/.test(val);
                },
                default: 1
            }
        },
        computed: {
            typesClass() {
                if (this.bgcolor) {
                    if (this.shape === 'square') {
                        return ' yd-badge-radius';
                    }
                    return '';
                }
                return (this.type ? 'yd-badge-' + this.type : '') + (this.shape === 'square' ? ' yd-badge-radius' : '');
            }
        },
        methods:{
            click(){
                 this.$emit('click', event);
            }
        }
    }
</script>

<style lang="less">
    @import '../../../styles/components/badge.less';
</style>
