<script lang="ts">
import type AvailableDate from "src/interfaces/AvailableDate.interface";
import { toast } from '@zerodevx/svelte-toast'

    export let ObjectReserve;
    export let handleShowModal;

    let selectOutput: string = '';
    let selectPerson: number = 1;
    let selectDate: string = '';

 
    let dateForm: Reserve;
    let disabledBtnReserve: boolean = true;
    let disabledBtnCompletedReserve: boolean = true;
    let showDateContact: boolean = false;

    let form = {
        name: '',
        surname: '',
        phone: ''
    }

    class Reserve {
        #output:       string = '';
        #numberPerson: number = 0;
        #price:        number = undefined;
        #date:         AvailableDate = null;
        constructor( output: string, numberPerson: number, price: number, date?: AvailableDate){
            this.#output = output;
            this.#numberPerson = numberPerson;
            this.#price = price;
            this.#date = date;
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
                disabledBtnReserve = false;
                return
                
            }

            disabledBtnReserve = true;
        }
    }

    class Client extends Reserve {
        #name: string;
        #surname: string;
        #phone: string;
        
        constructor(output: string, numberPerson: number, price: number, date?: AvailableDate){
            super(output, numberPerson, price, date)
            this.#name;
            this.#surname;
            this.#phone;
        }

        get name(){
            return this.#name;
        }

        get surname(){
            return this.#surname;
        }

        get phone(){
            return this.#phone;
        }

        set name(newName){
            this.#name = newName;
        }
        
        set surname(newSurname){
            this.#surname = newSurname;
        }
        set phone(newPhone){
            this.#phone = newPhone;
        }

        updateDate(){
            this.#name = form.name;
            this.#surname = form.surname;
            this.#phone = form.phone;
        
        }

        validateForm(){
            this.updateDate();
            priceTotal = this.priceTotal();
        
            if(this.#name && this.#surname && this.#phone){
                disabledBtnCompletedReserve = false;
                return
            }

            disabledBtnCompletedReserve = true;
        }
        
    }
    
    let newClient;
    $: {
        if(ObjectReserve){
            dateForm =  new Reserve("", 1, ObjectReserve.price);
            newClient = new Client("", 1, ObjectReserve.price)
        }
    }   

    $: priceTotal = dateForm.priceTotal();

   const register = () => {
        toast.push('Registrado correctamente',{theme: {
            '--toastBackground': '#48BB78',
            '--toastBarBackground': '#2F855A'
        }})

        handleShowModal()

        showDateContact = !showDateContact;
    
    }
    
    
   

    
</script>

{#if !showDateContact}
<div class="w-75 card p-4 shadow-lg position-relative">
    <button on:click={handleShowModal} type="button" class="btn-close position-absolute top-0 end-0 m-2"></button>
    <h2 class="my-3 text-center">{ObjectReserve.title}</h2>
    <form on:change={() => dateForm.validateForm()}  on:submit|preventDefault="{() => showDateContact = true}" class="d-flex flex-column align-items-center">
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

        <button disabled={disabledBtnReserve} type="submit" class="btn btn-secondary py-3 my-3 fw-bold w-75">Reservar</button>

    </form>
</div>
{:else}
    <div class="w-75 card p-4 shadow-lg d-flex justify-content-center align-items-center">
        <h1>Un paso más</h1>
        <p class="text-center">
            Añade tus datos de contactos y le reservaremos la ruta <span class="text-primary fw-bold">{ObjectReserve.title}</span>
        </p>

        <form on:change={() => newClient.validateForm()}  on:submit|preventDefault={() => register()} class=" w-75 d-flex flex-column align-items-center gap-3">
            <label for="name">Nombre</label>
            <input bind:value={form.name} class="form-control" id="name" type="text">

            <label for="surname">Apellidos</label>
            <input bind:value={form.surname} class="form-control" id="surname" type="text">

            <label for="phone">Teléfono</label>
            <input bind:value={form.phone} class="form-control" id="phone" type="text">
            <button disabled={disabledBtnCompletedReserve} type="submit" class="btn btn-secondary py-3 my-3 fw-bold w-50">Completar Reserva</button>
            <button on:click={handleShowModal()} type="button" class="btn btn-danger py-3 fw-bold w-50">Cancelar</button>
        </form>
    </div>
{/if}


<style>
button{
    width: 200px;
}
</style>