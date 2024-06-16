<template>
  <div>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mt-8">
      <text-input label="Passaporte do preso" v-model="form.passaportePreso" />
      <text-input label="Nome do preso" v-model="form.nomePreso" />
      <text-input
        label="Passaporte do advogado"
        v-model="form.passaporteAdvogado"
      />
    </div>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <div>
        <!-- CRIMES CONTRA A VIDA -->
        <div class="border-b py-4">
          <p class="mb-2 font-bold text-xl">CRIMES CONTRA A VIDA:</p>
          <div
            v-for="(crime, index) in crimesContraVida"
            :key="index"
            @click="toggleSelectedCrime(crime)"
            class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
            :class="{ 'text-green-600': crime.selected }"
          >
            {{ crime.label }}
          </div>
        </div>
        <!-- CRIMES CONTRA DIREITOS FUNDAMENTAIS -->
        <div class="border-b py-4">
          <p class="mb-2 font-bold text-xl">
            CRIMES CONTRA DIREITOS FUNDAMENTAIS:
          </p>
          <div
            v-for="(crime, index) in crimesContraDireitosFundamentais"
            :key="index"
            @click="toggleSelectedCrime(crime)"
            class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
            :class="{
              'text-green-600': crime.selected,
            }"
          >
            {{ crime.label }}
          </div>
        </div>
        <!-- CRIMES CONTRA A LIBERDADE PESSOAL -->
        <div class="border-b py-4">
          <p class="mb-2 font-bold text-xl">
            CRIMES CONTRA A LIBERDADE PESSOAL:
          </p>
          <div
            v-for="(crime, index) in crimesContraLiberdadePessoal"
            :key="index"
            @click="toggleSelectedCrime(crime)"
            class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
            :class="{
              'text-green-600': crime.selected,
            }"
          >
            {{ crime.label }}
          </div>
        </div>
        <!-- CRIMES CONTRA A ADMINISTRAÇÃO PÚBLICA -->
        <div class="border-b py-4">
          <p class="mb-2 font-bold text-xl">
            CRIMES CONTRA A ADMINISTRAÇÃO PÚBLICA:
          </p>
          <div
            v-for="(crime, index) in crimesContraAdministracaoPublica"
            :key="index"
            @click="toggleSelectedCrime(crime)"
            class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
            :class="{
              'text-green-600': crime.selected,
            }"
          >
            {{ crime.label }}
          </div>
        </div>
        <!-- CRIMES CONTRA O PATRIMÔNIO -->
        <div class="border-b md:border-b-0 py-4">
          <p class="mb-2 font-bold text-xl">CRIMES CONTRA O PATRIMÔNIO:</p>
          <div
            v-for="(crime, index) in crimesContraPatrimonio"
            :key="index"
            @click="toggleSelectedCrime(crime)"
            class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
            :class="{
              'text-green-600': crime.selected,
            }"
          >
            {{ crime.label }}
          </div>
        </div>
      </div>
      <div>
        <!-- CRIMES CONTRA A ORDEM PÚBLICA -->
        <div class="border-b py-4">
          <p class="mb-2 font-bold text-xl">CRIMES CONTRA A ORDEM PÚBLICA:</p>
          <div
            v-for="(crime, index) in crimesContraOrdemPublica"
            :key="index"
            @click="toggleSelectedCrime(crime)"
            class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
            :class="{
              'text-green-600': crime.selected,
            }"
          >
            {{ crime.label }}
          </div>
        </div>
        <!-- CRIMES DE TRÂNSITO -->
        <div class="border-b py-4">
          <p class="mb-2 font-bold text-xl">CRIMES DE TRÂNSITO:</p>
          <div
            v-for="(crime, index) in crimesDeTransito"
            :key="index"
            @click="toggleSelectedCrime(crime)"
            class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
            :class="{
              'text-green-600': crime.selected,
            }"
          >
            {{ crime.label }}
          </div>
        </div>

        <!-- ITENS APREENDIDOS -->
        <div class="border-b py-4 md:border-b-0 py-4">
          <p class="mb-2 font-bold text-xl">ITENS APREENDIDOS:</p>
          <textarea
            v-model="form.itensApreendidos"
            class="shadow appearance-none border rounded w-full h-[150px] py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          ></textarea>
        </div>
      </div>
      <div>
        <!-- ATENUANTES -->
        <div class="border-b py-4">
          <p class="mb-2 font-bold text-xl">ATENUANTES:</p>
          <div
            v-for="(atenuante, index) in atenuantes"
            :key="index"
            @click="toggleSelectedCrime(atenuante)"
            class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
            :class="{
              'text-green-600': atenuante.selected,
            }"
          >
            {{ atenuante.label }}
          </div>
        </div>
        <!-- AGRAVANTES -->
        <div class="border-b py-4">
          <p class="mb-2 font-bold text-xl">AGRAVANTES:</p>
          <div
            class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
            :class="{
              'text-green-600': form.mandato,
            }"
            @click="toggleMandato"
          >
            🔹 Mandado de busca e apreensão
          </div>
          <div
            class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
            :class="{
              'text-green-600': crimesContraOrdemPublica[10].selected,
            }"
            @click="toggleReincidente"
          >
            🔹 Réu reincidente
          </div>
        </div>
        <!-- FIANÇA -->
        <div class="border-b py-4">
          <p class="mb-2 font-bold text-xl">FIANÇA:</p>
          <text-input
            label="Dinheiro sujo"
            @keyup="moeda"
            v-model="form.dinheiroSujo"
          />
          <div class="flex flex-col">
            <label>Fiança total</label>
            <div
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            >
              {{ parseToBrl(fiancaTotal) }}
            </div>
          </div>
          <div class="flex flex-col">
            <label>Fiança policial</label>
            <div
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            >
              {{ parseToBrl(fiancaPolicial) }}
            </div>
          </div>
          <div class="flex flex-col">
            <label>Fiança advogado</label>
            <div
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            >
              {{ parseToBrl(fiancaAdvogado) }}
            </div>
          </div>
          <div class="flex flex-col">
            <label>Fiança bau</label>
            <div
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            >
              {{ parseToBrl(fiancaBau) }}
            </div>
          </div>
        </div>
        <!-- RELATÓRIO -->
        <div class="border-b py-4">
          <p class="mb-2 font-bold text-xl">RELATÓRIO:</p>
          <div class="shadow appearance-none border rounded w-full py-2 px-3">
            <p>```md</p>
            <span class="block"># INFORMAÇÕES DO PRESO:</span>
            <span class="block">⭐ NOME: {{ form.nomePreso }}</span>
            <span class="block">⭐ RG: {{ form.passaportePreso }}</span>
            <div v-if="form.passaporteAdvogado">
              <br />
              <span class="block"># INFORMAÇÕES DO ADVOGADO:</span>
              <span class="block">⭐ RG: {{ form.passaporteAdvogado }}</span>
            </div>
            <br />
            <span class="block"
              ># PENA TOTAL: {{ Math.floor(pena) }} ({{
                100 - somaAtenuantes
              }}%)</span
            >
            <span class="block"># MULTA: {{ multa }} (100%)</span>
            <div v-if="crimes.length">
              <br />
              <span class="block"># CRIMES:</span>
              <span class="block" v-for="(crime, index) in crimes" :key="index">
                {{ crime.label }}
              </span>
            </div>
            <div v-if="form.itensApreendidos">
              <br />
              <span class="block">#ITENS APREENDIDOS</span>
              <span
                class="block"
                v-html="form.itensApreendidos"
                style="white-space: break-spaces"
              ></span>
            </div>
            <div v-if="somaAtenuantes > 0">
              <br />
              <span class="block"># ATENUANTES:</span>
              <span
                class="block"
                v-for="(atenuante, index) in atenuantes.filter(
                  (el) => el.selected
                )"
                :key="index"
              >
                {{ atenuante.label }}
              </span>
            </div>
            <br />
            <span class="block"
              ># 📋 Porte de arma:
              {{
                atenuantes.filter(
                  (el) => el.label == "📋 Possui porte de arma"
                )[0].selected
                  ? "Sim"
                  : "Não"
              }}</span
            >
            <br />
            <span class="block">⭐ DATA: {{ dataHora }}</span>
            <p>```</p>
          </div>
        </div>
        <div class="mt-4">
          <button
            class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
            @click="copiar"
          >
            Copiar
          </button>
        </div>
      </div>
    </div>
    <div class="grid grid-cols-1 gap-4 mt-4"></div>
  </div>
</template>

<script>
import TextInput from "./textInput.vue";

export default {
  vue: {
    compilerOptions: {
      isCustomElement: (tag) => tag === "textearea",
    },
  },
  components: {
    TextInput,
  },
  data() {
    return {
      form: {
        passaportePreso: null,
        nomePreso: null,
        passaporteAdvogado: null,
        itensApreendidos: null,
        reincidente: false,
        dinheiroSujo: null,
        mandato: false,
      },
      crimesContraVida: [
        {
          label: "Art. 5 - Tentativa de Homicídio**",
          selected: false,
          pena: 5,
          multa: 3000,
          fianca: null,
        },
        {
          label: "Art. 6 - Homicídio Culposo",
          selected: false,
          pena: 5,
          multa: 5000,
          fianca: 2500,
        },
        {
          label: "Art. 7 - Homicídio Doloso**",
          selected: false,
          pena: 10,
          multa: 5000,
          fianca: null,
        },
        {
          label: "Art. 8 - Homicídio Doloso Qualificado**",
          selected: false,
          pena: 10,
          multa: 5000,
          fianca: null,
        },
        {
          label: "Art. 9 - Omissão de Socorro",
          selected: false,
          pena: 4,
          multa: 2000,
          fianca: 4000,
        },
        {
          label: "Art. 10 - Lesão Corporal",
          selected: false,
          pena: 2,
          multa: 1000,
          fianca: 3000,
        },
      ],
      crimesContraDireitosFundamentais: [
        {
          label: "Art. 11 - Sequestro**",
          selected: false,
          pena: 10,
          multa: 5000,
          fianca: null,
        },
        {
          label: "Art. 12 - Assédio Moral**",
          selected: false,
          pena: 10,
          multa: 50000,
          fianca: null,
        },
        {
          label: "Art. 13 - Calúnia, Injúria ou Difamação",
          selected: false,
          pena: 5,
          multa: 2500,
          fianca: 5000,
        },
        {
          label: "Art. 14 - Invasão de Propriedade",
          selected: false,
          pena: 5,
          multa: 5000,
          fianca: 10000,
        },
        {
          label: "Art. 15 - Perturbação do Sossego Alheio",
          selected: false,
          pena: 0,
          multa: 20000,
          fianca: 40000,
        },
      ],
      crimesContraLiberdadePessoal: [
        {
          label: "Art. 16 - Ameaça",
          selected: false,
          pena: 5,
          multa: 2500,
          fianca: 7000,
        },
        {
          label: "Art. 17 - Extorsão",
          selected: false,
          pena: 5,
          multa: 10000,
          fianca: 12000,
        },
      ],
      crimesContraAdministracaoPublica: [
        {
          label: "Art. 18 - Agressão a Funcionário Público",
          selected: false,
          pena: 5,
          multa: 10000,
          fianca: null,
        },
        {
          label: "Art. 19 - Falsidade Ideológica",
          selected: false,
          pena: 5,
          multa: 4000,
          fianca: 8000,
        },
        {
          label: "Art. 20 - Prevaricação",
          selected: false,
          pena: 10,
          multa: 10000,
          fianca: 15000,
        },
        {
          label: "Art. 21 - Abuso de Autoridade",
          selected: false,
          pena: 10,
          multa: 5000,
          fianca: 8000,
        },
        {
          label: "Art. 22 - Falsa Comunicação de Crime",
          selected: false,
          pena: 3,
          multa: 1000,
          fianca: 5000,
        },
        {
          label: "Art. 23 - Tentativa de Suborno",
          selected: false,
          pena: 10,
          multa: 4000,
          fianca: 8000,
        },
        {
          label: "Art. 24 - Uso indevido do sistema de emergência",
          selected: false,
          pena: 10,
          multa: 4000,
          fianca: 8000,
        },
        {
          label: "Art. 25 - Desacato",
          selected: false,
          pena: 20,
          multa: 50000,
          fianca: null,
        },
        {
          label: "Art. 25.1 - Desacato x1",
          selected: false,
          pena: 20,
          multa: 50000,
          fianca: null,
        },
        {
          label: "Art. 25.2 - Desacato x2",
          selected: false,
          pena: 20,
          multa: 50000,
          fianca: null,
        },
        {
          label: "Art. 26 - Desobediência",
          selected: false,
          pena: 0,
          multa: 15000,
          fianca: 30000,
        },
        {
          label: "Art. 26.1 - Desobediência x1",
          selected: false,
          pena: 0,
          multa: 15000,
          fianca: 30000,
        },
        {
          label: "Art. 26.2 - Desobediência x2",
          selected: false,
          pena: 10,
          multa: 15000,
          fianca: 30000,
        },
        {
          label: "Art. 27 - Obstrução de Justiça",
          selected: false,
          pena: 5,
          multa: 15000,
          fianca: 20000,
        },
        {
          label: "Art. 28 - Ocultação de Provas",
          selected: false,
          pena: 4,
          multa: 2500,
          fianca: 5000,
        },
        {
          label: "Art. 29 - Resistência a Prisão",
          selected: false,
          pena: 10,
          multa: 15000,
          fianca: 30000,
        },
      ],
      crimesContraPatrimonio: [
        {
          label: "Art. 59 - Desmanche de Veículos",
          selected: false,
          pena: 10,
          multa: 5000,
          fianca: 10000,
        },
        {
          label: "Art. 60 - Roubo",
          selected: false,
          pena: 5,
          multa: 2000,
          fianca: 5000,
        },
        {
          label: "Art. 61 - Furto a Caixa Eletrônico",
          selected: false,
          pena: 10,
          multa: 10000,
          fianca: 30000,
        },
        {
          label: "Art. 62 - Furto",
          selected: false,
          pena: 5,
          multa: 5000,
          fianca: 10000,
        },
        {
          label: "Art. 63 - Receptação de Veículos",
          selected: false,
          pena: 5,
          multa: 5000,
          fianca: 10000,
        },
        {
          label: "Art. 64 - Roubo de Veículos",
          selected: false,
          pena: 10,
          multa: 6000,
          fianca: 11000,
        },
        {
          label: "Art. 65 - Tentativa de Furto",
          selected: false,
          pena: 5,
          multa: 8000,
          fianca: 12000,
        },
        {
          label: "Art. 66 - Furto de Veículos",
          selected: false,
          pena: 6,
          multa: 1000,
          fianca: 5000,
        },
      ],
      crimesContraOrdemPublica: [
        {
          label: "Art. 30 - Dano a Patrimônio Público",
          selected: false,
          pena: 5,
          multa: 2000,
          fianca: 4000,
        },
        {
          label: "Art. 31 - Atentado ao Pudor",
          selected: false,
          pena: 10,
          multa: 10000,
          fianca: 20000,
        },
        {
          label: "Art. 32 - Formação de Quadrilha",
          selected: false,
          pena: 8,
          multa: 5000,
          fianca: 9000,
        },
        {
          label: "Art. 33 - Apologia ao Crime",
          selected: false,
          pena: 5,
          multa: 3000,
          fianca: 5000,
        },
        {
          label: "Art. 34 - Posse de Arma em Público",
          selected: false,
          pena: 5,
          multa: 2000,
          fianca: 5000,
        },
        {
          label: "Art. 35 - Uso de Máscara",
          selected: false,
          pena: 0,
          multa: 5000,
          fianca: 10000,
        },
        {
          label: "Art. 36 - Uso de Equipamentos Restritos",
          selected: false,
          pena: 5,
          multa: 5000,
          fianca: 7000,
        },
        {
          label: "Art. 37 - Vadiagem",
          selected: false,
          pena: 5,
          multa: 10000,
          fianca: 15000,
        },
        {
          label: "Art. 38 - Tentativa de Fuga",
          selected: false,
          pena: 10,
          multa: 5000,
          fianca: 10000,
        },
        {
          label: "Art. 39 - Vandalismo",
          selected: false,
          pena: 5,
          multa: 4000,
          fianca: 8000,
        },
        {
          label: "Art. 40 - Réu Reincidente",
          selected: false,
          pena: 5,
          multa: 0,
          fianca: 0,
        },
        {
          label: "Art. 41 - Cúmplice",
          selected: false,
          pena: 0,
          multa: 0,
          fianca: 5000,
        },
        {
          label: "Art. 42 - Tráfico de Armas",
          selected: false,
          pena: 10,
          multa: 10000,
          fianca: 20000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de armas",
        },
        {
          label: "Art. 43 - Tráfico de Itens Ilegais",
          selected: false,
          pena: 10,
          multa: 15000,
          fianca: 20000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de itens ilegais",
        },
        {
          label: "Art. 44 - Tráfico de Munições (+100)",
          selected: false,
          pena: 8,
          multa: 5000,
          fianca: 8000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de munições",
        },
        {
          label: "Art. 45 - Tráfico de Drogas (+100)",
          selected: false,
          pena: 10,
          multa: 50000,
          fianca: 80000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de drogas",
        },
        {
          label: "Art. 46 - Porte de Arma Pesada",
          selected: false,
          pena: 5,
          multa: 15000,
          fianca: 20000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de armas pesadas",
        },
        {
          label: "Art. 47 - Porte de Arma Leve",
          selected: false,
          pena: 3,
          multa: 10000,
          fianca: 15000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de armas leves",
        },
        {
          label: "Art. 48 - Porte de Arma Branca",
          selected: false,
          pena: 0,
          multa: 5000,
          fianca: 7000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de armas brancas",
        },
        {
          label: "Art. 49 - Posse de Peças de Armas",
          selected: false,
          pena: 5,
          multa: 10000,
          fianca: 15000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de peças de armas",
        },
        {
          label: "Art. 50 - Posse de Cápsulas",
          selected: false,
          pena: 5,
          multa: 10000,
          fianca: 15000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de cápsulas",
        },
        {
          label: "Art. 51 - Disparo de Arma de Fogo",
          selected: false,
          pena: 4,
          multa: 5000,
          fianca: 10000,
        },
        {
          label: "Art. 52 - Posse de Munição (-100)",
          selected: false,
          pena: 3,
          multa: 5000,
          fianca: 8000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de munições",
        },
        {
          label: "Art. 53 - Posse de Colete",
          selected: false,
          pena: 2,
          multa: 1000,
          fianca: 5000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de coletes",
        },
        {
          label: "Art. 54 - Aviãozinho (6 a 100)",
          selected: false,
          pena: 20,
          multa: 15000,
          fianca: 30000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de drogas",
        },
        {
          label: "Art. 55 - Posse de Componentes Narcóticos",
          selected: false,
          pena: 10,
          multa: 5000,
          fianca: 10000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de narcóticos",
        },
        {
          label: "Art. 56 - Posse de Drogas (1 a 5)",
          selected: false,
          pena: 0,
          multa: 10000,
          fianca: 0,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de drogas",
        },
        {
          label: "Art. 57 - Posse de Itens Ilegais",
          selected: false,
          pena: 5,
          multa: 10000,
          fianca: 15000,
          itemsRequired: true,
          errorMessage: "Preencha a quantidade de itens ilegais",
        },
        {
          label: "Art. 58 - Dinheiro Sujo",
          selected: false,
          pena: 10,
          multa: 100,
          fianca: 20000,
        },
      ],
      crimesDeTransito: [
        {
          label: "Art. 67 - Condução Imprudente",
          selected: false,
          pena: 2,
          multa: 1000,
          fianca: 2500,
        },
        {
          label: "Art. 68 - Dirigir na Contra Mão",
          selected: false,
          pena: 0,
          multa: 15000,
          fianca: 0,
        },
        {
          label: "Art. 69 - Alta Velocidade",
          selected: false,
          pena: 0,
          multa: 10000,
          fianca: 0,
        },
        {
          label: "Art. 70 - Poluição Sonora",
          selected: false,
          pena: 0,
          multa: 10000,
          fianca: 0,
        },
        {
          label: "Art. 71 - Corridas Ilegais",
          selected: false,
          pena: 5,
          multa: 25000,
          fianca: 0,
        },
        {
          label: "Art. 72 - Uso Excessivo de Insulfilm",
          selected: false,
          pena: 0,
          multa: 10000,
          fianca: 0,
        },
        {
          label: "Art. 73 - Veículo Irregular",
          selected: false,
          pena: 0,
          multa: 5000,
          fianca: 0,
        },
        {
          label: "Art. 74 - Estacionar em área proibida",
          selected: false,
          pena: 0,
          multa: 5000,
          fianca: 0,
        },
        {
          label: "Art. 75 - Não Ceder Passagem a Viaturas",
          selected: false,
          pena: 0,
          multa: 2000,
          fianca: 0,
        },
        {
          label: "Art. 76 - Impedir o Fluxo do Tráfego",
          selected: false,
          pena: 0,
          multa: 2000,
          fianca: 0,
        },
      ],
      atenuantes: [
        {
          label: "🔹 Advogado constituído: Redução de 30% na pena total",
          selected: false,
          reducao: 30,
        },
        {
          label: "🔹 Réu primário: Redução de 20% na pena total.",
          selected: false,
          reducao: 20,
        },
        {
          label: "🔹 Réu confesso: Redução de 20% na pena total.",
          selected: false,
          reducao: 20,
        },
        {
          label: "📋 Possui porte de arma",
          selected: false,
          reducao: 0,
        },
        {
          label:
            "🏥 REANIMADO NO HP: Reduzir os minutos tomados até o hospital (obrigatório sempre que o preso tiver sido reanimado)",
          selected: false,
          reducao: 30,
        },
      ],
    };
  },

  computed: {
    crimes() {
      let crimesContraVida = this.crimesContraVida?.filter((el) => el.selected);
      let crimesContraDireitosFundamentais =
        this.crimesContraDireitosFundamentais?.filter((el) => el.selected);
      let crimesContraLiberdadePessoal =
        this.crimesContraLiberdadePessoal?.filter((el) => el.selected);
      let crimesContraAdministracaoPublica =
        this.crimesContraAdministracaoPublica?.filter((el) => el.selected);
      let crimesContraPatrimonio = this.crimesContraPatrimonio?.filter(
        (el) => el.selected
      );
      let crimesContraOrdemPublica = this.crimesContraOrdemPublica?.filter(
        (el) => el.selected
      );
      let crimesDeTransito = this.crimesDeTransito?.filter((el) => el.selected);

      return [
        ...crimesContraVida,
        ...crimesContraDireitosFundamentais,
        ...crimesContraLiberdadePessoal,
        ...crimesContraAdministracaoPublica,
        ...crimesContraPatrimonio,
        ...crimesContraOrdemPublica,
        ...crimesDeTransito,
      ];
    },
    pena() {
      if (!this.crimes.length) return "100";

      let total = this.crimes.reduce((a, b) => a + b.pena, 0);

      if (this.somaAtenuantes > 0) {
        total = total - (total * this.somaAtenuantes) / 100;
      }

      if (total > 100) {
        return 100;
      }

      return total;
    },
    multa() {
      if (!this.crimes.length) return "0,00";

      if (this.crimes.length == 1) {
        return this.parseToBrl(this.crimes[0].multa);
      }

      return this.parseToBrl(this.crimes.reduce((a, b) => a + b.multa, 0));
    },
    somaAtenuantes() {
      let atenuantes = this.atenuantes.filter((el) => el.selected);

      return atenuantes.reduce((a, b) => a + b.reducao, 0);
    },
    dataHora() {
      return new Date().toLocaleString("pt-br", {
        day: "2-digit",
        month: "2-digit",
        year: "numeric",
        hour: "2-digit",
        minute: "2-digit",
      });
    },
    fiancaTotal() {
      const semFianca =
        this.crimes.some((a) => a.fianca === null) || this.form.mandato;

      if (semFianca) {
        return 0;
      }

      let fianca = this.crimes.reduce((a, b) => a + b.fianca, 0);

      if (this.form.dinheiroSujo) {
        let dinheiroSujo = parseFloat(
          this.form.dinheiroSujo.replaceAll(".", "").replaceAll(",", ".")
        );
        fianca += dinheiroSujo / 2;
      }

      return fianca * 1.3;
    },
    fiancaPolicial() {
      const fiancaTotal = this.fiancaTotal;

      if (fiancaTotal == 0) {
        return 0;
      }

      return fiancaTotal * 0.35;
    },
    fiancaAdvogado() {
      const fiancaTotal = this.fiancaTotal;

      if (fiancaTotal == 0) {
        return 0;
      }

      return fiancaTotal * 0.3;
    },
    fiancaBau() {
      const fiancaTotal = this.fiancaTotal;

      if (fiancaTotal == 0) {
        return 0;
      }

      return fiancaTotal * 0.35;
    },
  },
  methods: {
    toggleSelectedCrime(crime) {
      crime.selected = !crime.selected;
    },
    parseToBrl(value) {
      if (!value) return "R$ 0,00";

      return value.toLocaleString("pt-br", {
        style: "currency",
        currency: "BRL",
      });
    },
    toggleReincidente() {
      this.crimesContraOrdemPublica[10].selected =
        !this.crimesContraOrdemPublica[10].selected;
    },
    toggleMandato() {
      this.form.mandato = !this.form.mandato;
    },
    moeda() {
      if (!this.form.dinheiroSujo) return "0,00";

      let v = this.form.dinheiroSujo;
      v = v.replace(/\D/g, "");
      v = v.replace(/(\d{1})(\d{14})$/, "$1.$2");
      v = v.replace(/(\d{1})(\d{11})$/, "$1.$2");
      v = v.replace(/(\d{1})(\d{8})$/, "$1.$2");
      v = v.replace(/(\d{1})(\d{5})$/, "$1.$2");
      v = v.replace(/(\d{1})(\d{1,2})$/, "$1,$2");

      this.form.dinheiroSujo = v;
    },
    copiar() {
      let crimes = this.crimes;

      if (
        crimes.some(
          (el) => el.itemsRequired && el.selected && !this.form.itensApreendidos
        )
      ) {
        let message = crimes
          .filter((el) => el.itemsRequired && el.selected)
          .map((el) => el.errorMessage);
        alert(message);
      }
    },
  },
};
</script>
