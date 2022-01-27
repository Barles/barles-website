<script lang="ts">
import { onMount } from "svelte";
import Prism from "../libs/prismjs";
import { Variant } from "../design-system/types";

import Button from "../design-system/Button.svelte";

let code = `console.log('Hello world')`;
let language = 'html';

interface Btn {
    block: boolean;
    text: string;
    variant: Variant;
    disabled: boolean;
}

const btns: Btn[] = []

Object.keys(Variant).forEach(element => {
    btns.push({
        block: true,
        text: Variant[element],
        variant: Variant[element],
        disabled: false
    })    
});
</script>

<div class="container">
    <div class="container-header">
        Buttons
    </div>
    <div class="container-def">
        <pre>
            <code>
                {@html Prism.highlight('<Button\n  {block}\n  {text}\n  {variant}\n  {disabled}\n/>', Prism.languages[language])}
            </code>
        </pre>
    </div>
    <div class="container-body">
        {#each btns as { block, text, variant, disabled }}
        <div class="btn">
            <div class="btn-header">
                Variant <code>{variant}</code>
            </div>
            <div class="btn-container">
                <input bind:value={text} type="text" />
                <label>
                    <input type="checkbox" bind:checked={disabled} />
                    Disabled
                </label>
                <label>
                    <input type="checkbox" bind:checked={block} />
                    Block
                </label>
                <Button {block} {text} {variant} {disabled} on:click={() => alert(`Button ${variant} clicked`)} />
            </div>
        </div>
        {/each}
    </div>
</div>

<style lang="scss">
.container {
    width: 75vw;
    display:flex;
    margin:auto;
    flex-direction: column;
    box-shadow: 1px 1px 10px black;
    border-radius: 10px;
    overflow: hidden;
    
    &-header {
        background-color: #222;
        padding: 15px;
        font-weight: bold;
        font-size: 18px;
        color: white;
    }
    &-body {
        background-color: #444;
        display: flex;
        justify-content: space-around;
        padding-top: 25px;
        padding-bottom: 25px;
    }
    &-def {
        display: flex;
        background-color: #444;
        justify-content: center;
        
        & > pre {
            background-color: white;
            width: 100%;
            padding: 15px;
            margin: 0;
        }
    }
}
.btn {
    width: 20%;
    display: flex;
    flex-direction: column;
    box-shadow: 1px 1px 10px #222;

    &-header {
        background: #555;
        padding: 10px;
        color: white;
        text-align: center;
        & > code {
            font-weight: bold;
            font-size: 16px;
        }
        border-radius: 5px 5px 0 0;
    }
    &-container {
        background-color: #777;
        padding: 10px;
        & input[type=text] {
            width: 100%;
        }
        border-radius: 0 0 5px 5px;
    }
}
</style>