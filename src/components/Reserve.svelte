<script lang="ts">
    export let ObjectReserve;
    export let handleShowModal;

    let selectOutput: string = '';
    let selectPerson: number = 1;

    class Reserve {
        #output:       string = '';
        #numberPerson: number = 0;
        #price:        number = undefined;
        constructor( output: string, numberPerson: number, price: number ){
            this.#output = output;
            this.#numberPerson = numberPerson;
            this.#price = price;
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

        get numberPerson(){
            return this.#numberPerson;
        }
        set numberPerson(newnumberPerson: number){
            this.#numberPerson = newnumberPerson;
        }
        
        set price(newPrice: number){
            this.#price = newPrice;
        }

        priceTotal(){
            return this.#price * this.#numberPerson
        }
    }
    let dateForm: Reserve;

    $: {
        if(ObjectReserve){
            dateForm =  new Reserve("", 1, ObjectReserve.price);
            console.log(ObjectReserve.price)
        }
    }

    const handleForm = (newOutput: string, newnumberPerson: number ) => {
        dateForm.output = newOutput;
        dateForm.numberPerson = newnumberPerson;
        console.log('reserva realizada',dateForm)
    }

    
</script>

<div class="w-75 card p-4 shadow-lg position-relative">
    <button on:click={handleShowModal} type="button" class="btn-close position-absolute top-0 end-0 m-2"></button>
    <h2 class="my-3 text-center">{ObjectReserve.title}</h2>
    <form  on:change|preventDefault="{ () => handleForm(selectOutput, selectPerson)}" class="d-flex flex-column align-items-center">
        <div class="w-75 d-flex flex-column justify-content-start align-items-center gap-2">
            
            <label for="output" class="m-2">
                <img class="svg" src="/assets/svg/salida.svg" alt="svg salida">
                Salida:
            </label>
            <select bind:value={selectOutput} class="form-select" name="output" id="output">
                    <option value=""> -- </option>
                {#each ObjectReserve.output as output}
                    <option value={output}>{output}</option>
                {/each}
            </select>

        </div>
        <div class="w-75 d-flex flex-column justify-content-start align-items-center gap-2">
            
            <label for="person-number" class="m-2">
                <img class="svg" src="/assets/svg/person.svg" alt="svg personas">
                Personas:
            </label>
            <select onchange={() => dateForm.priceTotal()} bind:value={selectPerson} class="form-select" name="person" id="person-number">
                {#each Array(20) as _, i}
                     <option value={i + 1}>{i+1}</option>
                {/each}
            </select>
        </div>
        <div class="w-75 text-center my-2">
            
            <p>Precio total: {dateForm.priceTotal()} €</p>
        </div>

        <button type="submit" class="btn btn-secondary py-3 my-3 fw-bold w-75">Reservar</button>

    </form>
</div>
