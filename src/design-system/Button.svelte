<script lang="ts">
import { createEventDispatcher } from 'svelte'
import { Variant } from './types/index'

const dispatch = createEventDispatcher()

export let text: string = '';
export let disabled: boolean = false;
export let variant: Variant = Variant.Primary
export let block: boolean = false;

const handleClick = () => {
    if (!disabled)
        dispatch('click')
}

</script>

<button class={`${variant} ${block && 'block'}`} type="button" {disabled} on:click={handleClick}>
    <span>{text}</span>
</button>

<style lang="scss">
$primary: #1234ff;
$secondary: #12ff34;
$light: #bbb;
$dark: #333;

@mixin custom_btn($color) {
    min-width: 75px;
    border: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 10px;
    margin: 0;
    padding-bottom: 7px;
    padding-top: 5px;
    cursor: pointer;
    border-radius: 5px;
    border: 2px solid;

    transition: all .3s;

    background-color: $color;
    color: white;
    border-color: darken($color, 10%);
    &:hover, &:active {
        background-color: darken($color, 10%);
        
        transition: all .3s;
    }
    &:disabled {
        background-color: lighten($color, 25%);
        border-color: lighten($color, 25%);
        color: #ccc;
        cursor: default;

        transition: all .3s;
    }
    &.block {
        width: 100%;
    }
    & > span {
        width: 100%;
        height: 100%;
        overflow: hidden;
        text-overflow:ellipsis;
    }
}

.secondary { @include custom_btn($secondary); }
.primary { @include custom_btn($primary); }
.light { @include custom_btn($light); }
.dark { @include custom_btn($dark); }

</style>