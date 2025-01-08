<template>
    <button>
        <slot />
    </button>
</template>

<style lang="scss" scoped>
@mixin transition($duration: 0.15s) {
    transition-property: color, background-color, box-shadow;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: $duration;
}

button {
    display: inline-flex;
    align-items: center;

    padding: 0.5rem 1rem;

    border: 1px solid transparent;
    border-radius: 0.375rem;

    background-color: #dc2626;
    color: #ffffff;

    font-size: 0.75rem;
    line-height: 1rem;

    font-weight: 600;

    text-transform: uppercase;

    letter-spacing: 0.1em;
    
    @include transition;

    &:hover {
        background-color: #ef4444;
    }

    &:focus {
        outline: 2px solid transparent;
        outline-offset: 2px;

        box-shadow: 0 0 0 2px #ffffff, 0 0 0 4px #ef4444;
    }

    &:active {
        background-color: #b91c1c;
    }
}
</style>
