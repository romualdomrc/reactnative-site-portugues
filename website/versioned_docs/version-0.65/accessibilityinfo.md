---
id: accessibilityinfo
title: AccessibilityInfo
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

Às vezes, é útil saber se o dispositivo tem ou não um leitor de tela ativo no momento. A API `AccessibilityInfo` foi projetada para esse propósito. Você pode usá-lo para consultar o estado atual do leitor de tela, bem como para se registrar para ser notificado quando o estado do leitor de tela mudar.

## Exemplo

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=AccessibilityInfo%20Function%20Component%20Example&supportedPlatforms=android,ios
import React, { useState, useEffect } from "react";
import { AccessibilityInfo, View, Text, StyleSheet } from "react-native";

const App = () => {
  const [reduceMotionEnabled, setReduceMotionEnabled] = useState(false);
  const [screenReaderEnabled, setScreenReaderEnabled] = useState(false);

  useEffect(() => {
    const reduceMotionChangedSubscription = AccessibilityInfo.addEventListener(
      "reduceMotionChanged",
      reduceMotionEnabled => {
        setReduceMotionEnabled(reduceMotionEnabled);
      }
    );
    const screenReaderChangedSubscription = AccessibilityInfo.addEventListener(
      "screenReaderChanged",
      screenReaderEnabled => {
        setScreenReaderEnabled(screenReaderEnabled);
      }
    );

    AccessibilityInfo.isReduceMotionEnabled().then(
      reduceMotionEnabled => {
        setReduceMotionEnabled(reduceMotionEnabled);
      }
    );
    AccessibilityInfo.isScreenReaderEnabled().then(
      screenReaderEnabled => {
        setScreenReaderEnabled(screenReaderEnabled);
      }
    );

    return () => {
      reduceMotionChangedSubscription.remove();
      screenReaderChangedSubscription.remove();
    };
  }, []);

  return (
    <View style={styles.container}>
      <Text style={styles.status}>
        The reduce motion is {reduceMotionEnabled ? "enabled" : "disabled"}.
      </Text>
      <Text style={styles.status}>
        The screen reader is {screenReaderEnabled ? "enabled" : "disabled"}.
      </Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  },
  status: {
    margin: 30
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=AccessibilityInfo%20Class%20Component%20Example&supportedPlatforms=android,ios
import React, { Component } from 'react';
import { AccessibilityInfo, View, Text, StyleSheet } from 'react-native';

class AccessibilityStatusExample extends Component {
  state = {
    reduceMotionEnabled: false,
    screenReaderEnabled: false,
  };

  componentDidMount() {
    this.reduceMotionChangedSubscription = AccessibilityInfo.addEventListener(
      'reduceMotionChanged',
      reduceMotionEnabled => {
        this.setState({ reduceMotionEnabled });
      }
    );
    this.screenReaderChangedSubscription = AccessibilityInfo.addEventListener(
      'screenReaderChanged',
      screenReaderEnabled => {
        this.setState({ screenReaderEnabled });
      }
    );

    AccessibilityInfo.isReduceMotionEnabled().then(reduceMotionEnabled => {
      this.setState({ reduceMotionEnabled });
    });
    AccessibilityInfo.isScreenReaderEnabled().then(screenReaderEnabled => {
      this.setState({ screenReaderEnabled });
    });
  }

  componentWillUnmount() {
    this.reduceMotionChangedSubscription.remove();
    this.screenReaderChangedSubscription.remove();
  }

  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.status}>
          The reduce motion is{' '}
          {this.state.reduceMotionEnabled ? 'enabled' : 'disabled'}.
        </Text>
        <Text style={styles.status}>
          The screen reader is{' '}
          {this.state.screenReaderEnabled ? 'enabled' : 'disabled'}.
        </Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  status: {
    margin: 30,
  },
});

export default AccessibilityStatusExample;
```

</TabItem>
</Tabs>

---

# Referência

## Métodos

### `addEventListener()`

```jsx
static addEventListener(eventName, handler)
```

Adicione um manipulador de eventos. Eventos com suporte:

| Nome do evento                                                             | Descrição                                                                                                                                                                                                                                                                                                                        |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `announcementFinished`<br/><div class="label two-lines ios">iOS</div>      | É acionado quando o leitor de tela termina de fazer um anúncio. O argumento para o manipulador de eventos é um dicionário com estas chaves: <ul> <li> `announcement`: A string anunciada pelo leitor de tela. </li> <li> `success`: Um booleano indicando se o anúncio foi bem-sucedido feito. </li> </ul>                       |
| `boldTextChanged`<br/><div class="label two-lines ios">iOS</div>           | É acionado quando o estado do texto em negrito muda. O argumento para o manipulador de eventos é um booleano. O booleano é `verdadeiro` quando o texto em negrito está ativado e `falso` caso contrário.                                                                                                                         |
| `grayscaleChanged`<br/><div class="label two-lines ios">iOS</div>          | É acionado quando o estado da alternância de escala de cinza muda. O argumento para o manipulador de eventos é um booleano. O booleano é `verdadeiro` quando uma escala de cinza é ativada e `false` caso contrário.                                                                                                             |
| `invertColorsChanged`<br/><div class="label two-lines ios">iOS</div>       | É acionado quando o estado da alternância de cores invertidas muda. O argumento para o manipulador de eventos é um booleano. O booleano é `verdadeiro` quando as cores invertidas estão habilitadas e `false` caso contrário.                                                                                                    |
| `reduceMotionChanged`                                                      | É acionado quando o estado da alternância de redução de movimento muda. O argumento para o manipulador de eventos é um booleano. O booleano é `verdadeiro` quando um movimento de redução é ativado (ou quando “Escala de Animação de Transição” em “Opções do Desenvolvedor” é “Animação desativada”) e `false` caso contrário. |
| `reduceTransparencyChanged`<br/><div class="label two-lines ios">iOS</div> | É acionado quando o estado da alternância de redução de transparência muda. O argumento para o manipulador de eventos é um booleano. O booleano é `verdadeiro` quando a transparência reduzida está ativada e `false` caso contrário.                                                                                            |
| `screenReaderChanged`                                                      | É acionado quando o estado do leitor de tela muda. O argumento para o manipulador de eventos é um booleano. O booleano é `verdadeiro` quando um leitor de tela está ativado e `falso` caso contrário.                                                                                                                            |

---

### `announceForAccessibility()`

```jsx
static announceForAccessibility(announcement)
```

Publique uma string a ser anunciada pelo leitor de tela.

---

### `getRecommendedTimeoutMillis()` <div class="label android">Android</div>

```jsx
static getRecommendedTimeoutMillis(originalTimeout)
```

Obtém o tempo limite em milissegundos que o usuário precisa.
Esse valor é definido em “Tempo para agir (tempo limite de acessibilidade)” das configurações de “Acessibilidade”.

**Parâmetros: **

| Nome                                                             | Tipo   | Descrição                                                                                                              |
| ---------------------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------------------------------- |
| originalTimeout <div class="label basic required">Required</div> | number | O tempo limite para retornar se o “Tempo limite de acessibilidade” não estiver definido. Especifique em milissegundos. |

---

### `isBoldTextEnabled()` <div class="label ios">iOS</div>

```jsx
static isBoldTextEnabled()
```

Consulte se um texto em negrito está habilitado no momento. Retorna uma promessa que resolve para um booleano. O resultado é `verdadeiro` quando o texto em negrito está ativado e `falso` caso contrário.

---

### `isGrayscaleEnabled()` <div class="label ios">iOS</div>

```jsx
static isGrayscaleEnabled()
```

Consulte se a escala de cinza está habilitada no momento. Retorna uma promessa que resolve para um booleano. O resultado é `verdadeiro` quando a escala de cinza está ativada e `false` caso contrário.

---

### `isInvertColorsEnabled()` <div class="label ios">iOS</div>

```jsx
static isInvertColorsEnabled()
```

Consulte se a opção Inverter cores está habilitada no momento. Retorna uma promessa que resolve para um booleano. O resultado é `verdadeiro` quando as cores invertidas estão habilitadas e `false` caso contrário.

---

### `isReduceMotionEnabled()`

```jsx
static isReduceMotionEnabled()
```

Consulte se a opção Reduzir movimento está habilitada no momento. Retorna uma promessa que resolve para um booleano. O resultado é `verdadeiro` quando o movimento de redução está ativado e `falso` caso contrário.

---

### `isReduceTransparencyEnabled()` <div class="label ios">iOS</div>

```jsx
static isReduceTransparencyEnabled()
```

Consulte se a opção Reduzir transparência está habilitada no momento. Retorna uma promessa que resolve para um booleano. O resultado é `verdadeiro` quando uma transparência reduzida é ativada e `false` caso contrário.

---

### `isScreenReaderEnabled()`

```jsx
static isScreenReaderEnabled()
```

Consulte se um leitor de tela está habilitado no momento. Retorna uma promessa que resolve para um booleano. O resultado é `verdadeiro` quando um leitor de tela está ativado e `falso` caso contrário.

---

### `removeEventListener()`

```jsx
static removeEventListener(eventName, handler)
```

> **Descontinuado.** Use o método `remove () `na assinatura de evento retornada por [`addEventListener ()`] (#addeventlistener).

---

### `setAccessibilityFocus()`

```jsx
static setAccessibilityFocus(reactTag)
```

Defina o foco de acessibilidade para um componente React.

No Android, isso chama o método `UIManager.sendAccessibilityEvent` com os argumentos `ReactTag` e `UIManager.ACCESSIBILITYEventTypes.typeViewFocused` passados.

> **Nota**: Certifique-se de que qualquer `View` que você deseja receber o foco de acessibilidade tenha `accessible= {true} `.
