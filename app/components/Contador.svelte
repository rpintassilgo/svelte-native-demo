<page>
    <actionBar title="Contador" />
    <stackLayout>
        <label class="info">
            <formattedString>
                <span text="Número: " />
                <span text=" {numero}" />
            </formattedString>
        </label>

        <label class="info">
            <formattedString>
                <span text="Número * 2: " />
                <span text=" {resultado}" />
            </formattedString>
        </label>

        <label class="info">
            <formattedString>
                <span text="Número * 4: " />
                <span text=" {resultado2}" />
            </formattedString>
        </label>

        <button on:tap={handleTap}>Somar 1</button>
    </stackLayout>
</page>

<script lang="ts">
    let numero: number = 1
    $: resultado = numero * 2
    $: resultado2 = resultado * 2

    $: resultado2 == 100 ? alert("teste") : undefined

    const handleTap = () => numero++
</script>

<style>
    .info {
        padding-top: 10;
        font-size: 20;
        horizontal-align: center;
        vertical-align: center;
    }
</style>
