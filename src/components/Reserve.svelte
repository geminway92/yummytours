<script lang="ts">
import type AvailableDate from "src/interfaces/AvailableDate.interface";


    export let ObjectReserve;
    export let handleShowModal;

    
    let selectOutput: string = '';
    let selectPerson: number = 1;
    let selectDate: string = '';
    let dateForm: Reserve;
    let disabledButon: boolean = true;

    class Reserve {
        #output:       string = '';
        #numberPerson: number = 0;
        #price:        number = undefined;
        #date:         AvailableDate = null;
        constructor( output: string, numberPerson: number, price: number){
            this.#output = output;
            this.#numberPerson = numberPerson;
            this.#price = price;
            this.#date;
        }

        get output(){
            return this.#output;
        }

        set output(newOutput: string){
            this.#output = newOutput;
        }

        get price(){
            return this.#price;
        }

        get date(){
            return this.#date;
        }

        get numberPerson(){
            return this.#numberPerson;
        }
        set numberPerson(newNumberPerson: number){
            this.#numberPerson = newNumberPerson;
        }
        
        set price(newPrice: number){
            this.#price = newPrice;
        }

        set date( newDate: AvailableDate){
            this.#date = newDate;
        }

        priceTotal(){
            return (this.#price * this.#numberPerson).toFixed(2)
        }

        updateDate(){
            this.#output = selectOutput;
            this.#numberPerson = selectPerson;
            this.#date =  ObjectReserve.availableDate.find(route => route.from === selectDate);
        
        }

        validateForm(){
            this.updateDate();
            priceTotal = this.priceTotal();
        
            if(this.#date && this.#output && this.#date){
                disabledButon = false;
                console.log('Validado')
            }else {
                disabledButon = true;
                console.log('No valido')
            }
        }
    }
    

    $: {
        if(ObjectReserve){
            dateForm =  new Reserve("", 1, ObjectReserve.price);
            console.log(ObjectReserve)
        }
    }   

    $: priceTotal = dateForm.priceTotal();

   const register = () => {
    console.log('se ha registrado', dateForm)
   }

    
</script>

<div class="w-75 card p-4 shadow-lg position-relative">
    <button on:click={handleShowModal} type="button" class="btn-close position-absolute top-0 end-0 m-2"></button>
    <h2 class="my-3 text-center">{ObjectReserve.title}</h2>
    <form on:change={() => dateForm.validateForm()}  on:submit|preventDefault="{ () => register()}" class="d-flex flex-column align-items-center">
        <div class="w-75 d-flex flex-column justify-content-start align-items-center gap-2">
            
            <label for="output" class="m-2">
                <img class="svg" src="/assets/svg/salida.svg" alt="svg salida">
                Salida:
            </label>
            <select  bind:value={selectOutput} class="form-select" name="output" id="output">
                    <option value=""> -- </option>
                {#each ObjectReserve.output as output}
                    <option value={output}>{output}</option>
                {/each}
            </select>

        </div>
        <div class="w-75 d-flex flex-column justify-content-start align-items-center gap-2">
            <label for="person-number" class="m-2">
                <img class="svg" src="/assets/svg/calendar-date.svg" alt="svg fecha">
                Fecha:
            </label>
            <select bind:value={selectDate} class="form-select" name="person" id="person-number">
                <option value=""> -- </option>
                {#each ObjectReserve.availableDate as date }
                     <option value={date.from}>{date.from} - {date.to}</option>
                {/each}
            </select>
        </div>
        <div class="w-75 d-flex flex-column justify-content-start align-items-center gap-2">
            
            <label for="person-number" class="m-2">
                <img class="svg" src="/assets/svg/person.svg" alt="svg personas">
                Personas:
            </label>
            <select bind:value={selectPerson} class="form-select" name="person" id="person-number">
                {#each Array(20) as _, i}
                     <option value={i + 1}>{i+1}</option>
                {/each}
            </select>
        </div>
        <div class="w-75 text-center my-2">
            
            <p>Precio total: {priceTotal} €</p>
        </div>

        <button disabled={disabledButon} type="submit" class="btn btn-secondary py-3 my-3 fw-bold w-75">Reservar</button>

    </form>
</div>
