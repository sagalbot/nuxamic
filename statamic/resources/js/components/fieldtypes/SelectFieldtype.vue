<template>
    <div class="select select-full" :class="{ 'select--active': isActive }" :data-content="label">
    	<select v-el:select :name="name" v-model="data" tabindex="0" @focus="isActive = true" @blur="isActive = false">
    		<option v-for="option in selectOptions" :value="option.value">{{ option.text }}</option>
    	</select>
    </div>
</template>

<script>

export default {

    mixins: [Fieldtype],

    props: ['options'],

    data: function() {
        return {
            keyed: false,
            selectOptions: [],
            isActive: false,
        }
    },

    ready: function() {
        if (this.options) {
            this.selectOptions = this.options;
        } else {
            this.selectOptions = this.config.options;
        }
    },

    computed: {
        label: function() {
            // type juggle to make sure integers are treated as thus.
            const parsed = parseInt(this.data);
            const val = isNaN(parsed) ? this.data : parsed;

            var option = _.findWhere(this.selectOptions, {value: val});

            return (option) ? option.text : this.data;
        }
    },

    methods: {
        focus() {
            this.$els.select.focus();
        },

        getReplicatorPreviewText() {
            return this.label;
        },
    }
};
</script>
