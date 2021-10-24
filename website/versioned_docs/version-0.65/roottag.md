---
id: roottag
title: RootTag
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

`RootTag` é um identificador opaco atribuído à visualização raiz nativa da sua superfície React Native - ou seja, a instância `ReactRootView` ou `RCTRootView` para Android ou iOS, respectivamente. Resumindo, é um identificador de superfície.

## Quando usar um RootTag?

Para a maioria dos desenvolvedores React Native, você provavelmente não precisará lidar com `Roottag`s.

`Roottag`s são úteis para quando um aplicativo renderiza o**várias visualizações raiz do React Native** e você precisa lidar com chamadas de API nativas de maneira diferente, dependendo da superfície. Um exemplo disso é quando um aplicativo está usando navegação nativa e cada tela é uma visualização raiz do React Native separada.

Na navegação nativa, cada visualização raiz do React Native é renderizada na visualização de navegação de uma plataforma (por exemplo, `Activity` para Android, `UINavigationViewController` para iOS). Com isso, você é capaz de alavancar os paradigmas de navegação da plataforma, como aparência nativa e transições de navegação. A funcionalidade para interagir com as APIs de navegação nativas pode ser exposta ao React Native por meio de um [módulo nativo] (https://reactnative.dev/docs/next/native-modules-intro).

Por exemplo, para atualizar a barra de título de uma tela, você chamaria a API do módulo de navegação `setTitle (“Título atualizado”) `, mas ele precisaria saber qual tela da pilha atualizar. Uma `RootTag` é necessária aqui para identificar a visualização raiz e seu contêiner de hospedagem.

Outro caso de uso para `RootTag` é quando seu aplicativo precisa atribuir uma determinada chamada JavaScript ao nativo com base em sua visualização raiz de origem. Uma `RootTag` é necessária para diferenciar a fonte da chamada de diferentes superfícies.

## Como acessar o RootTag... se você precisar

Nas versões 0.65 e abaixo, o RootTag é acessado por meio de um [contexto legado] (https://github.com/facebook/react-native/blob/v0.64.1/Libraries/ReactNative/AppContainer.js#L56). Para preparar os recursos do React Native for Concurrent que chegam no React 18 e além, estamos migrando para a mais recente [API de contexto] (https://reactjs.org/docs/context.html#api) via `RootTagContext` em 0.66. A versão 0.65 suporta o contexto legado e o `RootTagContext` recomendado para permitir que os desenvolvedores tenham tempo para migrar seus sites de chamada. Veja o resumo das mudanças mais recentes.

Como acessar `RootTag` através do `RootTagContext`.

```js
import { RootTagContext } from 'react-native';
import NativeAnalytics from 'native-analytics';
import NativeNavigation from 'native-navigation';

function ScreenA() {
  const rootTag = useContext(RootTagContext);

  const updateTitle = (title) => {
    NativeNavigation.setTitle(rootTag, title);
  };

  const handleOneEvent = () => {
    NativeAnalytics.logEvent(rootTag, 'one_event');
  };

  // ...
}

class ScreenB extends React.Component {
  static contextType: typeof RootTagContext = RootTagContext;

  updateTitle(title) {
    NativeNavigation.setTitle(this.context, title);
  }

  handleOneEvent() {
    NativeAnalytics.logEvent(this.context, 'one_event');
  }

  // ...
}
```

Saiba mais sobre a API de contexto para [classes] (https://reactjs.org/docs/context.html#classcontexttype) e [hooks] (https://reactjs.org/docs/hooks-reference.html#usecontext) nos documentos do React.

### Quebrando a mudança em 0,65

`RootTagContext` foi anteriormente chamado de `unstable_roottagContext` e alterado para `roottagContext` em 0.65. Atualize todos os usos de `Unstable_roottagContext` em sua base de código.

### Quebrando a mudança em 0,66

O acesso de contexto legado a `RootTag` será removido e substituído por `RootTagContext`. A partir de 0.65, incentivamos os desenvolvedores a migrar proativamente os acessos `RootTag` para `RootTagContext`.

## Planos futuros

Com a nova arquitetura React Native progredindo, haverá futuras iterações para `RootTag`, com a intenção de manter o tipo `RootTag` opaco e evitar thrash nas bases de código React Native. Por favor, não confie no fato de que o RootTag atualmente é um alias para um número! Se seu aplicativo depende de RootTags, fique de olho em nossos registros de alteração de versão, que você pode encontrar [aqui] (https://github.com/react-native-community/releases/blob/master/CHANGELOG.md).
