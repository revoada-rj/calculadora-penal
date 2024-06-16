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
    <div class="grid grid-cols-1 gap-4 mt-4">
      <div class="border-b pb-4">
        <p class="mb-2 font-bold text-xl">CRIMES CONTRA A VIDA:</p>
        <div
          v-for="(crime, index) in crimesContraVida"
          :key="index"
          @click="toggleSelectedCrime(crime)"
          class="border rounded px-5 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
          :class="{ 'text-green-600': crime.selected }"
        >
          {{ crime.label }}
        </div>
      </div>
      <div class="border-b pb-4">
        <p class="mb-2 font-bold text-xl">
          CRIMES CONTRA DIREITOS FUNDAMENTAIS:
        </p>
        <div
          v-for="(crime, index) in crimesContraDireitosFundamentais"
          :key="index"
          @click="toggleSelectedCrime(crime)"
          class="border rounded px-5 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
          :class="{
            'text-green-600': crime.selected,
          }"
        >
          {{ crime.label }}
        </div>
      </div>
      <div class="border-b pb-4">
        <p class="mb-2 font-bold text-xl">CRIMES CONTRA A LIBERDADE PESSOAL:</p>
        <div
          v-for="(crime, index) in crimesContraLiberdadePessoal"
          :key="index"
          @click="toggleSelectedCrime(crime)"
          class="border rounded px-5 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
          :class="{
            'text-green-600': crime.selected,
          }"
        >
          {{ crime.label }}
        </div>
      </div>
      <div class="border-b pb-4">
        <p class="mb-2 font-bold text-xl">
          CRIMES CONTRA A ADMINISTRAÇÃO PÚBLICA:
        </p>
        <div
          v-for="(crime, index) in crimesContraAdministracaoPublica"
          :key="index"
          @click="toggleSelectedCrime(crime)"
          class="border rounded px-5 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
          :class="{
            'text-green-600': crime.selected,
          }"
        >
          {{ crime.label }}
        </div>
      </div>
      <div class="border-b pb-4">
        <p class="mb-2 font-bold text-xl">CRIMES CONTRA O PATRIMÔNIO:</p>
        <div
          v-for="(crime, index) in crimesContraPatrimonio"
          :key="index"
          @click="toggleSelectedCrime(crime)"
          class="border rounded px-5 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
          :class="{
            'text-green-600': crime.selected,
          }"
        >
          {{ crime.label }}
        </div>
      </div>
      <div class="border-b pb-4">
        <p class="mb-2 font-bold text-xl">CRIMES CONTRA A ORDEM PÚBLICA:</p>
        <div
          v-for="(crime, index) in crimesContraOrdemPublica"
          :key="index"
          @click="toggleSelectedCrime(crime)"
          class="border rounded px-5 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
          :class="{
            'text-green-600': crime.selected,
          }"
        >
          {{ crime.label }}
        </div>
      </div>
      <div class="border-b pb-4">
        <p class="mb-2 font-bold text-xl">CRIMES DE TRÂNSITO:</p>
        <div
          v-for="(crime, index) in crimesDeTransito"
          :key="index"
          @click="toggleSelectedCrime(crime)"
          class="border rounded px-5 py-3 mb-2 cursor-pointer hover:bg-green-100 transition ease-in-out delay-50"
          :class="{
            'text-green-600': crime.selected,
          }"
        >
          {{ crime.label }}
        </div>
      </div>
      <div class="border-b pb-4">
        <p class="mb-2 font-bold text-xl">ITENS APREENDIDOS:</p>
        <textearea>oi</textearea>
      </div>
    </div>
  </div>
</template>

<script>
import TextInput from "./textInput.vue";

export default {
	vue: {
    compilerOptions: {
      isCustomElement: tag => tag === 'textearea'
    }
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
      },
      crimesContraVida: [
        {
          label: "Art. 5 - Tentativa de Homicídio**",
          selected: false,
          pena: 10,
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
          multa: null,
          fianca: null,
        },
        {
          label: "Art. 25.1 - Desacato x1",
          selected: false,
          pena: 20,
          multa: null,
          fianca: null,
        },
        {
          label: "Art. 25.2 - Desacato x2",
          selected: false,
          pena: 20,
          multa: null,
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
        },
        {
          label: "Art. 43 - Tráfico de Itens Ilegais",
          selected: false,
          pena: 10,
          multa: 15000,
          fianca: 20000,
        },
        {
          label: "Art. 44 - Tráfico de Munições (+100)",
          selected: false,
          pena: 8,
          multa: 5000,
          fianca: 8000,
        },
        {
          label: "Art. 45 - Tráfico de Drogas (+100)",
          selected: false,
          pena: 10,
          multa: 50000,
          fianca: 80000,
        },
        {
          label: "Art. 46 - Porte de Arma Pesada",
          selected: false,
          pena: 5,
          multa: 15000,
          fianca: 20000,
        },
        {
          label: "Art. 47 - Porte de Arma Leve",
          selected: false,
          pena: 3,
          multa: 10000,
          fianca: 15000,
        },
        {
          label: "Art. 48 - Porte de Arma Branca",
          selected: false,
          pena: 0,
          multa: 5000,
          fianca: 7000,
        },
        {
          label: "Art. 49 - Posse de Peças de Armas",
          selected: false,
          pena: 5,
          multa: 10000,
          fianca: 15000,
        },
        {
          label: "Art. 50 - Posse de Cápsulas",
          selected: false,
          pena: 5,
          multa: 10000,
          fianca: 15000,
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
        },
        {
          label: "Art. 53 - Posse de Colete",
          selected: false,
          pena: 2,
          multa: 1000,
          fianca: 5000,
        },
        {
          label: "Art. 54 - Aviãozinho (6 a 100)",
          selected: false,
          pena: 20,
          multa: 15000,
          fianca: 30000,
        },
        {
          label: "Art. 55 - Posse de Componentes Narcóticos",
          selected: false,
          pena: 10,
          multa: 5000,
          fianca: 10000,
        },
        {
          label: "Art. 56 - Posse de Drogas (1 a 5)",
          selected: false,
          pena: 0,
          multa: 10000,
          fianca: 0,
        },
        {
          label: "Art. 57 - Posse de Itens Ilegais",
          selected: false,
          pena: 5,
          multa: 10000,
          fianca: 15000,
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
    };
  },
  methods: {
    toggleSelectedCrime(crime) {
      crime.selected = !crime.selected;
    },
  },
};
</script>
