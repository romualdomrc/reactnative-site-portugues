---
id: interactionmanager
title: InteractionManager
---

O InteractionManager permite que o trabalho de longa duração seja agendado após a conclusão de quaisquer interações/animações. Em particular, isso permite que as animações JavaScript sejam executadas sem problemas.

Os aplicativos podem agendar tarefas para serem executadas após interações com o seguinte:

```jsx
InteractionManager.runAfterInteractions(() => {
  // ...long-running synchronous task...
});
```

Compare isso com outras alternativas de agendamento:

- requestAnimationFrame (): para código que anima uma exibição ao longo do tempo.
- setImmediate/setTimeout (): execute o código mais tarde, observe que isso pode atrasar as animações.
- runAfterInteractions (): execute o código mais tarde, sem atrasar as animações ativas.

O sistema de tratamento de toque considera um ou mais toques ativos como uma 'interação' e atrasará os retornos de chamada `runAfterInteractions () `até que todos os toques tenham terminado ou sejam cancelados.

O InteractionManager também permite que os aplicativos registrem animações criando um “identificador” de interação no início da animação e limpe-o após a conclusão:

```jsx
var handle = InteractionManager.createInteractionHandle();
// run animation... (`runAfterInteractions` tasks are queued)
// later, on animation completion:
InteractionManager.clearInteractionHandle(handle);
// queued tasks run if all handles were cleared
```

`RunAfterInteractions` usa uma função de retorno de chamada simples ou um objeto `PromiseTask` com um método` gen` que retorna um `Promise`. Se um `PromiseTask` for fornecido, ele será totalmente resolvido (incluindo dependências assíncronas que também programam mais tarefas via `RunAfterInteractions`) antes de iniciar a próxima tarefa que pode ter sido enfileirada de forma síncrona anteriormente.

Por padrão, as tarefas enfileiradas são executadas juntas em um loop em um lote `setImmediate`. Se `setDeadline` for chamado com um número positivo, as tarefas só serão executadas até que o prazo (em termos de tempo de execução do loop de eventos js) se aproxime, momento em que a execução será produzida via setTimeout, permitindo que eventos como toques iniciem interações e bloqueiem a execução de tarefas em fila, tornando os aplicativos mais responsivo.

---

## Exemplo

### Básico

```SnackPlayer name=InteractionManager%20Function%20Component%20Basic%20Example&supportedPlatforms=ios,android
import React, { useState, useEffect } from "react";
import {
  Alert,
  Animated,
  InteractionManager,
  Platform,
  StyleSheet,
  Text,
  View,
} from "react-native";

const instructions = Platform.select({
  ios: "Press Cmd+R to reload,\n" + "Cmd+D or shake for dev menu",
  android:
    "Double tap R on your keyboard to reload,\n" +
    "Shake or press menu button for dev menu",
});

const useMount = func => useEffect(() => func(), []);

const useFadeIn = (duration = 5000) => {
  const [opacity] = useState(new Animated.Value(0));

  // Running the animation when the component is mounted
  useMount(() => {
    // Animated.timing() create a interaction handle by default, if you want to disabled that
    // behaviour you can set isInteraction to false to disabled that.
    Animated.timing(opacity, {
      toValue: 1,
      duration,
    }).start();
  });

  return opacity;
};

const Ball = ({ onShown }) => {
  const opacity = useFadeIn();

  // Running a method after the animation
  useMount(() => {
    const interactionPromise = InteractionManager.runAfterInteractions(() => onShown());
    return () => interactionPromise.cancel();
  });

  return <Animated.View style={[styles.ball, { opacity }]} />;
};

const App = () => {
  return (
    <View style={styles.container}>
      <Text>{instructions}</Text>
      <Ball onShown={() => Alert.alert("Animation is done")} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", alignItems: "center" },
  ball: {
    width: 100,
    height: 100,
    backgroundColor: "salmon",
    borderRadius: 100,
  },
});

export default App;
```

### Advanced

```SnackPlayer name=InteractionManager%20Function%20Component%20Advanced%20Example&supportedPlatforms=ios,android
import React, { useEffect } from "react";
import {
  Alert,
  Animated,
  InteractionManager,
  Platform,
  StyleSheet,
  Text,
  View,
} from "react-native";

const instructions = Platform.select({
  ios: "Press Cmd+R to reload,\n" + "Cmd+D or shake for dev menu",
  android:
    "Double tap R on your keyboard to reload,\n" +
    "Shake or press menu button for dev menu",
});

const useMount = func => useEffect(() => func(), []);

// You can create a custom interaction/animation and add
// support for InteractionManager
const useCustomInteraction = (timeLocked = 2000) => {
  useMount(() => {
    const handle = InteractionManager.createInteractionHandle();

    setTimeout(
      () => InteractionManager.clearInteractionHandle(handle),
      timeLocked
    );

    return () => InteractionManager.clearInteractionHandle(handle);
  });
};

const Ball = ({ onInteractionIsDone }) => {
  useCustomInteraction();

  // Running a method after the interaction
  useMount(() => {
    InteractionManager.runAfterInteractions(() => onInteractionIsDone());
  });

  return <Animated.View style={[styles.ball]} />;
};

const App = () => {
  return (
    <View style={styles.container}>
      <Text>{instructions}</Text>
      <Ball onInteractionIsDone={() => Alert.alert("Interaction is done")} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", alignItems: "center" },
  ball: {
    width: 100,
    height: 100,
    backgroundColor: "salmon",
    borderRadius: 100,
  },
});

export default App;
```

> **Note**: `InteractionManager.runAfterInteractions()` is not working properly on web. It triggers immediately without waiting until the interaction is finished.

# Referência

## Métodos

### `runAfterInteractions()`

```jsx
static runAfterInteractions(task)
```

Agende uma função para ser executada após a conclusão de todas as interações. Retorna uma “promessa” cancelável.

---

### `createInteractionHandle()`

```jsx
static createInteractionHandle()
```

Notifique o gerente de que uma interação foi iniciada.

---

### `clearInteractionHandle()`

```jsx
static clearInteractionHandle(handle)
```

Notifique o gerente de que uma interação foi concluída.

---

### `setDeadline()`

```jsx
static setDeadline(deadline)
```

Um número positivo usará setTimeout para agendar quaisquer tarefas após o EventLoopRunningTime atingir o valor do prazo, caso contrário, todas as tarefas serão executadas em um lote setImmediate (padrão).
