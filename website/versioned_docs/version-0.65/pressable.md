---
id: pressable
title: Pressable
---

Pressable é um wrapper de Core Component que pode detectar vários estágios de interações de impressão em qualquer um de seus filhos definidos.

`` `jsx
<Pressable onPress = {onPressFunction}>
  <Text> Sou pressionável! </Text>
</Pressable>
`` `

## Como funciona

Em um elemento envolvido por `Pressable`:

- [`onPressIn`] (# onpressin) é chamado quando um pressionamento é ativado.
- [`onPressOut`] (# onpressout) é chamado quando o gesto de pressionar é desativado.

Depois de pressionar [`onPressIn`] (# onpressin), uma de duas coisas acontecerá:

1. A pessoa removerá o dedo, acionando [`onPressOut`] (# onpressout) seguido por [` onPress`] (# onpress).
2. Se a pessoa deixar o dedo por mais de 500 milissegundos antes de removê-lo, [`onLongPress`] (# onlongpress) será acionado. ([`onPressOut`] (# onpressout) ainda irá disparar quando eles removerem o dedo.)

<img src = "/ docs / assets / d_pressable_pressing.svg" width = "1000" alt = "Diagrama dos eventos onPress em sequência." />

Os dedos não são os instrumentos mais precisos e é comum os usuários ativar acidentalmente o elemento errado ou perder a área de ativação. Para ajudar, `Pressable` tem um` HitRect` opcional que você pode usar para definir o quão longe um toque pode ser registrado longe do elemento empacotado. As impressoras podem começar em qualquer lugar dentro de um `HitRect`.

`PressRect` permite que os pressionamentos se movam além do elemento e seu` HitRect`, mantendo a ativação e sendo elegível para um "pressionamento" - pense em deslizar o dedo lentamente para longe de um botão que está pressionando.

> A área de toque nunca ultrapassa os limites da visualização pai e o Z-index das visualizações irmãs sempre tem precedência se um toque atingir duas visualizações sobrepostas.

<figura>
  <img src = "/ docs / assets / d_pressable_anatomy.svg" width = "1000" alt = "Diagrama de HitRect e PressRect e como eles funcionam." />
  <figcaption>
    Você pode definir <code> HitRect </code> com <code> hitSlop </code> e definir <code> PressRect </code> com <code> pressRetentionOffset </code>.
  </figcaption>
</figure>

> `Pressable` usa a API` Pressability` do React Native. Para obter mais informações sobre o fluxo da máquina de estado de Pressability e como ele funciona, verifique a implementação de [Pressability] (https://github.com/facebook/react-native/blob/16ea9ba8133a5340ed6751ec7d49bf03a0d4c5ea/Libraries/Pressability/Pressability.js# L347).

## Exemplo

`` `SnackPlayer name = Pressable
import React, {useState} de 'react';
import {Pressable, StyleSheet, Text, View} de 'react-native';

const App = () => {
  const [timesPressed, setTimesPressed] = useState (0);

  let textLog = '';
  if (timesPressed> 1) {
    textLog = timesPressed + 'x onPress';
  } else if (timesPressed> 0) {
    textLog = 'onPress';
  }

  Retorna (
    <Exibir estilo = {styles.container}>
      <Pressionável
        onPress = {() => {
          setTimesPressed ((atual) => atual + 1);
        }}
        estilo = {({pressionado}) => [
          {
            backgroundColor: pressionado
              ? 'rgb (210, 230, 255)'
              : 'Branco'
          },
          styles.wrapperCustom
        ]}>
        {({pressionado}) => (
          <Estilo do texto = {styles.text}>
            {pressionado? 'Pressionado!' : 'Pressione-me'}
          </Text>
        )}
      </Pressable>
      <Exibir estilo = {styles.logBox}>
        <Text testID = "pressable_press_console"> {textLog} </Text>
      </View>
    </View>
  );
};

estilos const = StyleSheet.create ({
  container: {
    flex: 1,
    justifyContent: "center",
  },
  texto: {
    fontSize: 16
  },
  wrapperCustom: {
    borderRadius: 8,
    preenchimento: 6
  },
  logBox: {
    preenchimento: 20,
    margem: 10,
    borderWidth: StyleSheet.hairlineWidth,
    borderColor: '# f0f0f0',
    backgroundColor: '# f9f9f9'
  }
});

exportar aplicativo padrão;
`` `

## Props

### `android_disableSound` <div class =" label android "> Android </div>

Se verdadeiro, não reproduz o som do sistema Android ao pressionar.

| Tipo | Padrão |
| ------- | ------- |
| booleano | `false` |

### `android_ripple` <div class =" label android "> Android </div>

Ativa o efeito cascata do Android e configura suas propriedades.

| Tipo |
| -------------------------------------- |
| [RippleConfig] (pressionável # rippleconfig) |

### `crianças`

Filhos ou uma função que recebe um booleano refletindo se o componente está pressionado no momento.

| Tipo |
| ------------------------ |
| [Nó de reação] (nó de reação) |

### `unstable_pressDelay`

Duração (em milissegundos) para esperar após pressionar para baixo antes de chamar `onPressIn`.

| Tipo |
| ------ |
| número |

### `delayLongPress`

Duração (em milissegundos) de `onPressIn` antes de` onLongPress` ser chamado.

| Tipo | Padrão |
| ------ | ------- |
| número | `500` |

### `disabled`

Se o comportamento da imprensa está desativado.

| Tipo | Padrão |
| ------- | ------- |
| booleano | `false` |

### `hitSlop`

Define a distância adicional fora do elemento em que uma pressão pode ser detectada.

| Tipo |
| ---------------------- |
| [Rect] (rect) ou número |

### `onLongPress`

Chamado se o tempo após `onPressIn` durar mais de 500 milissegundos. Este período de tempo pode ser personalizado com [`delayLongPress`] (# delaylongpress).

| Tipo |
| -------------------------------------------------- - |
| ({nativeEvent: [PressEvent] (pressevent)}) => void |

### `onPress`

Chamado após `onPressOut`.

| Tipo |
| -------------------------------------------------- - |
| ({nativeEvent: [PressEvent] (pressevent)}) => void |

### `onPressIn`

Chamado imediatamente quando um toque é ativado, antes de `onPressOut` e` onPress`.

| Tipo |
| -------------------------------------------------- - |
| ({nativeEvent: [PressEvent] (pressevent)}) => void |

### `onPressOut`

Chamado quando um toque é liberado.

| Tipo |
| -------------------------------------------------- - |
| ({nativeEvent: [PressEvent] (pressevent)}) => void |

### `pressRetentionOffset`

Distância adicional fora desta vista na qual um toque é considerado uma pressão antes de `onPressOut` ser disparado.

| Tipo | Padrão |
| ---------------------- | ---------------------------------------------- |
| [Rect] (rect) ou número | `{inferior: 30, esquerda: 20, direita: 20, superior: 20}` |

### `style`

Estilos de visualização ou uma função que recebe um booleano refletindo se o componente está pressionado no momento e retorna estilos de visualização.

| Tipo |
| ------------------------------ |
| [Estilo de visualização] (adereços de estilo de visualização) |

### `testOnly_pressed`

Usado apenas para documentação ou teste (por exemplo, teste de instantâneo).

| Tipo | Padrão |
| ------- | ------- |
| booleano | `false` |

## Definições de tipo

### RippleConfig

Configuração do efeito ondulação para a propriedade `android_ripple`.

| Tipo |
| ------ |
| objeto |

**Propriedades:**


| Name       | Type            | Required | Description                                         |
| ---------- | --------------- | -------- | --------------------------------------------------- |
| color      | [color](colors) | No       | Defines the color of the ripple effect.             |
| borderless | boolean         | No       | Defines if ripple effect should not include border. |
| radius     | number          | No       | Defines the radius of the ripple effect.            |