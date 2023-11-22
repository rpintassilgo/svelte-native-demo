<script lang="ts">
    import { onMount } from "svelte";
    import { Template } from 'svelte-native/components'

    const cores: Array<string> = [
        'IndianRed','LightCoral','Salmon','DarkSalmon','LightSalmon','Crimson','Red','FireBrick','DarkRed','Pink','LightPink','HotPink','DeepPink','MediumVioletRed','PaleVioletRed','Coral','Tomato','OrangeRed','DarkOrange','Orange','Gold','Yellow','LightYellow','LemonChiffon','LightGoldenrodYellow','PapayaWhip','Moccasin','PeachPuff','PaleGoldenrod','Khaki','DarkKhaki','Lavender','Thistle','Plum','Violet','Orchid','Fuchsia','Magenta','MediumOrchid','MediumPurple','BlueViolet','DarkViolet','DarkOrchid','DarkMagenta','Purple','RebeccaPurple','Indigo','MediumSlateBlue','SlateBlue','DarkSlateBlue','GreenYellow','Chartreuse','LawnGreen','Lime','LimeGreen','PaleGreen','LightGreen','MediumSpringGreen','SpringGreen','MediumSeaGreen','SeaGreen','ForestGreen','Green','DarkGreen','YellowGreen','OliveDrab','Olive','DarkOliveGreen','MediumAquamarine','DarkSeaGreen','LightSeaGreen','DarkCyan','Teal','Aqua','Cyan','LightCyan','PaleTurquoise','Aquamarine','Turquoise','MediumTurquoise','DarkTurquoise','CadetBlue','SteelBlue','LightSteelBlue','PowderBlue','LightBlue','SkyBlue','LightSkyBlue','DeepSkyBlue','DodgerBlue','CornflowerBlue','RoyalBlue','Blue','MediumBlue','DarkBlue','Navy','MidnightBlue','Cornsilk','BlanchedAlmond','Bisque','NavajoWhite','Wheat','BurlyWood','Tan','RosyBrown','SandyBrown','Goldenrod','DarkGoldenrod','Peru','Chocolate','SaddleBrown','Sienna','Brown','Maroon','White','Snow','Honeydew','MintCream','Azure','AliceBlue','GhostWhite','WhiteSmoke','Seashell','Beige','OldLace','FloralWhite','Ivory','AntiqueWhite','Linen','LavenderBlush','MistyRose','Gainsboro','LightGrey','Silver','DarkGrey','Grey','DimGrey','LightSlateGrey','SlateGrey','DarkSlateGrey','Black'
    ]

    let streak: number = 0
    let quantidadeCores: number = 2
    let coresSelecionadas: string[] = []
    let corCorreta: string = ""
    

    const gerarCores = (quantidade: number) => {
        const coresReordenadas = cores.sort(() => Math.random() - 0.5)

        coresSelecionadas = coresReordenadas.slice(0,quantidade)
        corCorreta = coresSelecionadas[Math.floor(Math.random() * quantidade)]; 
    }

    const clicarCor = (corClicada: string) => {
        if (corClicada == corCorreta){
            streak++
            alert("Acertas-te, parabéns! :)")
            if(quantidadeCores <= 6) quantidadeCores +=2
            gerarCores(quantidadeCores)
        } else {
            streak = 0
            gerarCores(quantidadeCores)
            quantidadeCores = 2
        }
    }

    onMount(() => {
        gerarCores(quantidadeCores) 
    })

    $: gerarCores(quantidadeCores)
 
    
</script>

<page>
    <actionBar title="Cores" />

    <stackLayout>
        <label textAlignment="center" class="label"> 
            <span text="Streak: {streak}" />
        </label>
        <stackLayout style="background-color: aliceblue">
            <label textAlignment="center" class="label"> 
                <span text="Número de cores: {quantidadeCores}" />
            </label>
            <dockLayout dock="left" width="50%" stretchLastChild="true">
                <button on:tap={() => quantidadeCores == 2 ? undefined : quantidadeCores-=2}>-</button>
                <button on:tap={() => quantidadeCores == 8 ? undefined : quantidadeCores+=2}>+</button>
            </dockLayout>
        </stackLayout>

        <label textAlignment="center" class="pergunta"> 
            {#await corCorreta then cor}
            <span text={"Qual é a cor " + cor + "?"} />
            {/await}
        </label>

        <wrapLayout alignSelf="center" class="retanguloCores" itemWidth="100">
            {#each coresSelecionadas as cor}
                <label on:tap={() => clicarCor(cor)} width="100" height="100" class="quadrado" backgroundColor={cor} />
            {/each}
        </wrapLayout>

        <!--
        <gridLayout columns="150,150" rows="150,150" alignSelf="center" class="retanguloCores">
            <label on:tap={() => clicarCor(coresSelecionadas[0])} textAlignment="center" row={0} col={0} class="quadrado" backgroundColor={coresSelecionadas[0]} />
            <label on:tap={() => clicarCor(coresSelecionadas[1])} textAlignment="center" row={0} col={1} class="quadrado" backgroundColor={coresSelecionadas[1]} />
            <label on:tap={() => clicarCor(coresSelecionadas[2])} textAlignment="center" row={1} col={0} class="quadrado" backgroundColor={coresSelecionadas[2]} />
            <label on:tap={() => clicarCor(coresSelecionadas[3])} textAlignment="center" row={1} col={1} class="quadrado" backgroundColor={coresSelecionadas[3]} />
        </gridLayout>
        -->

        <!--
        <listView items="{coresSelecionadas}" on:itemTap={(event) => console.log(event.index)}>
                <Template let:item>
                    <label on:tap={() => clicarCor(item)} textAlignment="center" class="quadrado" backgroundColor={item} />
                </Template>
        </listView>
        -->
    </stackLayout>

</page>

<style>
.label {
    font-size: 20;
    font-weight: 600;
    background-color: aliceblue;
}
.pergunta {
    margin-top: 20;
    font-size: 15;
    font-weight: 600;
}
.retanguloCores { 
    margin-top: 50;
    border-width: 2;
    border-color: black;
    /*width: 300; grid original sem slider */
    width: 205;
}
.quadrado {
    border-width: 1;
    border-color: black;
}
</style>