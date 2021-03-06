---
id: statusbar
title: StatusBar
---

Componente para controlar a barra de status do aplicativo.

### Usage with Navigator

É possível ter vários StatusBarcomponentes montados ao mesmo tempo. Os adereços serão mesclados na ordem em que os StatusBarcomponentes foram montados.

```SnackPlayer Nome=StatusBar%20Component%20Example&supportedPlatforms=android,ios
import React, { useState } from 'react';
import { Button, Platform, SafeAreaView, StatusBar, StyleSheet, Text, View } from 'react-native';

const STYLES = ['default', 'dark-content', 'light-content'];
const TRANSITIONS = ['fade', 'slide', 'none'];

const App = () => {
  const [hidden, setHidden] = useState(false);
  const [statusBarStyle, setStatusBarStyle] = useState(STYLES[0]);
  const [statusBarTransition, setStatusBarTransition] = useState(TRANSITIONS[0]);

  const changeStatusBarVisibility = () => setHidden(!hidden);

  const changeStatusBarStyle = () => {
    const styleId = STYLES.indexOf(statusBarStyle) + 1;
    if (styleId === STYLES.length) {
      setStatusBarStyle(STYLES[0]);
    } else {
      setStatusBarStyle(STYLES[styleId]);
    }
  };

  const changeStatusBarTransition = () => {
    const transition = TRANSITIONS.indexOf(statusBarTransition) + 1;
    if (transition === TRANSITIONS.length) {
      setStatusBarTransition(TRANSITIONS[0]);
    } else {
      setStatusBarTransition(TRANSITIONS[transition]);
    }
  };

  return (
    <SafeAreaView style={styles.container}>
      <StatusBar
        animated={true}
        backgroundColor="#61dafb"
        barStyle={statusBarStyle}
        showHideTransition={statusBarTransition}
        hidden={hidden} />
      <Text style={styles.textStyle}>
        StatusBar Visibility:{'\n'}
        {hidden ? 'Hidden' : 'Visible'}
      </Text>
      <Text style={styles.textStyle}>
        StatusBar Style:{'\n'}
        {statusBarStyle}
      </Text>
      {Platform.OS === 'ios' ? (
        <Text style={styles.textStyle}>
          StatusBar Transition:{'\n'}
          {statusBarTransition}
        </Text>
      ) : null}
      <View style={styles.buttonsContainer}>
        <Button
          title="Toggle StatusBar"
          onPress={changeStatusBarVisibility} />
        <Button
          title="Change StatusBar Style"
          onPress={changeStatusBarStyle} />
        {Platform.OS === 'ios' ? (
          <Button
            title="Change StatusBar Transition"
            onPress={changeStatusBarTransition} />
        ) : null}
      </View>
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    backgroundColor: '#ECF0F1'
  },
  buttonsContainer: {
    padding: 10
  },
  textStyle: {
    textAlign: 'center',
    marginBottom: 8
  }
});

export default App;
```

### Imperative API

Para os casos em que o uso de um componente não é ideal, também há uma API obrigatória exposta como funções estáticas no componente. No entanto, não é recomendado usar a API estática e o componente para o mesmo prop porque qualquer valor definido pela API estática será substituído por aquele definido pelo componente na próxima renderização.
---

# Referência

## Constantes 

### `currentHeight` <div class="label android">Android</div>

A altura da barra de status, que inclui a altura do entalhe, se houver.

---

## Props

### `animated`

Se a transição entre as alterações de propriedade da barra de status deve ser animada. Suportado por backgroundColor, barStylee hiddenpropriedades.

| Tipo    | Required | Default |
| ------- | -------- | ------- |
| boolean | No       | `false` |

---

### `backgroundColor` <div class="label android">Android</div>

A cor de fundo da barra de status.

| Tipo            | Required | Default                                                                |
| --------------- | -------- | ---------------------------------------------------------------------- |
| [color](colors) | No       | default system StatusBar background color, or `'black'` if not defined |

---

### `barStyle`

Define a cor do texto da barra de status.

No Android, isso só terá impacto nas versões 23 e superiores da API

| Tipo                                       | Required | Default     |
| ------------------------------------------ | -------- | ----------- |
| [StatusBarStyle](statusbar#statusbarstyle) | No       | `'default'` |

---

### `hidden`

Se a barra de status estiver oculta.

| Tipo    | Required | Default |
| ------- | -------- | ------- |
| boolean | No       | `false` |

---

### `networkActivityIndicatorVisible` <div class="label ios">iOS</div>

Se o indicador de atividade da rede deve estar visível.

| Tipo    | Default |
| ------- | ------- |
| boolean | `false` |

---

### `showHideTransition` <div class="label ios">iOS</div>

O efeito de transição ao mostrar e ocultar a barra de status usando o hiddensuporte.

| Tipo                                               | Default  |
| -------------------------------------------------- | -------- |
| [StatusBarAnimation](statusbar#statusbaranimation) | `'fade'` |

---

### `translucent` <div class="label android">Android</div>

Se a barra de status for translúcida. Quando translúcido estiver definido como true, o aplicativo será desenhado sob a barra de status. Isso é útil ao usar uma cor de barra de status semitransparente.

| Tipo    | Default |
| ------- | ------- |
| boolean | `false` |

## Methods

### `popStackEntry()`

```jsx
static popStackEntry(entry: any)
```

Obtenha e remova a última entrada StatusBar da pilha.

**Parâmetros:**

| Nome                                                   | Tipo | Descrição                           |
| ------------------------------------------------------ | ---- | ------------------------------------- |
| entry <div class="label basic required">Required</div> | any  | Entry returned from `pushStackEntry`. |

---

### `pushStackEntry()`

```jsx
static pushStackEntry(props: any)
```

Empurre uma entrada StatusBar para a pilha. O valor de retorno deve ser passado para popStackEntry quando concluído.

**Parâmetros:**

| Nome                                                   | Tipo | Descrição                                                      |
| ------------------------------------------------------ | ---- | ---------------------------------------------------------------- |
| props <div class="label basic required">Required</div> | any  | Object containing the StatusBar props to use in the stack entry. |

---

### `replaceStackEntry()`

```jsx
static replaceStackEntry(entry: any, props: any)
```

Substitua uma entrada de pilha StatusBar existente por novos adereços.

**Parâmetros:**

| Nome                                                   | Tipo | Descrição                                                                  |
| ------------------------------------------------------ | ---- | ---------------------------------------------------------------------------- |
| entry <div class="label basic required">Required</div> | any  | Entry returned from `pushStackEntry` to replace.                             |
| props <div class="label basic required">Required</div> | any  | Object containing the StatusBar props to use in the replacement stack entry. |

---

### `setBackgroundColor()` <div class="label android">Android</div>

```jsx
static setBackgroundColor(color: string, [animated]: boolean)
```

Defina a cor de fundo da barra de status.

**Parâmetros:**

| Nome                                                   | Tipo    | Descrição               |
| ------------------------------------------------------ | ------- | ------------------------- |
| color <div class="label basic required">Required</div> | string  | Background color.         |
| animated                                               | boolean | Animate the style change. |

---

### `setBarStyle()`

```jsx
static setBarStyle(style: StatusBarStyle, [animated]: boolean)
```

Defina o estilo da barra de status.

**Parâmetros:**

| Nome                                                   | Tipo                                       | Descrição               |
| ------------------------------------------------------ | ------------------------------------------ | ------------------------- |
| style <div class="label basic required">Required</div> | [StatusBarStyle](statusbar#statusbarstyle) | Status bar style to set.  |
| animated                                               | boolean                                    | Animate the style change. |

---

### `setHidden()`

```jsx
static setHidden(hidden: boolean, [animation]: StatusBarAnimation)
```

Mostra ou esconde a barra de status.

**Parâmetros:**

| Nome                                                    | Tipo                                               | Descrição                                             |
| ------------------------------------------------------- | -------------------------------------------------- | ------------------------------------------------------- |
| hidden <div class="label basic required">Required</div> | boolean                                            | Hide the status bar.                                    |
| animation <div class="label ios">iOS</div>              | [StatusBarAnimation](statusbar#statusbaranimation) | Animation when changing the status bar hidden property. |

---

### `setNetworkActivityIndicatorVisible()` <div class="label ios">iOS</div>

```jsx
static setNetworkActivityIndicatorVisible(visible: boolean)
```

Controle a visibilidade do indicador de atividade da rede.

**Parâmetros:**

| Nome                                                     | Tipo    | Descrição         |
| -------------------------------------------------------- | ------- | ------------------- |
| visible <div class="label basic required">Required</div> | boolean | Show the indicator. |

---

### `setTranslucent()` <div class="label android">Android</div>

```jsx
static setTranslucent(translucent: boolean)
```

Controle a translucidez da barra de status.

**Parâmetros:**

| Nome                                                         | Tipo    | Descrição         |
| ------------------------------------------------------------ | ------- | ------------------- |
| translucent <div class="label basic required">Required</div> | boolean | Set as translucent. |

## Tipo Definitions

### StatusBarAnimation

Tipo de animação da barra de status para transições no iOS.

| Tipo |
| ---- |
| enum |

**Constants:**

| Value     | Tipo   | Descrição     |
| --------- | ------ | --------------- |
| `'fade'`  | string | Fade animation  |
| `'slide'` | string | Slide animation |
| `'none'`  | string | No animation    |

---

### StatusBarStyle

Tipo de estilo da barra de status.

| Tipo |
| ---- |
| enum |

**Constantes::**

| Value             | Tipo   | Descrição                                                          |
| ----------------- | ------ | -------------------------------------------------------------------- |
| `'default'`       | string | Estilo de barra de status padrão (escuro para iOS, claro para Android)           |
| `'light-content'` | string | Fundo escuro, textos em branco e ícones                             |
| `'dark-content'`  | string | Plano de fundo claro, textos e ícones escuros (requer API> = 23 no Android) |
