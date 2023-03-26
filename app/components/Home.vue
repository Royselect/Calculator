<template>
    <Page>
        <ActionBar class="navbar">
            <Label class="nav-name" text="CALCULATOR"/>
        </ActionBar>
        <DockLayout id="calc">
            <StackLayout class='input-label' dock="top">
                <GridLayout columns="*" rows="*, *">
                    <!-- <Label row="0" col="0" class="value" v-model="value"/> -->
                    <Label row="1" col="0" class="input" v-model="result"/>
                </GridLayout>
                
            </StackLayout>
            <GridLayout columns="*, *, *, *" rows="*, *, *, *, *" backgroundColor="#d8d8d8" dock="bottom">
                <Button @tap="calculation('C')" class="button" text="C" row="0" col="0" colSpan="2"></Button>
                <Button @tap="calculation('^')" class='button' text="^" row="0" col="2"></Button>
                <Button @tap="calculation('7')" class='button' text="7" row="1" col="0"></Button>
                <Button @tap="calculation('8')" class='button' text="8" row="1" col="1"></Button>
                <Button @tap="calculation('9')" class='button' text="9" row="1" col="2"></Button>
                <Button @tap="calculation('4')" class='button' text="4" row="2" col="0"></Button>
                <Button @tap="calculation('5')" class='button' text="5" row="2" col="1"></Button>
                <Button @tap="calculation('6')" class='button' text="6" row="2" col="2"></Button>
                <Button @tap="calculation('1')" class='button' text="1" row="3" col="0"></Button>
                <Button @tap="calculation('2')" class='button' text="2" row="3" col="1"></Button>
                <Button @tap="calculation('3')" class='button' text="3" row="3" col="2"></Button>
                <Button @tap="calculation('0')" class='button' text="0" row="4" col="0" colSpan="2"></Button>
                <Button @tap="calculation('.')" class='button' text="." row="4" col="2"></Button>
                <GridLayout col='3' rowSpan="5" columns="*" rows="*,*,*,*,*">
                    <Button @tap="calculation('+')" class='button' text='+' row="0" backgroundColor="#25c5dd"></Button>
                    <Button @tap="calculation('-')" class='button' text='-' row="1" backgroundColor="#25c5dd"></Button>
                    <Button @tap="calculation('/')" class='button' text="/" row="2" backgroundColor="#25c5dd"></Button>
                    <Button @tap="calculation('*')" class='button' text="*" row="3" backgroundColor="#25c5dd"></Button>
                    <Button @tap="calculation('=')" class='button' text="=" row='4' backgroundColor="#25c5dd"></Button>
                </GridLayout>
            </GridLayout>
        </DockLayout>
    </Page>
</template>

<script>

export default {
    data(){
        return{
            value: '0', // строковая переменная для записи примера
            result: '0', // переменная для вывода и подсчета ответа
            // operator: null,
            // equation: '',
            alertOptions : {
                title: "Предупреждение",
                message: "Делить на ноль нельзя!",
                okButtonText: "OK",
            },
        }
    },

    methods:{

        calculation(n){

            if(n === 'C'){ //очистка значений
                this.value = '';
                this.result = '0';
            }

            if(n === '='){
                this.result = eval(this.value)
                if(!isFinite(eval(this.value))){
                    alert(this.alertOptions)
                    this.result = '0'
                    this.value = '0'
                }
            }

            if(['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '.'].includes(n)){

                if(n === '.'){
                    if(this.result[0] === '0'){
                        if(this.result.length === 1){
                            this.result = this.result.toString()
                            this.result = this.result.concat(n)
                            this.value = this.value.concat(n)
                        }                        
                    }

                    if(this.result[this.result.length - 1] != '.'){
                        if(!this.result.includes(n)){
                            this.result = this.result.toString()
                            this.result = this.result.concat(n)
                            this.value = this.value.concat(n)
                        }
                        
                    }
                }else{ // знаки кроме точки

                    if(this.result.length === 1){
                        if(this.result[0] === '0' || this.result[0] === ''){
                            this.result = n
                            this.value = n
                        }else{
                            this.result = this.result.toString()
                            this.result = this.result.concat(n)
                            this.value = this.value.concat(n)
                        }
                    }else{
                        this.result = this.result.toString()
                        this.result = this.result.concat(n)
                        this.value = this.value.concat(n)
                    }



                }
                
            }

            if(['/','*','-','+', '^'].includes(n)){

                if(n === '^'){
                    this.result = this.result.toString()
                    this.result = this.result.concat(n)
                    this.value = this.value.concat('**')
                }else{  
                    this.result = this.result.toString()
                    this.result = this.result.concat(n)
                    this.value = this.value.concat(n)
                }


            }         

        },
    }
}



// import { DockLayout, StackLayout } from '@nativescript/core';

const { GridLayout, Button } = require('@nativescript/core');

</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';

    // Custom styles
    .fas {
        @include colorize($color: accent);
        width: 50%;
    }

    .info {
        font-size: 20;
        horizontal-align: center;
        vertical-align: center;
    }
</style>
