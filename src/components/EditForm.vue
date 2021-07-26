<template>
    <div>
        <b-form @submit="onSubmit" >
            <b-form-group
                id="input-group-1"
                label="SKU:"
                label-for="input-1"              
            >
                <b-form-input
                    id="input-1"
                    v-model="stockData[0].sku"    
                    required>
                </b-form-input>
            </b-form-group>
            <b-form-group
                id="input-group-2"
                label="Store:"
                label-for="input-2"              
            >
                <b-form-input
                    id="input-2"
                    v-model="stockData[0].store"    
                    required>
                </b-form-input>
            </b-form-group>
             <b-form-group
                id="input-group-3"
                label="Style Option:"
                label-for="input-3"              
            >
                <b-form-input
                    id="input-3"
                    v-model="stockData[0].style"    
                    required>
                </b-form-input>
            </b-form-group>
            <b-button id="btnSubmit" type="submit" variant="primary">Submit</b-button>
        </b-form>      
    </div>
</template>

<script>
export default {
    name: 'EditForm',
    data () {
        return {
        }
    },
    props: {
        stockData: {
            type: Array,
            default: () => { return []; }
        }
    },
    methods: {
      onSubmit(event) {
        event.preventDefault()
        alert(JSON.stringify(this.stockData))
      }
    }
}
</script>
<style>
  #btnSubmit {
    position: relative;
    top: 70px;
  }
</style>