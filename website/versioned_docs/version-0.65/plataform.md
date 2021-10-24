---
id: platform
title: Platform
---

## Example

```SnackPlayer name=Platform%20API%20Example&supportedPlatforms=ios,android
import React from 'react';
import { Platform, StyleSheet, Text, ScrollView } from 'react-native';

const App = () => {
  return (
    <ScrollView contentContainerStyle={styles.container}>
      <Text>OS</Text>
      <Text style={styles.value}>{Platform.OS}</Text>
      <Text>OS Version</Text>
      <Text style={styles.value}>{Platform.Version}</Text>
      <Text>isTV</Text>
      <Text style={styles.value}>{Platform.isTV.toString()}</Text>
      {Platform.OS === 'ios' && <>
        <Text>isPad</Text>
        <Text style={styles.value}>{Platform.isPad.toString()}</Text>
      </>}
      <Text>Constants</Text>
      <Text style={styles.value}>
        {JSON.stringify(Platform.constants, null, 2)}
      </Text>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  value: {
    fontWeight: '600',
    padding: 4,
    marginBottom: 8
  }
});

export default App;
```

---

# Reference

## Properties

### `constants`

```jsx
Platform.constants;
```

Retorna um objeto que contém todas as constantes comuns e específicas disponíveis relacionadas à plataforma.

**Propriedades: **

|  <div className="widerColumn"> Nome: </div>                    | Tipo    | Opcional | Descrição                                                                                                                                                                                       |
| --------------------------------------------------------- | ------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| isTesting                                                 | boolean | Não       |                                                                                                                                                                                                   |
| reactNativeVersion                                        | object  | Não       | Informações sobre a versão React Native. As chaves são `major`, `minor`, `patch` com `pré-lançamento` opcional e os valores são `número`s.                                                                   |
| Versão: <div className="label android"> Android </div>       | number  | Não       | Constante de versão do sistema operacional específica para Android.                                                                                                                                                          |
| Lançamento <div className="label android"> Android </div>       | string  | Não       |                                                                                                                                                                                                   |
| Serial <div className="label android">Android</div>       | string  | Não       | Número de série do hardware de um dispositivo Android.                                                                                                                                                      |
| Impressão digital <div className="label android"> Android </div>   | string  | Não       | Uma string que identifica exclusivamente a compilação.                                                                                                                                                      |
| Modelo <div className="label android"> Android </div>         | string  | Não       | O nome visível para o usuário final do dispositivo Android.                                                                                                                                                 |
| Marca: <div className="label android"> Android </div>         | string  | No       | A marca visível ao consumidor à qual o produto/hardware será associado.                                                                                                                    |
| Fabricante <div className="label android"> Android </div>  | string  | Não       | O fabricante do dispositivo Android.                                                                                                                                                           |
| ServerHost <div className="label android">Android</div>   | string  | sim      |                                                                                                                                                                                                   |
| uiMode <div className="label android">Android</div>       | string  | Não       | Os valores possíveis são: `'car'`, `'desk'`, `'normal'`, `'tv'`, `'watch'` e `'desconhecido' `. Leia mais sobre [Android ModeType] (https://developer.android.com/reference/android/app/UiModeManager.html). |
| forceTouchAvailable <div className="label ios">iOS</div>  | boolean | Não       | Indique a disponibilidade do 3D Touch em um dispositivo.                                                                                                                                                |
| interfaceIdiom <div className="label ios">iOS</div>       | string  | Não       | O tipo de interface do dispositivo. Leia mais sobre [UIUserInterfaceIdiom] (https://developer.apple.com/documentation/uikit/uiuserinterfaceidiom).                                                  |
| osVersion <div className="label ios">iOS</div>            | string  | Não       | Constante de versão do sistema operacional específica para iOS.                                                                                                                                                              |
| systemName <div className="label ios">iOS</div>           | string  | Não       | Constante de nome do sistema operacional específica para iOS.                                                                                                                                                                 |

---

### `isPad` <div class="label ios">iOS</div>

```jsx
Platform.isPad;
```

Retorna um booleano que define se o dispositivo é um iPad.

| Tipo    |
| ------- |
| boolean |

---

### `isTV`

```jsx
Platform.isTV;
```

Retorna um booleano que define se o dispositivo é uma TV.

| Tipo    |
| ------- |
| boolean |

---

### `isTesting`

```jsx
Platform.isTesting;
```

Retorna um booleano que define se o aplicativo está sendo executado no Modo Desenvolvedor com sinalizador de teste definido.

| Tipo    |
| ------- |
| boolean |

---

### `OS`

```jsx
static Platform.OS
```

Retorna o valor da string que representa o SO atual.

| Tipo                       |
| -------------------------- |
| enum(`'android'`, `'ios'`) |

---

### `Version`

```jsx
Platform.Version;
```

Retorna a versão do sistema operacional.

| Tipo                                                                                                 |
| ---------------------------------------------------------------------------------------------------- |
| number <div className="label android">Android</div><hr />string <div className="label ios">iOS</div> |

## Métodos

### `select()`

```jsx
static select(config: object): any
```

Retorna o valor mais adequado para a plataforma em que você está executando no momento.

#### Parâmetros:

| Nome   | Tipo   | Obrigatório | Descrição                   |
| ------ | ------ | -------- | ----------------------------- |
| config | object | sim      | Veja a descrição da configuração abaixo. |

O método Select retorna o valor mais adequado para a plataforma em que você está executando no momento. Ou seja, se você estiver executando em um telefone, as teclas `android` e `ios` terão preferência. Se esses não forem especificados, a chave `nativa` será usada e, em seguida, a chave `default`.

O parâmetro `config` é um objeto com as seguintes chaves:

- `android` (any)
- `ios` (any)
- `native` (any)
- `default` (any)

**Exemplo de uso: **

```jsx
import { Platform, StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    ...Platform.select({
      android: {
        backgroundColor: 'green'
      },
      ios: {
        backgroundColor: 'red'
      },
      default: {
        // other platforms, web for example
        backgroundColor: 'blue'
      }
    })
  }
});
```

Isso resultará em um contêiner com `flex: 1` em todas as plataformas, uma cor de fundo verde no Android, uma cor de fundo vermelha no iOS e uma cor de fundo azul em outras plataformas.

Como o valor da chave de plataforma correspondente pode ser do tipo `any`, o método [`select`] (platform.md #select) também pode ser usado para retornar componentes específicos da plataforma, como abaixo:

```jsx
const Component = Platform.select({
  ios: () => require('ComponentIOS'),
  android: () => require('ComponentAndroid')
})();

<Component />;
```

```jsx
const Component = Platform.select({
  native: () => require('ComponentForNative'),
  default: () => require('ComponentForWeb')
})();

<Component />;
```
