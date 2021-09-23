---
id: appregistry
title: AppRegistry
---

 <div className="banner-native-code-required"> 
 <h3> Projeto com código nativo necessário </h3> 
 <p> 
 Se você estiver usando o fluxo de trabalho gerenciado <code> expo-cli </code>, há apenas um componente de entrada registrado com <code> AppRegistry </code> e ele é tratado automaticamente, você não precisa usar essa API.
 </p> 
 </div> 

`AppRegistry` é o ponto de entrada JS para executar todos os aplicativos React Native. Os componentes raiz do aplicativo devem se registrar com `AppRegistry.registerComponent`, então o sistema nativo pode carregar o pacote para o aplicativo e, em seguida, executar o aplicativo quando ele estiver pronto, invocando `appRegistry.runApplication`.

```jsx
import { Text, AppRegistry } from 'react-native';

const App = (props) => (
  <View>
    <Text>App1</Text>
  </View>
);

AppRegistry.registerComponent('Appname', () => App);
```

Para “parar” um aplicativo quando uma visualização deve ser destruída, chame `AppRegistry.UnmountApplicationComponentaTrootTag` com a tag que foi passada para `RunApplication`. Eles sempre devem ser usados como um par.

O `AppRegistro de aplicação` deve ser necessário no início da sequência `require` para garantir que o ambiente de execução JS esteja configurado antes que outros módulos sejam necessários.

---

# Referência

## Métodos

### `cancelHeadlessTask()`

```jsx
static cancelHeadlessTask(taskId, taskKey)
```

Chamado apenas de código nativo. Cancela uma tarefa sem cabeça.

**Parâmetros: **

| Nome                                                         | Tipo   | Descrição                                                                             |
| ------------------------------------------------------------ | ------ | --------------------------------------------------------------------------------------- |
| taskId <div className="label basic required">Required</div>  | number | O id nativo dessa instância de tarefa que foi usado quando `StartEadlessTask` foi chamado. |
| taskKey <div className="label basic required">Required</div> | string | A chave para a tarefa que foi usada quando `StartEadlessTask` foi chamada.                 |

---

### `enableArchitectureIndicator()`

```jsx
static enableArchitectureIndicator(enabled)
```

**Parâmetros: **

| Nome                                                         | Tipo    |
| ------------------------------------------------------------ | ------- |
| enabled <div className="label basic required">Required</div> | boolean |

---

### `getAppKeys()`

```jsx
static getAppKeys()
```

Retorna uma matriz de strings.

---

### `getRegistry()`

```jsx
static getRegistry()
```

Retorna um objeto [Registry] (appregistry #registry).

---

### `getRunnable()`

```jsx
static getRunnable(appKey)
```

Retorna um objeto [Runnable] (appregistry #runnable).

**Parâmetros: **

| Nome                                                        | Tipo   |
| ----------------------------------------------------------- | ------ |
| appKey <div className="label basic required">Required</div> | string |

---

### `getSectionKeys()`

```jsx
static getSectionKeys()
```

Retorna uma matriz de strings.

---

### `getSections()`

```jsx
static getSections()
```

Retorna um objeto [Runnables] (appregistry #runnables).

---

### `registerCancellableHeadlessTask()`

```jsx
static registerCancellableHeadlessTask(taskKey, taskProvider, taskCancelProvider)
```

Registre uma tarefa sem cabeça que pode ser cancelada. Uma tarefa sem cabeça é um pouco de código que é executado sem uma interface do usuário.

**Parâmetros: **

| Nome                                                                                  | Tipo                                                 | Descrição                                                                                                                                                                                                                         |
| ------------------------------------------------------------------------------------- | ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| taskKey<br/><div className="label basic required two-lines">Required</div>            | string                                               | O id nativo dessa instância de tarefa que foi usado quando StartEadlessTask foi chamado.                                                                                                                                               |
| taskProvider<br/><div className="label basic required two-lines">Required</div>       | [TaskProvider](appregistry#taskprovider)             | Uma função de retorno de promessa que usa alguns dados passados do lado nativo como o único argumento. Quando a promessa é resolvida ou rejeitada, o lado nativo é notificado desse evento e pode decidir destruir o contexto JS. |
| taskCancelProvider<br/><div className="label basic required two-lines">Required</div> | [TaskCancelProvider](appregistry#taskcancelprovider) | uma função de retorno vazio que não aceita argumentos; quando um cancelamento é solicitado, a função que está sendo executada pelo TaskProvider deve encerrar e retornar o mais rápido possível.                                                                    |

---

### `registerComponent()`

```jsx
static registerComponent(appKey, componentProvider, section?)
```

**Parâmetros: **

| Nome                                                                   | Tipo              |
| ---------------------------------------------------------------------- | ----------------- |
| appKey <div className="label basic required">Required</div>            | string            |
| componentProvider <div className="label basic required">Required</div> | ComponentProvider |
| section                                                                | boolean           |

---

### `registerConfig()`

```jsx
static registerConfig(config)
```

**Parâmetros: **

| Nome                                                        | Tipo                               |
| ----------------------------------------------------------- | ---------------------------------- |
| config <div className="label basic required">Required</div> | [AppConfig](appregistry#appconfig) |

---

### `registerHeadlessTask()`

```jsx
static registerHeadlessTask(taskKey, taskProvider)
```

Registre uma tarefa sem cabeça. Uma tarefa sem cabeça é um pouco de código que é executado sem uma interface do usuário.

Essa é uma forma de executar tarefas em JavaScript enquanto o aplicativo está em segundo plano. Ele pode ser usado, por exemplo, para sincronizar dados novos, lidar com notificações push ou reproduzir música.

**Parâmetros: **

| Nome                                                                        | Tipo                                     | Descrição                                                                                                                                                                                                                         |
| --------------------------------------------------------------------------- | ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| taskKey <div className="label basic required two-lines">Required</div>      | string                                   | O id nativo dessa instância de tarefa que foi usado quando StartEadlessTask foi chamado.                                                                                                                                               |
| taskProvider <div className="label basic required two-lines">Required</div> | [TaskProvider](appregistry#taskprovider) | Uma função de retorno de promessa que usa alguns dados passados do lado nativo como o único argumento. Quando a promessa é resolvida ou rejeitada, o lado nativo é notificado desse evento e pode decidir destruir o contexto JS. |

---

### `registerRunnable()`

```jsx
static registerRunnable(appKey, run)
```

**Parâmetros: **

| Nome                                                        | Tipo     |
| ----------------------------------------------------------- | -------- |
| appKey <div className="label basic required">Required</div> | string   |
| run <div className="label basic required">Required</div>    | function |

---

### `registerSection()`

```jsx
static registerSection(appKey, component)
```

**Parâmetros: **

| Nome                                                           | Tipo              |
| -------------------------------------------------------------- | ----------------- |
| appKey <div className="label basic required">Required</div>    | string            |
| component <div className="label basic required">Required</div> | ComponentProvider |

---

### `runApplication()`

```jsx
static runApplication(appKey, appParameters)
```

Carrega o pacote JavaScript e executa o aplicativo.

**Parâmetros: **

| Nome                                                               | Tipo   |
| ------------------------------------------------------------------ | ------ |
| appKey <div className="label basic required">Required</div>        | string |
| appParameters <div className="label basic required">Required</div> | any    |

---

### `setComponentProviderInstrumentationHook()`

```jsx
static setComponentProviderInstrumentationHook(hook)
```

**Parâmetros: **

| Nome                                                      | Tipo     |
| --------------------------------------------------------- | -------- |
| hook <div className="label basic required">Required</div> | function |

Uma função `hook` válida aceita o seguinte como argumentos:

| Nome                                                                         | Tipo               |
| ---------------------------------------------------------------------------- | ------------------ |
| component <div className="label basic required">Required</div>               | ComponentProvider  |
| scopedPerformanceLogger <div className="label basic required">Required</div> | IPerformanceLogger |

A função também deve retornar um Componente React.

---

### `setWrapperComponentProvider()`

```jsx
static setWrapperComponentProvider(provider)
```

**Parâmetros: **

| Nome                                                          | Tipo              |
| ------------------------------------------------------------- | ----------------- |
| provider <div className="label basic required">Required</div> | ComponentProvider |

---

### `startHeadlessTask()`

```jsx
static startHeadlessTask(taskId, taskKey, data)
```

Chamado apenas de código nativo. Inicia uma tarefa sem cabeça.

**Parâmetros: **

| Nome                                                         | Tipo   | Descrição                                                          |
| ------------------------------------------------------------ | ------ | -------------------------------------------------------------------- |
| taskId <div className="label basic required">Required</div>  | number | O id nativo dessa instância de tarefa para acompanhar sua execução. |
| taskKey <div className="label basic required">Required</div> | string | The key for the task to start.                                       |
| data <div className="label basic required">Required</div>    | any    | The data to pass to the task.                                        |

---

### `unmountApplicationComponentAtRootTag()`

```jsx
static unmountApplicationComponentAtRootTag(rootTag)
```

Interrompe um aplicativo quando uma exibição deve ser destruída.

**Parâmetros: **

| Nome                                                         | Tipo   |
| ------------------------------------------------------------ | ------ |
| rootTag <div className="label basic required">Required</div> | number |

## Type Definitions

### AppConfig

Configuração do aplicativo para o método `RegisterConfig`.

| Type   |
| ------ |
| object |

**Propriedades: **

| Nome                                                        | Tipo              |
| ----------------------------------------------------------- | ----------------- |
| appKey <div className="label basic required">Required</div> | string            |
| component                                                   | ComponentProvider |
| run                                                         | function          |
| section                                                     | boolean           |

> **Nota: ** Espera-se que toda configuração defina a função `component` ou` run`.

### Registry

| Type   |
| ------ |
| object |

**Properties:**

| Nome      | Tipo                                       |
| --------- | ------------------------------------------ |
| runnables | matriz de [Runnables] (registro de appregistry #runnable) |
| sections  | matriz de cordas                           |

### Runnable

| Type   |
| ------ |
| object |

**Propriedades: **

| Nome      | Tipo              |
| --------- | ----------------- |
| component | ComponentProvider |
| run       | function          |

### Runnables

Um objeto com chave de `AppKey` e valor do tipo de [`Runnable`] (appregistry #runnable).

| Type   |
| ------ |
| object |

### Task

Uma `Tarefa` é uma função que aceita qualquer dado como argumento e retorna uma Promessa que resolve para `indefinido`.

| Type     |
| -------- |
| function |

### TaskCanceller

Um `TaskCanceller` é uma função que não aceita argumentos e retorna void.

| Type     |
| -------- |
| function |

### TaskCancelProvider

Um `TaskCancelProvider` válido é uma função que retorna um [`TaskCanceller`] (appregistry #taskcanceller).

| Type     |
| -------- |
| function |

### TaskProvider

Um `TaskProvider` válido é uma função que retorna um [`Task`] (appregistry #task).

| Type     |
| -------- |
| function |
