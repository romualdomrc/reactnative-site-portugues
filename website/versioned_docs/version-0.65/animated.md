---
id: animated
title: Animated
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

A biblioteca `Animated` foi projetada para tornar as animações fluidas, poderosas e indolores de construir e manter. `Animated` concentra-se em relações declarativas entre entradas e saídas, transformações configuráveis entre elas e métodos `start`/`stop` para controlar a execução de animação baseada em tempo.

O fluxo de trabalho principal para criar uma animação é criar um `Animated.Value`, conectá-lo a um ou mais atributos de estilo de um componente animado e, em seguida, gerar atualizações por meio de animações usando `Animated.Timing () `.

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

> Não modifique o valor animado diretamente. Você pode usar o [`UseRef` Hook] (https://reactjs.org/docs/hooks-reference.html#useref) para retornar um objeto ref mutável. A propriedade `current` deste objeto ref é inicializada como o argumento fornecido e persiste durante todo o ciclo de vida do componente.

</TabItem>
<TabItem value="classical">

> Não modifique o valor animado diretamente. Geralmente é armazenado como uma [variável de estado] (intro-react #state) em componentes de classe.

</TabItem>
</Tabs>

## Exemplo

O exemplo a seguir contém uma `View` que irá desaparecer e desaparecer com base no valor animado `FadeAnim`

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Animated
import React, { useRef } from "react";
import { Animated, Text, View, StyleSheet, Button, SafeAreaView } from "react-native";

const App = () => {
  // fadeAnim will be used as the value for opacity. Initial Value: 0
  const fadeAnim = useRef(new Animated.Value(0)).current;

  const fadeIn = () => {
    // Will change fadeAnim value to 1 in 5 seconds
    Animated.timing(fadeAnim, {
      toValue: 1,
      duration: 5000
    }).start();
  };

  const fadeOut = () => {
    // Will change fadeAnim value to 0 in 3 seconds
    Animated.timing(fadeAnim, {
      toValue: 0,
      duration: 3000
    }).start();
  };

  return (
    <SafeAreaView style={styles.container}>
      <Animated.View
        style={[
          styles.fadingContainer,
          {
            // Bind opacity to animated value
            opacity: fadeAnim
          }
        ]}
      >
        <Text style={styles.fadingText}>Fading View!</Text>
      </Animated.View>
      <View style={styles.buttonRow}>
        <Button title="Fade In View" onPress={fadeIn} />
        <Button title="Fade Out View" onPress={fadeOut} />
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  },
  fadingContainer: {
    padding: 20,
    backgroundColor: "powderblue"
  },
  fadingText: {
    fontSize: 28
  },
  buttonRow: {
    flexBasis: 100,
    justifyContent: "space-evenly",
    marginVertical: 16
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Animated
import React, { Component } from "react";
import { Animated, Text, View, StyleSheet, Button, SafeAreaView } from "react-native";

class App extends Component {
  // fadeAnim will be used as the value for opacity. Initial Value: 0
  state = {
    fadeAnim: new Animated.Value(0)
  };

  fadeIn = () => {
    // Will change fadeAnim value to 1 in 5 seconds
    Animated.timing(this.state.fadeAnim, {
      toValue: 1,
      duration: 5000
    }).start();
  };

  fadeOut = () => {
    // Will change fadeAnim value to 0 in 3 seconds
    Animated.timing(this.state.fadeAnim, {
      toValue: 0,
      duration: 3000
    }).start();
  };

  render() {
    return (
      <SafeAreaView style={styles.container}>
        <Animated.View
          style={[
            styles.fadingContainer,
            {
              // Bind opacity to animated value
              opacity: this.state.fadeAnim
            }
          ]}
        >
          <Text style={styles.fadingText}>Fading View!</Text>
        </Animated.View>
        <View style={styles.buttonRow}>
          <Button title="Fade In View" onPress={this.fadeIn} />
          <Button title="Fade Out View" onPress={this.fadeOut} />
        </View>
      </SafeAreaView>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  },
  fadingContainer: {
    padding: 20,
    backgroundColor: "powderblue"
  },
  fadingText: {
    fontSize: 28
  },
  buttonRow: {
    flexBasis: 100,
    justifyContent: "space-evenly",
    marginVertical: 16
  }
});

export default App;
```

</TabItem>
</Tabs>

Consulte o guia [Animações] (animações #animated -api) para ver exemplos adicionais de `Animated` em ação.

## Visão geral

Existem dois tipos de valores que você pode usar com `Animated`:

- [`Animated.Value () `] (animado #value) para valores únicos
- [`Animated.valueXY () `] (animado #valuexy) para vetores

`Animated.Value` pode se vincular a propriedades de estilo ou outros adereços e também pode ser interpolado. Um único `Animated.Value` pode gerar qualquer número de propriedades.

### Configurando animações

`Animated` fornece três tipos de tipos de animação. Cada tipo de animação fornece uma curva de animação específica que controla como seus valores são animados desde o valor inicial até o valor final:

- [`Animated.decay () `] (animado #decay) começa com uma velocidade inicial e diminui gradualmente até uma parada.
- [`Animated.spring () `] (animado #spring) fornece um modelo básico de física de primavera.
- [`Animated.timing () `] (animado #timing) anima um valor ao longo do tempo usando [funções de atenuação] (atenuação).

Na maioria dos casos, você usará `timing () `. Por padrão, ele usa uma curva EaseInOut simétrica que transmite a aceleração gradual de um objeto a toda velocidade e conclui desacelerando gradualmente até uma parada.

### Trabalhando com animações

As animações são iniciadas chamando `start () `em sua animação. `start () `recebe um retorno de chamada de conclusão que será chamado quando a animação for concluída. Se a animação terminar de ser executada normalmente, o retorno de chamada de conclusão será invocado com `{finished: true}`. Se a animação for feita porque `stop () `foi chamada antes de terminar (por exemplo, porque foi interrompida por um gesto ou outra animação), ela receberá` {finished: false} `.

```jsx
Animated.timing({}).start(({ finished }) => {
  /* completion callback */
});
```

### Usando o driver nativo

Usando o driver nativo, enviamos tudo sobre a animação para o nativo antes de iniciar a animação, permitindo que o código nativo execute a animação no encadeamento da interface do usuário sem ter que passar pela ponte em cada quadro. Depois que a animação for iniciada, o encadeamento JS poderá ser bloqueado sem afetar a animação.

Você pode usar o driver nativo especificando `useNativeDriver: true` em sua configuração de animação. Consulte o guia [Animações] (animações #using -the-native-driver) para saber mais.

### Componentes animáveis

Somente componentes animáveis podem ser animados. Esses componentes exclusivos fazem a mágica de vincular os valores animados às propriedades e fazem atualizações nativas direcionadas para evitar o custo do processo de renderização e reconciliação do React em cada quadro. Eles também lidam com a limpeza na desmontagem, para que fiquem seguros por padrão.

- [`CreateAnimatedComponent () `] (animado #createanimatedcomponent) pode ser usado para tornar um componente animável.

`Animated` exporta os seguintes componentes animáveis usando o wrapper acima:

- `Animated.Image`
- `Animated.ScrollView`
- `Animated.Text`
- `Animated.View`
- `Animated.FlatList`
- `Animated.SectionList`

### Compondo animações

As animações também podem ser combinadas de maneiras complexas usando funções de composição:

- [`Animated.delay () `] (animado #delay) inicia uma animação após um determinado atraso.
- [`Animated.parallel () `] (animado #parallel) inicia várias animações ao mesmo tempo.
- [`Animated.sequence () `] (animado #sequence) inicia as animações em ordem, esperando que cada uma seja concluída antes de iniciar a próxima.
- [`Animated.stagger () `] (animado #stagger) inicia animações em ordem e em paralelo, mas com atrasos sucessivos.

As animações também podem ser encadeadas definindo o `toValue` de uma animação para ser outra `Animated.Value`. Consulte [Rastreamento de valores dinâmicos] (animações #tracking -valores dinâmicos) no guia Animações.

Por padrão, se uma animação for interrompida ou interrompida, todas as outras animações do grupo também serão interrompidas.

### Combinando valores animados

Você pode combinar dois valores animados por meio de adição, subtração, multiplicação, divisão ou módulo para criar um novo valor animado:

- [`Animated.add()`](animated#add)
- [`Animated.subtract()`](animated#subtract)
- [`Animated.divide()`](animated#divide)
- [`Animated.modulo()`](animated#modulo)
- [`Animated.multiply()`](animated#multiply)

### Interpolation

A função `interpolar () `permite que os intervalos de entrada sejam mapeados para diferentes intervalos de saída. Por padrão, ele extrapolará a curva além dos intervalos fornecidos, mas você também pode fazer com que ele fixe o valor de saída. Ele usa interpolação linear por padrão, mas também suporta funções de atenuação.

- [`interpolate()`](animated#interpolate)

Leia mais sobre interpolação no guia [Animação] (animações #interpolation).

### Lidar com gestos e outros eventos

Gestos, como panorâmica ou rolagem, e outros eventos podem mapear diretamente para valores animados usando `Animated.event () `. Isso é feito com uma sintaxe de mapa estruturado para que os valores possam ser extraídos de objetos de eventos complexos. O primeiro nível é uma matriz para permitir o mapeamento em vários argumentos, e essa matriz contém objetos aninhados.

- [`Animated.event()`](animated#event)

Por exemplo, ao trabalhar com gestos de rolagem horizontal, você faria o seguinte para mapear `event.nativeEvent.contentOffset.x` para `scrollX` (um `Animated.Value`):

```jsx
 onScroll={Animated.event(
   // scrollX = e.nativeEvent.contentOffset.x
   [{ nativeEvent: {
        contentOffset: {
          x: scrollX
        }
      }
    }]
 )}
```

---

# Referência

## Métodos

Quando o valor fornecido é um valorXy em vez de um Valor, cada opção de configuração pode ser um vetor da forma `{x:..., y:...}` em vez de um escalar.

### `decay()`

```jsx
static decay(value, config)
```

Anima um valor de uma velocidade inicial a zero com base em um coeficiente de decaimento.

Config é um objeto que pode ter as seguintes opções:

- `velocity`: Initial velocity. Required.
- `desaceleração`: Taxa de decaimento. Padrão 0,997.
- `IsInteraction`: Se esta animação cria ou não um “identificador de interação” no `InteractionManager`. Padrão verdadeiro.
- `useNativeDriver`: Usa o driver nativo quando verdadeiro. Padrão falso.

---

### `timing()`

```jsx
static timing(value, config)
```

Anima um valor ao longo de uma curva de atenuação cronometrada. O módulo [`Easing`] (atenuação) tem toneladas de curvas predefinidas, ou você pode usar sua própria função.

Config é um objeto que pode ter as seguintes opções:

- `duração`: Duração da animação (milissegundos). Padrão 500.
- `easing`: Função de atenuação para definir a curva. O padrão é `Easing.inOut (Easing.ease) `.
- `delay`: Inicie a animação após o atraso (milissegundos). Padrão 0.
- `IsInteraction`: Se esta animação cria ou não um “identificador de interação” no `InteractionManager`. Padrão verdadeiro.
- `useNativeDriver`: Usa o driver nativo quando verdadeiro. Padrão falso.

---

### `spring()`

```jsx
static spring(value, config)
```

Anima um valor de acordo com um modelo analítico de mola baseado em [oscilação harmônica amortecida] (https://en.wikipedia.org/wiki/Harmonic_oscillator#Damped_harmonic_oscillator). Rastreia o estado da velocidade para criar movimentos fluidos à medida que o `ToValue` é atualizado e pode ser encadeado.

Config é um objeto que pode ter as seguintes opções.

Observe que você só pode definir um de saltite/velocidade, tensão/atrito ou rigidez/amortecimento/massa, mas não mais do que um:

As opções de fricção/tensão ou saltite/velocidade correspondem ao modelo de mola em [`Facebook Pop`] (https://github.com/facebook/pop), [Rebound] (https://github.com/facebookarchive/rebound) e [Origami] (http://origami.design/).

- `fricção`: Controla “bounciness” /overshoot. Padrão 7.
- `tensão`: Controla a velocidade. Padrão 40.
- `velocidade`: Controla a velocidade da animação. Padrão 12.
- `bounciness`: Controla o bounciness. Padrão 8.

Especificar rigidez/amortecimento/massa como parâmetros faz com que `Animated.spring` use um modelo analítico de mola baseado nas equações de movimento de um [oscilador harmônico amortecido] (https://en.wikipedia.org/wiki/Harmonic_oscillator#Damped_harmonic_oscillator). Esse comportamento é um pouco mais preciso e fiel à física por trás da dinâmica da primavera, e imita de perto a implementação no CasSpringAnimation do iOS.

- `rigidez`: O coeficiente de rigidez da mola. Padrão 100.
- `amortecimento`: Define como o movimento da mola deve ser amortecido devido às forças de atrito. Padrão 10.
- `mass`: A massa do objeto anexado ao final da mola. Padrão 1.

Outras opções de configuração são as seguintes:

- `velocidade`: A velocidade inicial do objeto anexado à mola. Padrão 0 (o objeto está em repouso).
- `OvershootClamping`: Booleano indicando se a mola deve ser presa e não saltar. Padrão falso.
- `RestDisplacementThreshold`: O limiar de deslocamento do repouso abaixo do qual a mola deve ser considerada em repouso. Padrão 0.001.
- `RestSpeedThreshold`: A velocidade na qual a mola deve ser considerada em repouso em pixels por segundo. Padrão 0.001.
- `delay`: Inicie a animação após o atraso (milissegundos). Padrão 0.
- `IsInteraction`: Se esta animação cria ou não um “identificador de interação” no `InteractionManager`. Padrão verdadeiro.
- `useNativeDriver`: Usa o driver nativo quando verdadeiro. Padrão falso.

---

### `add()`

```jsx
static add(a, b)
```

Cria um novo valor Animado composto de dois valores Animados somados.

---

### `subtract()`

```jsx
static subtract(a, b)
```

Cria um novo valor Animado composto subtraindo o segundo valor Animado do primeiro valor Animado.

---

### `divide()`

```jsx
static divide(a, b)
```

Cria um novo valor Animado composto dividindo o primeiro valor Animado pelo segundo valor Animado.

---

### `multiply()`

```jsx
static multiply(a, b)
```

Cria um novo valor Animado composto de dois valores Animados multiplicados juntos.

---

### `modulo()`

```jsx
static modulo(a, modulus)
```

Cria um novo valor Animado que é o módulo (não negativo) do valor Animado fornecido

---

### `diffClamp()`

```jsx
static diffClamp(a, min, max)
```

Crie um novo valor Animado limitado entre 2 valores. Ele usa a diferença entre o último valor, portanto, mesmo que o valor esteja longe dos limites, ele começará a mudar quando o valor começar a se aproximar novamente. (`value = clamp (valor + diff, min, max) `).

Isso é útil com eventos de rolagem, por exemplo, para mostrar a barra de navegação ao rolar para cima e ocultá-la ao rolar para baixo.

---

### `delay()`

```jsx
static delay(time)
```

Inicia uma animação após o atraso determinado.

---

### `sequence()`

```jsx
static sequence(animations)
```

Inicia uma série de animações em ordem, esperando que cada uma seja concluída antes de começar a próxima. Se a animação em execução atual for interrompida, nenhuma animação a seguir será iniciada.

---

### `parallel()`

```jsx
static parallel(animations, config?)
```

Inicia uma série de animações ao mesmo tempo. Por padrão, se uma das animações for interrompida, todas elas serão interrompidas. Você pode substituir isso com o sinalizador `StopTogether`.

---

### `stagger()`

```jsx
static stagger(time, animations)
```

A matriz de animações pode ser executada em paralelo (sobreposição), mas são iniciadas em sequência com atrasos sucessivos. Bom para fazer efeitos finais.

---

### `loop()`

```jsx
static loop(animation, config?)
```

Realça uma determinada animação continuamente, de modo que cada vez que ela chega ao fim, ela é reiniciada e reinicie desde o início. Irá repetir sem bloquear o encadeamento JS se a animação filho estiver definida como `useNativeDriver: true`. Além disso, os loops podem impedir que componentes baseados em `VirtualizedList`renderizem mais linhas enquanto a animação está em execução. Você pode passar `isInteraction: false` na configuração de animação filho para corrigir isso.

Config é um objeto que pode ter as seguintes opções:

- `iterations`: Número de vezes que a animação deve repetir. Padrão `-1` (infinito).

---

### `event()`

```jsx
static event(argMapping, config?)
```

Pega uma matriz de mapeamentos e extrai valores de cada arg de acordo, em seguida, chama `setValue` nas saídas mapeadas. por exemplo

```jsx
 onScroll={Animated.event(
   [{nativeEvent: {contentOffset: {x: this._scrollX}}}],
   {listener: (event) => console.log(event)}, // Optional async listener
 )}
 ...
 onPanResponderMove: Animated.event([
   null,                // raw event arg ignored
   {dx: this._panX}],    // gestureState arg
{listener: (event, gestureState) => console.log(event, gestureState)}, // Optional async listener
 ),
```

Config é um objeto que pode ter as seguintes opções:

- `listener`: Optional async listener.
- `useNativeDriver`: Usa o driver nativo quando verdadeiro. Padrão falso.

---

### `forkEvent()`

```jsx
static forkEvent(event, listener)
```

API imperativa avançada para espionar eventos animados que são transmitidos por meio de props. Ele permite adicionar um novo ouvinte javascript a um `AnimateDvent` existente. Se `AnimateDvent` for um ouvinte javascript, ele mesclará os 2 ouvintes em um único, e se `AnimateDvent` for nulo/indefinido, ele atribuirá o ouvinte javascript diretamente. Use valores diretamente sempre que possível.

---

### `unforkEvent()`

```jsx
static unforkEvent(event, listener)
```

---

### `start()`

```jsx
static start([callback]: ?(result?: {finished: boolean}) => void)
```

As animações são iniciadas chamando start () em sua animação. O start () recebe um retorno de chamada de conclusão que será chamado quando a animação for concluída ou quando a animação for concluída porque stop () foi chamado antes de terminar.

**Parameters:**

| Name     | Type                            | Required | Description                                                                                                                                                     |
| -------- | ------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| callback | ?(result?: {finished: boolean}) | No       | Função que será chamada depois que a animação terminar em execução normalmente ou quando a animação for concluída porque stop () foi chamada nela antes que ela pudesse terminar |

Comece o exemplo com o retorno de chamada:

```jsx
Animated.timing({}).start(({ finished }) => {
  /* completion callback */
});
```

---

### `stop()`

```jsx
static stop()
```

Interrompe qualquer animação em execução.

---

### `reset()`

```jsx
static reset()
```

Interrompe qualquer animação em execução e redefine o valor para o original.

## Properties

### `Value`

Classe de valor padrão para dirigir animações. Normalmente inicializado com `new Animated.Value (0); `

Você pode ler mais sobre a API `Animated.Value` na [página] separada (animatedvalue).

---

### `ValueXY`

Classe de valor 2D para gerar animações 2D, como gestos de panorâmica.

Você pode ler mais sobre a API `Animated.valueXY` na [página] separada (animatedvaluexy).

---

### `Interpolation`

Exportado para usar o tipo de interpolação no fluxo.

---

### `Node`

Exportado para facilitar a verificação de tipos. Todos os valores animados derivam dessa classe.

---

### `createAnimatedComponent`

Torne qualquer componente React animável. Usado para criar `Animated.View`, etc.

---

### `attachNativeEvent`

API imperativa para anexar um valor animado a um evento em uma exibição. Prefira usar `Animated.event` com `useNativeDrive: true` se possível.
