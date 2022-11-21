<script setup lang="ts">
import Sections from "./TheSection.vue";
import Form from "./TheForrm.vue";
import IconBagCoin from "./icons/IconBagCoin.vue";
import BannerIcon from "./icons/IconBanner.vue";
import LaptopIcon from "./icons/IconLaptop.vue";
import LogoIcon from "./icons/IconLogo.vue";
</script>

<template>
  <Sections class="bg-purple logo">
    <template #icon><LogoIcon /></template>
  </Sections>

  <Sections class="bg-purple primary">
    <template #heading>Chega de esperar o fim do mês!</template>

    A Empresa proporciona para seus clientes uma solução inovadora que
    transforma radicalmente o dia a dia do RH.

    <template #icon>
      <BannerIcon />
    </template>
  </Sections>

  <Sections class="bg-orange secondary">
    <template #heading>De básico a folha Empresa não tem nada!</template>

    Nosso padrão de folha é o mais completo do mercado! <br />
    Diferente dos outros fornecedores, nossos KPI's, Workflow, Gestão de
    benefícios e eSocial fazem parte do sistema Folha de Pagamentos Empresa sem
    custos adicionais!

    <template #icon>
      <IconBagCoin />
    </template>
  </Sections>

  <div class="asides">
    <Sections class="bg-purple tertiary">
      <template #icon>
        <LaptopIcon />
      </template>
      Quer levar a Empresa para o seu dia a dia?
    </Sections>

    <Form class="bg-orange" />
  </div>
</template>

<style>
.logo .item {
  padding: 30px 25px;
}

.logo i {
  max-width: 140px;
  margin: 0 auto 0 0;
}

.primary h2 {
  max-width: 800px;
}

.primary .details {
  max-width: 645px;
}

.secondary .item {
  padding-top: 60px;
}

.secondary h2 {
  max-width: 1090px;
}

.secondary .details {
  max-width: 686px;
}

.secondary i {
  margin: 0 -25px 0 auto;
}

.asides {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.tertiary {
  width: 100%;
}

.tertiary .details {
  font-size: 1.875rem;
  line-height: 2.813rem;
  max-width: 335px;
  margin: 60px auto 30px;
}

@media screen and (min-width: 1215px) {
  .logo .item {
    padding-left: 70px;
  }
  .primary h2,
  .secondary h2 {
    font-size: 5rem;
    line-height: 6rem;
  }

  .primary .item {
    padding-left: 70px;
    min-height: 650px;
  }

  .primary i {
    position: absolute;
    right: 0;
    top: 15px;
  }

  .secondary .item {
    padding-left: 70px;
    min-height: 800px;
  }

  .secondary i {
    position: absolute;
    right: 0;
    top: 180px;
    margin: 0;
  }
}

@media screen and (min-width: 768px) {
  .primary h2,
  .secondary h2 {
    font-size: 5rem;
    line-height: 6rem;
  }

  .primary .details,
  .secondary .details {
    font-size: 1.875rem;
    line-height: 2.813rem;
  }
}

@media screen and (min-width: 915px) {
  .tertiary {
    width: 50%;
  }

  .tertiary .item {
    max-width: 640px;
    height: 100%;
    margin: 0 0 0 auto;
  }
}
</style>
