<template>

	<div data-selectpostion :id="id" :data-static="static ? 'true' : 'false'" :style="'margin: auto; width: ' + size + '; height: ' + size + ';'">
		<div :class="value == 'tl' ? 'selected' : ''" @click="changeSelection" data-value="tl"></div>
		<div :class="value == 'tr' ? 'selected' : ''" @click="changeSelection" data-value="tr"></div>
		<div :class="value == 'bl' ? 'selected' : ''" @click="changeSelection" data-value="bl"></div>
		<div :class="value == 'br' ? 'selected' : ''" @click="changeSelection" data-value="br"></div>
		<div :class="value == 'cc' ? 'selected' : ''" @click="changeSelection" data-value="cc"></div>
	</div>

</template>


<script>
	export default {
	    props: {
	        static: {
	            type: Boolean,
	            default: false
	        },

	        preselected: {
	            type: String,
	            default: ''
	        },

	        size: {
	            type: String, // == Number || Percent
	            default: '100%'
	        },
	    },

		data() {
			return {
				id: 'sp' + Math.floor(Math.random() * 1000000),

				value: this.preselected,
			};
		},

		watch: {
			preselected(val) {
				this.value = val;
			},
		},

    	methods: {
    		changeSelection(ev) {
    			if (this.static) return;

    			const $$ = this.$$;
    			const $el = $$(ev.currentTarget);
    			
    			this.value = $el.attr('data-value');
    			this.$emit('changed', this.value);
    		},
    	},
	};
</script>


<style lang="less">
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
		
		position: relative;
		display: grid;
		border: 0;

		grid-template-columns: 25% 25% 25% 25%;
		grid-template-rows: 25% 25% 25% 25%;
		
		width: 100%;
		height: 100%;
		
		grid-gap: --sp-default-border-size;
		

		// radio buttons
		> input[type="radio"] {
			-webkit-appearance: none;
			-moz-appearance: none;
			-ms-appearance: none;
			-o-appearance: none;
			appearance: none;
			
			&:focus {
				outline: 0;
			}
		}
		
		> * {
			border-radius: 0;
			box-shadow: 0 0 0 var(--sp-default-border-size) var(--sp-default-border-color);
			background: var(--sp-default-bg);
			position: relative;
			
			transition: all .3s;
			
			width: 100%;
			height: 100%;
		}
		&:not([data-static="true"]) > *:hover {
			box-shadow: 0 0 0 var(--sp-hover-border-size) var(--sp-hover-border-color);
			background: var(--sp-hover-bg);
			z-index: 1;
			cursor: pointer;
		}
			
		> *.selected {
			box-shadow: 0 0 0 var(--sp-selected-border-size) var(--sp-selected-border-color);
			background: var(--sp-selected-bg);
		}
		
		> *:nth-child(1) {
			grid-column-start: 1;
			grid-column-end: 3;
			grid-row-start: 1;
			grid-row-end: 3;
			border-top-left-radius: var(--sp-default-border-radius);
		}
		> *:nth-child(2) {
			grid-column-start: 3;
			grid-column-end: 5;
			grid-row-start: 1;
			grid-row-end: 3;
			border-top-right-radius: var(--sp-default-border-radius);
		}
		> *:nth-child(3) {
			grid-column-start: 1;
			grid-column-end: 3;
			grid-row-start: 3;
			grid-row-end: 5;
			border-bottom-left-radius: var(--sp-default-border-radius);
		}
		> *:nth-child(4) {
			grid-column-start: 3;
			grid-column-end: 5;
			grid-row-start: 3;
			grid-row-end: 5;
			border-bottom-right-radius: var(--sp-default-border-radius);
		}

		> *:nth-child(5) {
			position: absolute;
			z-index: 2;
			grid-column-start: 2;
			grid-column-end: 4;
			grid-row-start: 2;
			grid-row-end: 4;
			border-radius: var(--sp-default-border-radius);
		}

	}
</style>