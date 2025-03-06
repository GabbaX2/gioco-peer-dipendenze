<script lang="ts">
  import { writable } from "svelte/store";

  const miti = [
    "Chi ha una dipendenza è solo una persona debole.",
    "Basta forza di volontà per smettere.",
    "Le droghe leggere non creano dipendenza.",
    "Solo le droghe pesanti sono pericolose.",
    "Se una sostanza è legale, allora non fa male.",
    "Chi ha una vita stabile non può diventare dipendente.",
    "Si diventa dipendenti solo se si fa uso quotidiano.",
    "La dipendenza è solo fisica, basta disintossicarsi.",
    "Una volta disintossicato, il problema è risolto.",
    "Se una persona ha una dipendenza, è colpa sua.",
    "Solo le persone con problemi psicologici diventano dipendenti.",
    "Le terapie non servono, chi vuole smettere lo fa da solo.",
    "Se qualcuno riesce a controllare il consumo, allora non è dipendente.",
    "Smetto quando voglio.",
    "Posso consumare solo nei weekend senza problemi.",
    "Se non mi buco, non sono un vero tossicodipendente.",
    "Bere alcol tutti i giorni è normale, non è dipendenza.",
    "Posso smettere da solo senza aiuto.",
    "Tutti lo fanno, quindi non è pericoloso.",
    "Solo i senzatetto o i criminali hanno problemi di dipendenza.",
    "Le droghe migliorano la creatività e non hanno conseguenze serie.",
    "Le droghe leggere, come la marijuana, non sono dannose.",
    "La cocaina ti rende più energico e produttivo.",
    "Le droghe non creano dipendenza se le usi solo di tanto in tanto.",
    "Le persone che usano eroina sono sempre senza speranza e non possono migliorare.",
    "Fumare hashish non è pericoloso come fumare tabacco.",
    "Le droghe psichedeliche sono sicure e non hanno effetti collaterali gravi.",
    "Se una persona usa droghe una sola volta, non correrà alcun rischio.",
    "L'uso di droghe non influisce sul tuo aspetto fisico.",
    "Se una persona smette di usare droghe, può riprendersi completamente senza conseguenze.",
    "Solo i poveri o chi vive in situazioni difficili usa droghe.",
    "Bere un bicchiere di vino ogni giorno fa bene alla salute.",
    "L'alcol non è una droga, perché è legale.",
    "L'alcol non causa dipendenza se lo bevi solo nei weekend.",
    "Se una persona può dosare la quantità di alcol, non è dipendente.",
    "Bere solo durante le feste non è un problema.",
    "Il corpo di una persona tollera meglio l'alcol con l'età.",
    "Bevendo alcol in modo responsabile non corri rischi.",
    "Gli alcolisti sono sempre visibili e hanno problemi evidenti.",
    "Solo le persone che bevono troppo in una volta diventano alcolisti.",
    "Se non vomiti dopo aver bevuto, non hai bevuto troppo.",
    "Fumare solo qualche sigaretta ogni tanto non fa male.",
    "Le sigarette elettroniche come iqos, glo, ploom sono meno dannose delle normali.",
    "Fumare solo all'aperto non influisce sulla salute.",
    "Se fumi solo in gioventù, il danno non è permanente.",
    "Chi fuma può smettere facilmente quando vuole.",
    "Se fumi solo in compagnia, non sei un vero fumatore.",
    "Il fumo passivo non è pericoloso per gli altri.",
    "Le sigarette elettroniche sono completamente sicure e non causano danni.",
    "Il fumo non influisce sulla pelle o sull'aspetto esteriore.",
    "Fumare qualche sigaretta al giorno non ti farà ammalare.",
  ];

  let mito_random = writable("");
  let mito_sfatato = writable("");
  let modalOpen = writable(false);

  // Funzione per scegliere un mito casuale
  const scegliMito = () => {
    const selectedMito = miti[Math.floor(Math.random() * miti.length)];
    mito_random.set(selectedMito);
  };

  const sfataMito = () => {
    const currentMito = $mito_random;
    const frasiSfatate = {
      "Chi ha una dipendenza è solo una persona debole.":
        "La dipendenza è una malattia complessa che non dipende solo dalla volontà della persona. È legata a fattori genetici, ambientali e psicologici.",
      "Basta forza di volontà per smettere.":
        "La dipendenza richiede trattamenti specifici e supporto. Non si tratta solo di forza di volontà, ma anche di un processo che coinvolge il corpo e la mente.",
      "Le droghe leggere non creano dipendenza.":
        "Anche le droghe 'leggere' come la marijuana possono creare dipendenza, specialmente se usate regolarmente o in età giovane.",
      "Solo le droghe pesanti sono pericolose.":
        "Le droghe leggere e l'alcol possono essere altrettanto dannosi, soprattutto quando si sviluppa una dipendenza.",
      "Se una sostanza è legale, allora non fa male.":
        "La legalità di una sostanza non è sinonimo di sicurezza. L'alcol e il tabacco, pur essendo legali, causano danni alla salute.",
      "Chi ha una vita stabile non può diventare dipendente.":
        "Chiunque può sviluppare una dipendenza, indipendentemente dal proprio stato sociale o dalla stabilità della sua vita.",
      "Si diventa dipendenti solo se si fa uso quotidiano.":
        "Anche l'uso occasionale di sostanze può portare a dipendenza, a seconda della persona e del tipo di sostanza.",
      "La dipendenza è solo fisica, basta disintossicarsi.":
        "La dipendenza è anche psicologica e comportamentale. Disintossicarsi non è sufficiente senza un trattamento completo.",
      "Una volta disintossicato, il problema è risolto.":
        "La disintossicazione è solo il primo passo. La vera sfida è mantenere la sobrietà e affrontare le cause psicologiche della dipendenza.",
      "Se una persona ha una dipendenza, è colpa sua.":
        "La dipendenza è una malattia che può colpire chiunque, e non è colpa della persona che ne è affetta.",
      "Solo le persone con problemi psicologici diventano dipendenti.":
        "Chiunque può sviluppare una dipendenza, indipendentemente dalla propria salute mentale o dalle esperienze passate.",
      "Le terapie non servono, chi vuole smettere lo fa da solo.":
        "Le terapie sono essenziali per trattare la dipendenza. Il supporto psicologico e medico è fondamentale.",
      "Se qualcuno riesce a controllare il consumo, allora non è dipendente.":
        "Il controllo del consumo non è sempre segno di non dipendenza. Molti dipendenti riescono a nascondere la loro dipendenza e a mantenere il controllo in pubblico.",
      "Smetto quando voglio.":
        "La dipendenza non è una questione di volere o non volere. La dipendenza è una malattia che necessita di un trattamento professionale.",
      "Posso usare solo nei weekend senza problemi.":
        "L'uso occasionale può sembrare innocuo, ma può comunque sviluppare una dipendenza o portare a danni fisici e psicologici.",
      "Se non mi buco, non sono un vero tossicodipendente.":
        "La dipendenza non dipende dal tipo di sostanza usata. Anche l'alcol, il fumo o le droghe leggere possono causare dipendenza.",
      "Bere alcol tutti i giorni è normale, non è dipendenza.":
        "Bere alcol tutti i giorni può essere un segno di dipendenza. Anche l'alcol può causare gravi danni alla salute, sia fisica che mentale.",
      "Posso smettere da solo senza aiuto.":
        "Molte persone hanno bisogno di un trattamento professionale per affrontare la dipendenza in modo sicuro ed efficace.",
      "Tutti lo fanno, quindi non è pericoloso.":
        "Anche se altre persone usano una sostanza, non significa che sia sicura. Ogni persona reagisce diversamente alle sostanze.",
      "Solo i senzatetto o i criminali hanno problemi di dipendenza.":
        "La dipendenza può colpire chiunque, indipendentemente dalla propria posizione sociale o dalle circostanze della vita.",
      "Le droghe migliorano la creatività e non hanno conseguenze serie.":
        "Molti studi hanno dimostrato che le droghe danneggiano il cervello, riducono la capacità cognitiva e causano danni fisici.",
      "Le droghe leggere, come la marijuana, non sono dannose.":
        "Anche la marijuana può danneggiare la salute, soprattutto se usata in modo regolare e a lungo termine. Può causare dipendenza e influire negativamente sulla memoria e sull'apprendimento.",
      "La cocaina ti rende più energico e produttivo.":
        "La cocaina è una droga altamente pericolosa che può causare danni permanenti al cuore, al cervello e ad altri organi. La sensazione di energia è temporanea e viene seguita da un forte crollo.",
      "Le droghe non creano dipendenza se le usi solo di tanto in tanto.":
        "Anche l'uso di una sola volta può avere gravi conseguenze, inclusi danni alla salute mentale e fisica, e può portare a una dipendenza.",
      "Le persone che usano eroina sono sempre senza speranza e non possono migliorare.":
        "Chi usa eroina può recuperare e migliorare con il giusto trattamento. La riabilitazione è possibile.",
      "Fumare hashish non è pericoloso come fumare tabacco.":
        "Il fumo di hashish contiene molte delle stesse sostanze tossiche e cancerogene del tabacco. È dannoso per i polmoni e la salute in generale.",
      "Le droghe psichedeliche sono sicure e non hanno effetti collaterali gravi.":
        "Le droghe psichedeliche possono avere effetti collaterali gravi, inclusi danni psicologici e comportamentali, e non sono prive di rischi.",
      "Se una persona usa droghe una sola volta, non correrà alcun rischio.":
        "Anche un singolo uso di droghe può avere conseguenze gravi, tra cui overdose e danni fisici e psicologici.",
      "L'uso di droghe non influisce sul tuo aspetto fisico.":
        "L'uso di droghe può danneggiare la pelle, i capelli e provocare invecchiamento precoce.",
      "Se una persona smette di usare droghe, può riprendersi completamente senza conseguenze.":
        "La riabilitazione è un processo lungo e impegnativo. Anche dopo aver smesso, molte persone affrontano difficoltà fisiche e psicologiche.",
      "Solo i poveri o chi vive in situazioni difficili usa droghe.":
        "La dipendenza non ha confini di classe sociale. Può colpire chiunque, indipendentemente dalle risorse economiche.",
      "Bere un bicchiere di vino ogni giorno fa bene alla salute.":
        "Anche l'assunzione regolare di alcol può avere effetti dannosi sulla salute, come danni al fegato, al cuore e al cervello.",
      "L'alcol non è una droga, perché è legale.":
        "L'alcol è una droga che può causare dipendenza, danni al fegato, al cuore e a molti altri organi.",
      "L'alcol non causa dipendenza se lo bevi solo nei weekend.":
        "L'alcol può causare dipendenza anche con un consumo non quotidiano, a seconda della persona e delle circostanze.",
      "Se una persona può tenere l'alcol, non è dipendente.":
        "Il fatto che una persona riesca a mantenere un consumo moderato non significa che non sia dipendente.",
      "Bere solo durante le feste non è un problema.":
        "Bere regolarmente, anche solo durante le feste, può portare a una dipendenza graduale e danni alla salute.",
      "Il corpo di una persona tollera meglio l'alcol con l'età.":
        "Con l'età, il corpo diventa più vulnerabile agli effetti dannosi dell'alcol, e non lo tollera meglio.",
      "Bevendo alcol in modo responsabile non corri rischi.":
        "Anche un consumo responsabile di alcol può portare a dipendenza e danni alla salute a lungo termine.",
      "Gli alcolisti sono sempre visibili e hanno problemi evidenti.":
        "Gli alcolisti possono sembrare perfettamente normali all'esterno, anche se stanno affrontando una dipendenza grave.",
      "Solo le persone che bevono troppo in una volta diventano alcolisti.":
        "L'alcolismo non dipende solo dalla quantità bevuta in una sola volta, ma anche dalla frequenza e dal comportamento complessivo.",
      "Se non vomiti dopo aver bevuto, non hai bevuto troppo.":
        "Il fatto di non vomitare non significa che l'alcol non stia danneggiando il corpo. Gli effetti possono essere interni e subdoli.",
      "Fumare solo qualche sigaretta ogni tanto non fa male.":
        "Anche fumare occasionalmente può danneggiare la salute e aumentare il rischio di malattie gravi come il cancro.",
      "Le sigarette leggere sono meno dannose delle normali.":
        "Le sigarette leggere contengono le stesse sostanze dannose delle sigarette normali e sono ugualmente pericolose.",
      "Fumare solo all'aperto non influisce sulla salute.":
        "Il fumo passivo è pericoloso anche all'aperto, e può danneggiare la salute delle persone intorno a te.",
      "Se fumi solo in gioventù, il danno non è permanente.":
        "I danni del fumo possono essere permanenti, anche se si inizia a fumare da giovani.",
      "Chi fuma può smettere facilmente quando vuole.":
        "La dipendenza dal fumo è difficile da superare senza supporto, e non è facile smettere da soli.",
      "Se fumi solo in compagnia, non sei un vero fumatore.":
        "Anche fumare occasionalmente può portare alla dipendenza e aumentare il rischio di malattie gravi.",
      "Il fumo passivo non è pericoloso per gli altri.":
        "Il fumo passivo è estremamente pericoloso per gli altri, e può causare malattie respiratorie e cardiovascolari.",
      "Le sigarette elettroniche sono completamente sicure e non causano danni.":
        "Le sigarette elettroniche possono ancora causare danni alla salute e non sono prive di rischi.",
      "Il fumo non influisce sulla pelle o sull'aspetto esteriore.":
        "Il fumo danneggia la pelle, accelera l'invecchiamento e aumenta il rischio di rughe e altre condizioni.",
      "Fumare qualche sigaretta al giorno non ti farà ammalare.":
        "Anche fumare solo poche sigarette al giorno può causare danni alla salute e aumentare il rischio di malattie gravi.",
    };

    mito_sfatato.set(frasiSfatate[currentMito] || "Mito non trovato");
    modalOpen.set(true);
  };
</script>

<main
  class="container mx-auto p-6 min-h-screen bg-gradient-to-b from-blue-100 to-purple-100"
>
  <h1
    class="text-5xl font-bold text-center mb-8 text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600"
  >
    🧨 SFATA IL MITO! 🧨
  </h1>

  <div
    class="bg-white p-8 rounded-3xl shadow-2xl mb-8 border-4 border-yellow-400"
  >
    <div class="text-center mb-10">
      <div class="inline-block bg-red-500 p-4 rounded-full animate-bounce">
        <span class="text-4xl">🎯</span>
      </div>
      <h2 class="text-4xl font-black mb-6 mt-4 text-gray-800">COME SI GIOCA</h2>
      <div class="space-y-6 text-left text-2xl">
        <div class="flex items-center bg-blue-50 p-4 rounded-xl">
          <span class="text-3xl mr-4">1️⃣</span>
          <p>
            Clicca <span class="font-bold text-blue-600">"Genera Mito"</span> per
            iniziare
          </p>
        </div>
        <div class="flex items-center bg-green-50 p-4 rounded-xl">
          <span class="text-3xl mr-4">2️⃣</span>
          <p>
            Scegli <span class="font-bold text-green-600"
              >"Scopri la verità"</span
            > per sfatarlo
          </p>
        </div>
        <div class="flex items-center bg-purple-50 p-4 rounded-xl">
          <span class="text-3xl mr-4">3️⃣</span>
          <p>
            Diventa un <span class="font-bold text-purple-600"
              >esperto anti-bufale</span
            >! 🏆
          </p>
        </div>
      </div>
    </div>

    <div
      class="bg-white p-8 rounded-3xl shadow-2xl mb-8 border-4 border-blue-400"
    >
      <h2 class="text-4xl font-black text-center mb-6 text-gray-800">
        🔥 MITO DEL GIORNO 🔥
      </h2>
      <div
        class="bg-yellow-100 p-6 rounded-xl mb-8 border-2 border-dashed border-yellow-500"
      >
        <p
          class="text-3xl text-center font-semibold text-red-600 animate-pulse"
        >
          {$mito_random || "Clicca il pulsante per iniziare!"}
        </p>
      </div>

      <div class="flex flex-col sm:flex-row justify-center gap-6">
        <button
          onclick={scegliMito}
          class="btn transform transition-all duration-200 hover:scale-105 active:scale-95
                 text-3xl font-black py-6 px-12 rounded-2xl
                 bg-gradient-to-r from-yellow-400 to-orange-500
                 shadow-lg hover:shadow-xl"
        >
          🎰 GENERA MITO
        </button>

        <button
          onclick={sfataMito}
          class="btn transform transition-all duration-200 hover:scale-105 active:scale-95
                 text-3xl font-black py-6 px-12 rounded-2xl
                 bg-gradient-to-r from-green-400 to-blue-500
                 shadow-lg hover:shadow-xl"
        >
          💥 SCOPRI LA VERITÀ
        </button>
      </div>
    </div>

    {#if $modalOpen}
      <div
        class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4"
      >
        <div
          class="bg-white rounded-3xl p-8 max-w-2xl border-4 border-green-400
                    animate__animated animate__bounceIn"
        >
          <h3 class="text-4xl font-black mb-6 text-center text-green-600">
            ✅ VERITÀ SVELATA!
          </h3>
          <div class="bg-green-50 p-6 rounded-xl mb-6">
            <p class="text-2xl leading-relaxed text-gray-800">
              {$mito_sfatato}
            </p>
          </div>
          <button
            onclick={() => modalOpen.set(false)}
            class="w-full btn transform transition-all duration-200 hover:scale-105
                   text-2xl font-bold py-4 px-8 rounded-xl
                   bg-gradient-to-r from-red-400 to-pink-500
                   shadow-lg hover:shadow-xl"
          >
            🚪 CHIUDI E CONTINUA A GIOCARE!
          </button>
        </div>
      </div>
    {/if}
  </div>
</main>

<style>
  .animate-bounce {
    animation: bounce 2s infinite;
  }
  @keyframes bounce {
    0%,
    100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-20px);
    }
  }
</style>
