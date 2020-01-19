# vue-selectposition
 position selection component for Vue and/or Framework7

![screenshot](https://user-images.githubusercontent.com/1894723/72679136-85b15a00-3aac-11ea-872e-7fddad2f0328.png)

None Vue version: [jsFiddle](https://jsfiddle.net/BananaAcid/fuzw8dmy/)

## usage
```html
<template>
    <select-position @changed="doValue" :static="true" :preselected="initialValue" size="25px" />
</template>

<script>
    import selectposition from 'selectPosition';
    Vue.component('select-position', selectposition);
</script>
```

- @changed (fn(val)) - event triggered on tapping an area, that gets the same value passed as `preselected`
- static (bool) - disables interaction
- preselected ('tl', 'tr', 'bl', 'br', 'cc') - what area is selected (is like :value on other elements)
  - control updates if value changes
- size (css value) - defines the size, is set for height and width to be square



## important
if you do not use Framework7, you need to overwrite the color variables in a style block (they are prefilled with F7 definitions).

## color definition
```css
[data-selectpostion] {
    --sp-default-border-size: 1px;
    --sp-default-border-color: var(--f7-button-border-color, var(--f7-theme-color));
    --sp-default-bg: var(--f7-block-strong-bg-color);
    --sp-selected-border-size: 1px;
    --sp-selected-border-color: var(--f7-button-fill-bg-color, var(--f7-theme-color));
    --sp-selected-bg: var(--f7-button-fill-bg-color, var(--f7-theme-color));
    --sp-hover-border-size: 1px;
    --sp-hover-border-color: var(--f7-button-fill-pressed-bg-color, var(--f7-theme-color-tint));
    --sp-hover-bg: var(--f7-button-fill-pressed-bg-color, var(--f7-theme-color-tint));
    --sp-default-border-radius: var(--f7-button-border-radius);
}
```