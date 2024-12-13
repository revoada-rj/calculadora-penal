<template>
  <div class="grid grid-cols-1 md:grid-cols-12 gap-4 mt-8">
    <div class="col-span-1"></div>
    <div class="col-span-10 border rounded-lg">
      <div class="flex items-center py-4 px-4 border-b gap-8 active-tab">
        <div class="flex flex-col font-bold" :class="{'active-tab': activeTab == index}" v-for="(tab, index) in tabs"
          :key="index" v-show="index == activeTab" @click="selectTab(index)">
          <span class="text-6xl">{{(index + 1).toString().padStart(2, '0')}}</span>
          <span class="text-sm">{{tab}}</span>
        </div>
        <!-- <span style="font-size: 24px; font-weight: bolder; cursor: pointer" @click="previousTab">
          &lt;
        </span>
        
        <span style="font-size: 24px; font-weight: bolder; cursor: pointer" @click="nextTab">&gt;</span> -->
      </div>
      <!-- stepper -->
      <div class="p-4">
        <div v-if="activeTab == 0">
          <text-input label="Passaporte do preso" v-model="form.passaportePreso" type="number" />
          <text-input label="Nome do preso" v-model="form.nomePreso" type="text" />
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div>
            <!-- step 0 -->
            <div v-if="activeTab == 1">
              <div class="">
                <p class="mb-2 font-bold text-xl">CRIMES CONTRA A VIDA:</p>
                <div v-for="(crime, index) in crimesContraVida" :key="index" @click="toggleSelectedCrime(crime)"
                  class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-blue-100 transition ease-in-out delay-50 flex flex-col"
                  :class="{
                  'text-blue-600': crime.selected,
                  'bg-blue-100': crime.selected,
                }">
                  <span>{{ crime.label }}</span>
                  <span v-if="crime.subtitle" style="font-size: 12px" class="text-gray-400">{{ crime.subtitle }}</span>
                </div>
              </div>
            </div>
            <!-- CRIMES CONTRA DIREITOS FUNDAMENTAIS -->
            <div v-if="activeTab == 2">
              <p class="mb-2 font-bold text-xl">
                CRIMES CONTRA DIREITOS FUNDAMENTAIS:
              </p>
              <div v-for="(crime, index) in crimesContraDireitosFundamentais" :key="index"
                @click="toggleSelectedCrime(crime)"
                class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-blue-100 transition ease-in-out delay-50"
                :class="{
                  'text-blue-600': crime.selected,
                  'bg-blue-100': crime.selected,
                }">
                {{ crime.label }}
              </div>
            </div>
            <!-- CRIMES CONTRA A LIBERDADE PESSOAL -->
            <div v-if="activeTab == 3">
              <p class="mb-2 font-bold text-xl">
                CRIMES CONTRA A LIBERDADE PESSOAL:
              </p>
              <div v-for="(crime, index) in crimesContraLiberdadePessoal" :key="index"
                @click="toggleSelectedCrime(crime)"
                class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-blue-100 transition ease-in-out delay-50"
                :class="{
                  'text-blue-600': crime.selected,
                  'bg-blue-100': crime.selected,
                }">
                {{ crime.label }}
              </div>
            </div>
            <!-- CRIMES CONTRA A ADMINISTRAÇÃO PÚBLICA -->
            <div v-if="activeTab == 4">
              <p class="mb-2 font-bold text-xl">
                CRIMES CONTRA A ADMINISTRAÇÃO PÚBLICA:
              </p>
              <div v-for="(crime, index) in crimesContraAdministracaoPublica" :key="index"
                @click="toggleSelectedCrime(crime)"
                class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-blue-100 transition ease-in-out delay-50"
                :class="{
                  'text-blue-600': crime.selected,
                  'bg-blue-100': crime.selected,
                }">
                {{ crime.label }}
              </div>
            </div>
            <!-- CRIMES CONTRA O PATRIMÔNIO -->
            <div v-if="activeTab == 5">
              <p class="mb-2 font-bold text-xl">CRIMES CONTRA O PATRIMÔNIO:</p>
              <div v-for="(crime, index) in crimesContraPatrimonio" :key="index" @click="toggleSelectedCrime(crime)"
                class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-blue-100 transition ease-in-out delay-50"
                :class="{
                  'text-blue-600': crime.selected,
                  'bg-blue-100': crime.selected,
                }">
                {{ crime.label }}
              </div>
            </div>
            <!-- CRIMES CONTRA A ORDEM PÚBLICA -->
            <div v-if="activeTab == 6">
              <p class="mb-2 font-bold text-xl">CRIMES CONTRA A ORDEM PÚBLICA:</p>
              <div v-for="(crime, index) in crimesContraOrdemPublica" :key="index" @click="toggleSelectedCrime(crime)"
                class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-blue-100 transition ease-in-out delay-50 flex flex-col"
                :class="{
                  'text-blue-600': crime.selected,
                  'bg-blue-100': crime.selected,
                }">
                <span>{{ crime.label }}</span>
                <span v-if="crime.subtitle" style="font-size: 12px" class="text-gray-400">{{ crime.subtitle }}</span>
              </div>
              <!-- ITENS APREENDIDOS -->
              <div class="border-b py-4 md:border-b-0 py-4" style="position: relative">
                <p class="mb-2 font-bold text-xl">ITENS APREENDIDOS:</p>

                <textarea v-model="form.itensApreendidos" ref="itensApreendidos" v-if="form.dinheiroSujo"
                  class="shadow appearance-none border rounded w-full h-[150px] py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                  style="padding-top: 30px;">
                </textarea>
                <textarea v-model="form.itensApreendidos" ref="itensApreendidos" v-else
                  class="shadow appearance-none border rounded w-full h-[150px] py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                </textarea>

                <span v-if="form.dinheiroSujo"
                  style="position: absolute; top: 60px; left: 13px; color: rgb(55, 65, 81)">R$ {{ form.dinheiroSujo }}
                  dinheiro sujo</span>

                <div v-if="crimesContraOrdemPublica[28].selected">
                  <p class="mb-2 font-bold text-xl">DINHEIRO SUJO:</p>
                  <text-input @keyup="moeda" v-model="form.dinheiroSujo" type="text" />
                </div>
              </div>
            </div>
            <!-- CRIMES DE TRÂNSITO -->
            <div v-if="activeTab == 7">
              <p class="mb-2 font-bold text-xl">CRIMES DE TRÂNSITO:</p>
              <div v-for="(crime, index) in crimesDeTransito" :key="index" @click="toggleSelectedCrime(crime)"
                class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-blue-100 transition ease-in-out delay-50"
                :class="{
                  'text-blue-600': crime.selected,
                  'bg-blue-100': crime.selected,
                }">
                {{ crime.label }}
              </div>
            </div>
            <!-- AGRAVANTES -->
            <div v-if="activeTab == 8">
              <p class="mb-2 font-bold text-xl">SITUAÇÃO:</p>
              <div
                class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-blue-100 transition ease-in-out delay-50"
                :class="{
                  'text-blue-600': !crimesContraOrdemPublica[10].selected,
                  'bg-blue-100': !crimesContraOrdemPublica[10].selected,
                }" @click="toggleReincidente(false)">
                🔹 Réu primário
              </div>
              <div
                class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-blue-100 transition ease-in-out delay-50"
                :class="{
                  'text-blue-600': crimesContraOrdemPublica[10].selected,
                  'bg-blue-100': crimesContraOrdemPublica[10].selected,
                }" @click="toggleReincidente(true)">
                🛑 Réu reincidente
              </div>
            </div>
            <!-- ATENUANTES -->
            <div v-if=" activeTab==9">
              <p class="mb-2 font-bold text-xl">ATENUANTES:</p>
              <div v-for="(atenuante, index) in atenuantes" :key="index" @click="toggleSelectedCrime(atenuante)"
                v-show="index < 4"
                class="border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-blue-100 transition ease-in-out delay-50"
                :class="{
                  'text-blue-600': atenuante.selected,
                  'bg-blue-100': atenuante.selected,
                }">
                {{ atenuante.label }}
              </div>

              <div v-if="atenuantes[0].selected">
                <p class="mb-2 font-bold text-xl">PASSAPORTE DO ADVOGADO:</p>
                <text-input v-model="form.passaporteAdvogado" type="number" />
              </div>

              <div @click="toogleFianca()" v-if="atenuantes[0].selected"
                class="mt-2 border rounded px-3 py-3 mb-2 cursor-pointer hover:bg-blue-100 transition ease-in-out delay-50"
                :class="{
                  'text-blue-600': fiancaPaga,
                  'bg-blue-100': fiancaPaga,
                }">
                🔹 Fiança Paga
              </div>

            </div>
          </div>
          <div v-if="activeTab > 0 && activeTab < tabs.length - 1">
            <!-- RELATÓRIO -->
            <div class="border-b">
              <p class="mb-2 font-bold text-xl">PRÉ VISUALIZAÇÃO:</p>
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
                <span class="block"># PENA TOTAL: {{ Math.floor(pena) }} ({{
                  100 - somaAtenuantes
                  }}%)</span>
                <span class="block"># MULTA: {{ multa }} (100%)</span>
                <div v-if="crimesContraOrdemPublica[28].selected">
                  <br>
                  <span class="block"># DINHEIRO SUJO</span>
                  <span class="block">R$ {{ form.dinheiroSujo }}</span>
                </div>
                <div v-if="crimes.length">
                  <br />
                  <span class="block"># CRIMES:</span>
                  <span class="block flex items-center gap-2" v-for="(crime, index) in crimes" :key="index">
                    {{ crime.label }}
                    <div class="items-center justify-center text-red-800 cursor-pointer hover:text-red-100"
                      @click="remover(crime)">
                      <span title="Remover crime">x</span>
                    </div>
                  </span>
                </div>
                <div v-if="form.itensApreendidos || form.dinheiroSujo">
                  <br />
                  <span class="block"># ITENS APREENDIDOS</span>
                  <span v-if="form.dinheiroSujo" class="block" style="white-space: break-spaces">R$ {{ form.dinheiroSujo
                  }} dinheiro sujo</span>
                  <span class="block" v-html="form.itensApreendidos" style="white-space: break-spaces"></span>
                </div>
                <div v-if="somaAtenuantes > 0">
                  <br />
                  <span class="block"># ATENUANTES:</span>
                  <span class="block flex items-center gap-2" v-for="(atenuante, index) in atenuantes.filter(
                    (el) => el.selected
                  )" :key="index">
                    {{ atenuante.label }}
                    <div class="items-center justify-center text-red-800 cursor-pointer hover:text-red-100"
                      @click="remover(atenuante)">
                      <span title="Remover atenuante">x</span>
                    </div>
                  </span>
                </div>
                <br />
                <span class="block"># 📋 Porte de arma:
                  {{
                  atenuantes.filter(
                  (el) => el.label == "📋 Possui porte de arma"
                  )[0].selected
                  ? "Sim"
                  : "Não"
                  }}</span>

                <div v-if="fiancaPaga">
                  <br>
                  <span class="block">⭐ 🔹 Fiança paga</span>
                </div>
                <br />
                <span class="block">⭐ DATA: {{ dataHora }}</span>
                <p>```</p>
              </div>
            </div>
          </div>
        </div>
        <!-- RESUMO -->
        <div v-if="activeTab == 10">
          <div class="grid grid-cols-1">
            <div class="shadow appearance-none border rounded w-full py-2 px-3">
              <h1 class="text-xl font-bold mb-4">Dados do Preso</h1>
              <div class="flex gap-1">
                <span class="font-bold">Passaporte: </span>
                <span>{{form.passaportePreso}}</span>
              </div>
              <div class="flex gap-1">
                <span class="font-bold">Nome: </span>
                <span>{{form.nomePreso}}</span>
              </div>
              <div class="flex gap-1" v-if="form.passaporteAdvogado">
                <span class="font-bold">Passaporte do advogado: </span>
                <span>{{form.passaporteAdvogado}}</span>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
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
                <span class="block"># PENA TOTAL: {{ Math.floor(pena) }} ({{
                  100 - somaAtenuantes
                  }}%)</span>
                <span class="block"># MULTA: {{ multa }} (100%)</span>
                <div v-if="crimesContraOrdemPublica[28].selected">
                  <br>
                  <span class="block"># DINHEIRO SUJO</span>
                  <span class="block">R$ {{ form.dinheiroSujo }}</span>
                </div>
                <div v-if="crimes.length">
                  <br />
                  <span class="block"># CRIMES:</span>
                  <span class="block flex items-center gap-2" v-for="(crime, index) in crimes" :key="index">
                    {{ crime.label }}
                    <div class="items-center justify-center text-red-800 cursor-pointer hover:text-red-100"
                      @click="remover(crime)">
                      <span title="Remover crime">x</span>
                    </div>
                  </span>
                </div>
                <div v-if="form.itensApreendidos || form.dinheiroSujo">
                  <br />
                  <span class="block">#ITENS APREENDIDOS</span>
                  <span v-if="form.dinheiroSujo" class="block" style="white-space: break-spaces">R$ {{ form.dinheiroSujo
                    }} dinheiro sujo</span>
                  <span class="block" v-html="form.itensApreendidos" style="white-space: break-spaces"></span>
                </div>
                <div v-if="somaAtenuantes > 0">
                  <br />
                  <span class="block"># ATENUANTES:</span>
                  <span class="block flex items-center gap-2" v-for="(atenuante, index) in atenuantes.filter(
                    (el) => el.selected
                  )" :key="index">
                    {{ atenuante.label }}
                    <div class="items-center justify-center text-red-800 cursor-pointer hover:text-red-100"
                      @click="remover(atenuante)">
                      <span title="Remover atenuante">x</span>
                    </div>
                  </span>
                </div>
                <br />
                <span class="block"># 📋 Porte de arma:
                  {{
                  atenuantes.filter(
                  (el) => el.label == "📋 Possui porte de arma"
                  )[0].selected
                  ? "Sim"
                  : "Não"
                  }}</span>
                <div v-if="fiancaPaga">
                  <br>
                  <span class="block">⭐ 🔹 Fiança paga</span>
                </div>
                <br />
                <span class="block">⭐ DATA: {{ dataHora }}</span>
                <p>```</p>
              </div>
            </div>
            <!-- FIANÇA -->
            <div class="border-b py-4">
              <p class="mb-2 font-bold text-xl">FIANÇA:</p>
              <div class="shadow appearance-none border rounded w-full py-2 px-3">
                <div class="flex flex-col">
                  <label>Multa</label>
                  <div
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                    {{ parseToBrl(multa) }}
                  </div>
                </div>
                <div class="flex flex-col">
                  <label>Fiança total</label>
                  <div
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                    {{ parseToBrl(fiancaTotal) }}
                  </div>
                </div>
                <div class="flex flex-col">
                  <label>Fiança policial</label>
                  <div
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                    {{ parseToBrl(fiancaPolicial) }}
                  </div>
                </div>
                <div class="flex flex-col">
                  <label>Fiança advogado</label>
                  <div
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                    {{ parseToBrl(fiancaAdvogado) }}
                  </div>
                </div>
                <div class="flex flex-col">
                  <label>Fiança bau</label>
                  <div
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                    {{ parseToBrl(fiancaBau) }}
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="my-4 flex gap-4">
          <button class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded" v-if="activeTab > 0"
            @click="activeTab--">Anterior</button>
          <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
            v-if="activeTab < tabs.length - 1" @click="nextTab()">Próximo</button>
          <button class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded"
            v-if="activeTab == tabs.length - 1" @click="copiar">Copiar</button>
        </div>
      </div>

    </div>
    <div></div>
  </div>
  <div class="fixed flex items-center justify-center" style="
        z-index: 9999999999999999999999;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        background: rgb(0, 0, 0, 0.3);
      " v-if="displayError">
    <div class="rounded bg-slate-50 shadow py-5 px-5 w-2/3 md:w-1/3">
      <div class="flex items-center justify-between mb-4">
        <p class="text-2xl font-bold">Atenção!</p>
        <span class="font-bold text-xl cursor-pointer hover:text-slate-500 transition ease-in-out"
          @click="displayError = false">X</span>
      </div>
      <p class="mb-1" v-for="(message, index) in errorMessage" :key="index">
        {{ message }}
      </p>
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mt-4"
        @click="displayError = false">
        Entendi
      </button>
    </div>
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
            subtitle: "Quando um individuo tenta matar alguém, mas não consegue.",
            selected: false,
            pena: 5,
            multa: 20000,
            fianca: null,
          },
          {
            label: "Art. 6 - Homicídio Culposo",
            subtitle: "Quando um indivíduo mata alguém sem intenção.",
            selected: false,
            pena: 5,
            multa: 5000,
            fianca: 2500,
          },
          {
            label: "Art. 7 - Homicídio Doloso**",
            subtitle: "Quando um indivíduo mata alguém de propósito, utilizando de meios cruéis.",
            selected: false,
            pena: 10,
            multa: 25000,
            fianca: null,
          },
          {
            label: "Art. 8 - Homicídio Doloso Qualificado**",
            subtitle: "É uma forma mais grave de homicídio doloso, envolvendo circunstâncias agravantes.",
            selected: false,
            pena: 15,
            multa: 25000,
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
            pena: 7,
            multa: 10000,
            fianca: 20000,
          },
        ],
        crimesContraDireitosFundamentais: [
          {
            label: "Art. 11 - Sequestro**",
            selected: false,
            pena: 10,
            multa: 25000,
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
            pena: 10,
            multa: 5000,
            fianca: 10000,
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
            pena: 10,
            multa: 10000,
            fianca: 20000,
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
            label: "Art. 18 - Agressão a Funcionário Público**",
            selected: false,
            pena: 15,
            multa: 20000,
            fianca: null,
          },
          {
            label: "Art. 19 - Falsidade Ideológica",
            selected: false,
            pena: 5,
            multa: 10000,
            fianca: 20000,
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
            multa: 10000,
            fianca: 20000,
          },
          {
            label: "Art. 24 - Uso indevido do sistema de emergência",
            selected: false,
            pena: 10,
            multa: 4000,
            fianca: 8000,
          },
          {
            label: "Art. 25 - Desacato**",
            selected: false,
            pena: 20,
            multa: 70000,
            fianca: null,
          },
          {
            label: "Art. 25.1 - Desacato 2x**",
            selected: false,
            pena: 20,
            multa: 70000,
            fianca: null,
          },
          {
            label: "Art. 25.2 - Desacato 3x**",
            selected: false,
            pena: 20,
            multa: 70000,
            fianca: null,
          },
          {
            label: "Art. 26 - Desobediência",
            selected: false,
            pena: 5,
            multa: 15000,
            fianca: 30000,
          },
          {
            label: "Art. 26.1 - Desobediência 2x",
            selected: false,
            pena: 5,
            multa: 15000,
            fianca: 30000,
          },
          {
            label: "Art. 26.2 - Desobediência 3x",
            selected: false,
            pena: 10,
            multa: 15000,
            fianca: 30000,
          },
          {
            label: "Art. 27 - Obstrução de Justiça",
            selected: false,
            pena: 10,
            multa: 15000,
            fianca: 20000,
          },
          {
            label: "Art. 28 - Ocultação de Provas",
            selected: false,
            pena: 10,
            multa: 15000,
            fianca: 20000,
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
            multa: 10000,
            fianca: 20000,
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
            multa: 7000,
            fianca: 14000,
          },
          {
            label: "Art. 63 - Receptação de Veículos",
            selected: false,
            pena: 5,
            multa: 7000,
            fianca: 14000,
          },
          {
            label: "Art. 64 - Roubo de Veículos",
            selected: false,
            pena: 10,
            multa: 9000,
            fianca: 18000,
          },
          {
            label: "Art. 65 - Tentativa de Furto",
            selected: false,
            pena: 10,
            multa: 8000,
            fianca: 12000,
          },
          {
            label: "Art. 66 - Furto de Veículos",
            selected: false,
            pena: 10,
            multa: 9000,
            fianca: 18000,
          },
        ],
        crimesContraOrdemPublica: [
          {
            label: "Art. 30 - Dano a Patrimônio Público",
            selected: false,
            pena: 5,
            multa: 10000,
            fianca: 20000,
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
            multa: 10000,
            fianca: 20000,
          },
          {
            label: "Art. 33 - Apologia ao Crime",
            selected: false,
            pena: 10,
            multa: 15000,
            fianca: 30000,
          },
          {
            label: "Art. 34 - Posse de Arma em Público",
            selected: false,
            pena: 10,
            multa: 18000,
            fianca: 36000,
          },
          {
            label: "Art. 35 - Uso de Máscara",
            selected: false,
            pena: 0,
            multa: 10000,
            fianca: 20000,
          },
          {
            label: "Art. 36 - Uso de Equipamentos Restritos",
            selected: false,
            pena: 5,
            multa: 10000,
            fianca: 20000,
          },
          {
            label: "Art. 37 - Vadiagem",
            selected: false,
            pena: 10,
            multa: 10000,
            fianca: 15000,
          },
          {
            label: "Art. 38 - Tentativa de Fuga",
            selected: false,
            pena: 10,
            multa: 15000,
            fianca: 30000,
          },
          {
            label: "Art. 39 - Vandalismo",
            selected: false,
            pena: 5,
            multa: 10000,
            fianca: 20000,
          },
          {
            label: "Art. 40 - Réu Reincidente",
            selected: false,
            pena: 5,
            multa: 0,
            fianca: 15000,
          },
          {
            label: "Art. 41 - Cúmplice",
            selected: false,
            pena: 5,
            multa: 0,
            fianca: 15000,
          },
          {
            label: "Art. 42 - Tráfico de Armas",
            subtitle: "3 armas ou mais.",
            selected: false,
            pena: 10,
            multa: 20000,
            fianca: 40000,
            itemsRequired: true,
            errorMessage: "Preencha a quantidade de armas",
          },
          {
            label: "Art. 43 - Tráfico de Itens Ilegais",
            subtitle: "3 itens ou mais.",
            selected: false,
            pena: 10,
            multa: 15000,
            fianca: 20000,
            itemsRequired: true,
            errorMessage: "Preencha a quantidade de itens ilegais",
          },
          {
            label: "Art. 44 - Tráfico de Munições",
            subtitle: 'Acima de 100 munições.',
            selected: false,
            pena: 8,
            multa: 10000,
            fianca: 20000,
            itemsRequired: true,
            errorMessage: "Preencha a quantidade de munições",
          },
          {
            label: "Art. 45 - Tráfico de Drogas",
            subtitle: 'Acima de 100 drogas.',
            selected: false,
            pena: 10,
            multa: 50000,
            fianca: 80000,
            itemsRequired: true,
            errorMessage: "Preencha a quantidade de drogas",
          },
          {
            label: "Art. 46 - Porte de Arma Pesada",
            subtitle: "Menos de 3 armas.",
            selected: false,
            pena: 5,
            multa: 15000,
            fianca: 20000,
            itemsRequired: true,
            errorMessage: "Preencha a quantidade de armas pesadas",
          },
          {
            label: "Art. 47 - Porte de Arma Leve",
            subtitle: "Menos de 3 armas.",
            selected: false,
            pena: 5,
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
            pena: 5,
            multa: 5000,
            fianca: 10000,
          },
          {
            label: "Art. 52 - Posse de Munição",
            subtitle: "100 munições ou menos.",
            selected: false,
            pena: 5,
            multa: 10000,
            fianca: 20000,
            itemsRequired: true,
            errorMessage: "Preencha a quantidade de munições",
          },
          {
            label: "Art. 53 - Posse de Colete",
            selected: false,
            pena: 5,
            multa: 10000,
            fianca: 20000,
            itemsRequired: true,
            errorMessage: "Preencha a quantidade de coletes",
          },
          {
            label: "Art. 54 - Aviãozinho",
            subtitle: "De 6 a 100 unidades (qualquer tipo de droga).",
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
            label: "Art. 56 - Posse de Drogas",
            subtitle: "De 1 a 5 unidades (qualquer tipo de droga).",
            selected: false,
            pena: 0,
            multa: 10000,
            fianca: 0,
            itemsRequired: true,
            errorMessage: "Preencha a quantidade de drogas",
          },
          {
            label: "Art. 57 - Posse de Itens Ilegais",
            subtitle: "Menos de 3 itens.",
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
            multa: 5000,
            fianca: 0,
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
            label: "🔹 Réu confesso: Redução de 20% na pena total.",
            selected: false,
            reducao: 20,
          },
          {
            label:
              "🏥 REANIMADO NO HP: Reduzir os minutos tomados até o hospital",
            selected: false,
            reducao: 30,
          },
          {
            label: "📋 Possui porte de arma",
            selected: false,
            reducao: 0,
          },
          {
            label: "🔹 Réu primário: Redução de 20% na pena total",
            selected: true,
            reducao: 20,
          },
        ],
        errorMessage: [],
        displayError: false,
        activeTab: 0,
        tabs: [
          'DADOS DO PRESO',
          'CONTRA A VIDA',
          'CONTRA DIREITOS FUNDAMENTAIS',
          'CONTRA A LIBERDADE PESSOAL',
          'CONTRA A ADMINISTRAÇÃO PÚBLICA',
          'CONTRA O PATRIMÔNIO',
          'CONTRA A ORDEM PÚBLICA',
          'DE TRÂNSITO',
          'SITUAÇÃO',
          'ATENUANTES',
          'RESUMO',
        ],
        reuPrimario: false,
        fiancaPaga: false,
        multiplicadorMulta: 2,
        multiplicadorFianca: 4,
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

        if (total > 100) {
          total = 100
        }

        if (this.somaAtenuantes > 0) {
          total = total - (total * this.somaAtenuantes) / 100;
        }

        return total;
      },
      multa() {
        if (!this.crimes.length) return "0,00";

        if (this.crimes.length == 1) {
          let multa = this.crimes[0].multa;
          multa = multa * this.multiplicadorMulta;

          if (this.form.dinheiroSujo) {
            let dinheiroSujo = parseFloat(
              this.form.dinheiroSujo.replaceAll(".", "").replaceAll(",", ".")
            );
            multa += dinheiroSujo / 2;
          }

          return this.parseToBrl(multa);
        }

        let multa = this.crimes.reduce((a, b) => a + b.multa, 0);
        multa = multa * this.multiplicadorMulta;

        if (multa > 700000) {
          multa = 700000;
        }

        if (this.form.dinheiroSujo) {
          let dinheiroSujo = parseFloat(
            this.form.dinheiroSujo.replaceAll(".", "").replaceAll(",", ".")
          );
          multa += dinheiroSujo / 2;
        }

        return this.parseToBrl(multa);
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
        const inafiancavel =
          this.crimes.some((a) => a.fianca === null) || this.form.mandato;

        if (inafiancavel) {
          return 0;
        }

        let fianca = this.crimes.reduce((a, b) => a + b.fianca, 0);

        fianca = fianca * this.multiplicadorFianca;

        if (fianca > 600000) {
          fianca = 600000;
        }

        if (this.form.dinheiroSujo) {
          let dinheiroSujo = parseFloat(
            this.form.dinheiroSujo.replaceAll(".", "").replaceAll(",", ".")
          );
          fianca += dinheiroSujo / 2;
        }

        return fianca;
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
      selectTab(tab) {
        this.activeTab = tab;
      },
      toggleSelectedCrime(crime) {
        crime.selected = !crime.selected;

        console.log('aaaa', crime.label == 'Art. 40 - Réu Reincidente' && crime.selected)
        if (crime.label == 'Art. 40 - Réu Reincidente' && crime.selected) {
          this.form.reuPrimario = false
          this.atenuantes[4].selected = false
        } else {
          this.form.reuPrimario = true
          this.atenuantes[4].selected = true
        }
      },
      parseToBrl(value) {
        if (!value) return "R$ 0,00";

        return value.toLocaleString("pt-br", {
          style: "currency",
          currency: "BRL",
        });
      },
      toggleReincidente(situacao) {
        if (situacao) {
          this.atenuantes[4].selected = false;
          this.crimesContraOrdemPublica[10].selected = true;
          return;
        }

        this.atenuantes[4].selected = true;
        this.crimesContraOrdemPublica[10].selected = false;
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
        this.errorMessage = [];

        if (!this.form.passaportePreso) {
          this.errorMessage.push("Informe o passaporte do preso!");
        }

        if (!this.form.nomePreso) {
          this.errorMessage.push("Informe o nome do preso!");
        }

        if (this.atenuantes[0].selected && !this.form.passaporteAdvogado) {
          this.errorMessage.push("Informe o passaporte do advogado!");
        }

        if (!this.crimes.length) {
          this.errorMessage.push("Selecione ao menos um crime!");
        }

        if (this.errorMessage.length) {
          this.displayError = true;
          return;
        }

        let crimes = this.crimes;

        if (
          crimes.some(
            (el) => el.itemsRequired && el.selected && !this.form.itensApreendidos
          )
        ) {
          let messages = crimes
            .filter((el) => el.itemsRequired && el.selected)
            .map((el) => el.errorMessage);

          this.errorMessage = messages;
          this.displayError = true;
          this.activeTab = 6;
          return;
        }

        let text = "QRA:\n```md";

        text += `\n\n# INFORMAÇÕES DO PRESO:`;
        text += `\n⭐ NOME: ${this.form.nomePreso}`;
        text += `\n⭐ RG: ${this.form.passaportePreso}`;

        if (this.form.passaporteAdvogado) {
          text += `\n\n# INFORMAÇÕES DO ADVOGADO:`;
          text += `\n⭐ RG: ${this.form.passaporteAdvogado}`;
        }

        text += `\n\n# PENA TOTAL: ${Math.floor(this.pena)} meses (${100 - this.somaAtenuantes
          }%)`;

        text += `\n\n# MULTA: ${this.multa}`;

        if (this.form.dinheiroSujo) {
          text += `\n\n# DINHEIRO SUJO`;
          text += `\nR$ ${this.form.dinheiroSujo}`
        }

        text += `\n\n# CRIMES:`;

        this.crimes.map((crime) => {
          text += `\n${crime.label}`;
        });

        if (this.form.itensApreendidos || this.form.dinheiroSujo) {
          text += `\n\n# ITENS APREENDIDOS: `;

          if (this.form.dinheiroSujo) {
            text += `\nR$ ${this.form.dinheiroSujo} dinheiro sujo`;
          }

          if (this.form.itensApreendidos)
            text += `\n${this.form.itensApreendidos}`;
        }

        let atenuantes = this.atenuantes
          .filter((el) => el.selected)

        if (atenuantes) {
          text += `\n\n# ATENUANTES:`;
          atenuantes.map((atenuante) => {
            text += `\n${atenuante.label}`;
          });
        }

        let porte = this.atenuantes.filter(
          (el) => el.label == "📋 Possui porte de arma"
        )[0].selected
          ? "Sim"
          : "Não";

        text += `\n\n# 📋 Porte de arma: ${porte}`;

        if (this.fiancaPaga) {
          text += `\n\n🔹 Fiança paga`;
        }

        text += `\n\n⭐ DATA: ${this.dataHora}`;

        text += "\n```";

        let textArea = document.createElement("textarea");
        textArea.value = text;
        document.body.append(textArea);
        textArea.select();
        document.execCommand("copy");
        document.body.removeChild(textArea);

        this.errorMessage.push("Copiado");
        this.displayError = true;
      },
      nextTab() {
        let currentTab = this.activeTab;
        this.errorMessage = [];

        if (currentTab == 0) {
          if (!this.form.passaportePreso) {
            this.errorMessage.push("Informe o passaporte do preso!");
          }

          if (!this.form.nomePreso) {
            this.errorMessage.push("Informe o nome do preso!");
          }
        }

        if (currentTab == 6) {
          let crimes = this.crimes;
          if (
            crimes.some(
              (el) => el.itemsRequired && el.selected && !this.form.itensApreendidos
            )
          ) {
            let messages = crimes
              .filter((el) => el.itemsRequired && el.selected)
              .map((el) => el.errorMessage);

            this.errorMessage = messages;
            this.displayError = true;
            this.activeTab = 6;
            return;
          }

          if (this.crimesContraOrdemPublica[28].selected && (!this.form.dinheiroSujo || this.form.dinheiroSujo < 1)) {
            this.errorMessage = ['Preencha a quantidade de dinheiro sujo!'];
            this.displayError = true;
            this.activeTab = 6;
          }
        }

        if (currentTab == 9) {
          if (!this.form.passaporteAdvogado && this.atenuantes[0].selected) {
            this.errorMessage = ['Preencha o passaporte do advogado!'];
            this.displayError = true;
            this.activeTab = 9;
          }
        }

        if (this.errorMessage.length) {
          this.displayError = true;
          return;
        }

        if (this.activeTab < this.tabs.length - 1) {
          this.activeTab++;
        }
      },
      previousTab() {
        if (this.activeTab > 0) {
          this.activeTab--;
        }
      },
      toogleFianca() {
        if (this.crimes.filter(el => el.fianca === null && el.selected).length > 0) return false;

        this.fiancaPaga = !this.fiancaPaga
      },
      remover(item) {
        item.selected = false;
      }
    },
  };
</script>

<style>
  .active-tab {
    color: rgb(0, 91, 255);
    /* font-weight: bolder; */
  }
</style>