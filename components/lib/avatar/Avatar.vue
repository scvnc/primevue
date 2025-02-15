<template>
    <div :class="containerClass" :aria-labelledby="ariaLabelledby" :aria-label="ariaLabel">
        <slot></slot>
        <template v-if="!$slots.default">
            <span v-if="label" class="p-avatar-text">{{ label }}</span>
            <component v-else-if="$slots.icon" :is="$slots.icon" class="p-avatar-icon" />
            <span v-else-if="icon" :class="['p-avatar-icon', icon]" />
            <img v-else-if="image" :src="image" :alt="ariaLabel" @error="onError" />
        </template>
    </div>
</template>

<script>
export default {
    name: 'Avatar',
    emits: ['error'],
    props: {
        label: {
            type: String,
            default: null
        },
        icon: {
            type: String,
            default: null
        },
        image: {
            type: String,
            default: null
        },
        size: {
            type: String,
            default: 'normal'
        },
        shape: {
            type: String,
            default: 'square'
        },
        'aria-labelledby': {
            type: String,
            default: null
        },
        'aria-label': {
            type: String,
            default: null
        }
    },
    methods: {
        onError() {
            this.$emit('error');
        }
    },
    computed: {
        containerClass() {
            return [
                'p-avatar p-component',
                {
                    'p-avatar-image': this.image != null,
                    'p-avatar-circle': this.shape === 'circle',
                    'p-avatar-lg': this.size === 'large',
                    'p-avatar-xl': this.size === 'xlarge'
                }
            ];
        }
    }
};
</script>

<style>
.p-avatar {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 2rem;
    height: 2rem;
    font-size: 1rem;
}

.p-avatar.p-avatar-image {
    background-color: transparent;
}

.p-avatar.p-avatar-circle {
    border-radius: 50%;
}

.p-avatar-circle img {
    border-radius: 50%;
}

.p-avatar .p-avatar-icon {
    font-size: 1rem;
}

.p-avatar img {
    width: 100%;
    height: 100%;
}
</style>
