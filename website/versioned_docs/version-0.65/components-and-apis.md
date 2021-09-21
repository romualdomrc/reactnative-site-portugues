---
id: components-and-apis
title: Core Components and APIs
---

O React Native fornece vários [Componentes principais](intro-react-native-components) integrados prontos para você usar em seu aplicativo. Você pode encontrá-los todos na barra lateral esquerda (ou no menu acima, se você estiver em uma tela estreita). Se você não sabe por onde começar, dê uma olhada nas seguintes categorias:

- [Basic Components](components-and-apis#basic-components)
- [User Interface](components-and-apis#user-interface)
- [List Views](components-and-apis#list-views)
- [Android-specific](components-and-apis#android-components-and-apis)
- [iOS-specific](components-and-apis#ios-components-and-apis)
- [Others](components-and-apis#others)

Você não está limitado aos componentes e APIs incluídos no React Native. O React Native tem uma comunidade de milhares de desenvolvedores. Se você está procurando uma biblioteca que faça algo específico, consulte [este guia sobre como encontrar bibliotecas](bibliotecas#finding-libraries).

## Basic Components

A maioria dos aplicativos acabará usando um desses componentes básicos.

<div className="component-grid component-grid-border">
  <div className="component">
    <a href="./view">
      <h3>View</h3>
      <p>O componente fundamental para construir uma UI.</p>
    </a>
  </div>
  <div className="component">
    <a href="./text">
      <h3>Text</h3>
      <p>Um componente para exibir texto.</p>
    </a>
  </div>
  <div className="component">
    <a href="./image">
      <h3>Image</h3>
      <p>Um componente para exibir imagens.</p>
    </a>
  </div>
  <div className="component">
    <a href="./textinput">
      <h3>TextInput</h3>
      <p>Um componente para inserir texto no aplicativo por meio do teclado.</p>
    </a>
  </div>
  <div className="component">
    <a href="./scrollview">
      <h3>ScrollView</h3>
      <p>Fornece um contêiner com rolagem da tela que pode conter diversos componentes.
     </p>
    </a>
  </div>
  <div className="component">
    <a href="./stylesheet">
      <h3>StyleSheet</h3>
      <p>Fornece uma camada de abstração semelhantes às folhas de estilo CSS.</p>
    </a>
  </div>
</div>

## Interface do usuário

Esses controles comuns da interface do usuário serão renderizados em qualquer plataforma.

<div className="component-grid component-grid-border">
  <div className="component">
    <a href="./button">
      <h3>Button</h3>
      <p>
      Um componente de botão básico para gerenciar toques que deve renderizar bem em qualquer plataforma
      </p>
    </a>
  </div>
  <div className="component">
    <a href="./switch">
      <h3>Switch</h3>
      <p>Renderiza uma entrada booleana</p>
    </a>
  </div>
</div>

## Visualizações de lista

Ao contrário do mais genérico [`ScrollView`](./scrollview), os seguintes componentes de exibição de lista renderizam apenas elementos que estão sendo exibidos na tela. Isso os torna uma escolha de alto desempenho para exibir listas longas de dados.

<div className="component-grid component-grid-border">
  <div className="component">
    <a href="./flatlist">
      <h3>FlatList</h3>
      <p>Um componente para renderizar com desempenho listas com rolagem da tela.</p>
    </a>
  </div>
  <div className="component">
    <a href="./sectionlist">
      <h3>SectionList</h3>
      <p>Como <code>FlatList</code>, mas para listas seccionadas.</p>
    </a>
  </div>
</div>

## Android Components and APIs

Muitos dos componentes a seguir fornecem invólucros para classes Android comumente usadas.

<div className="component-grid component-grid-border">
  <div className="component">
    <a href="./backhandler">
      <h3>BackHandler</h3>
      <p>Detect pressionamentos de botões físicos para navegação de retorno</p>
    </a>
  </div>
  <div className="component">
    <a href="./drawerlayoutandroid">
      <h3>DrawerLayoutAndroid</h3>
      <p>Renderiza um <code>DrawerLayout</code> no Android.</p>
    </a>
  </div>
  <div className="component">
    <a href="./permissionsandroid">
      <h3>PermissionsAndroid</h3>
      <p>Fornece acesso ao modelo de permissões introduzido no Android M.</p>
    </a>
  </div>
  <div className="component">
    <a href="./toastandroid">
      <h3>ToastAndroid</h3>
      <p>Cria um Android Toast alert.</p>
    </a>
  </div>
</div>

## Componentes e APIs do iOS

Muitos dos componentes a seguir fornecem invólucros para classes UIKit comumente usadas.

<div className="component-grid component-grid-border">
  <div className="component">
    <a href="./actionsheetios">
      <h3>ActionSheetIOS</h3>
      <p>API para mostrar iOS folhas de ação ou de compartilhamento.</p>
    </a>
  </div>
</div>

## Outros

Esses componentes podem ser úteis para determinados aplicativos. Para obter uma lista exaustiva de componentes e APIs, confira a barra lateral à esquerda (ou o menu acima, se você estiver em uma tela estreita).

<div className="component-grid">
  <div className="component">
    <a href="./activityindicator">
      <h3>ActivityIndicator</h3>
      <p>Apresenta um indicador de carregamento circular.</p>
    </a>
  </div>
  <div className="component">
    <a href="./alert">
      <h3>Alert</h3>
      <p>Inicia uma caixa de diálogo de alerta com o título e a mensagem especificados.
      </p>
    </a>
  </div>
  <div className="component">
    <a href="./animated">
      <h3>Animated</h3>
      <p>Uma biblioteca para criar animações fluidas e poderosas que são fáceis de construir e manter.</p>
    </a>
  </div>
  <div className="component">
    <a href="./dimensions">
      <h3>Dimensions</h3>
      <p>Fornece uma interface para obter as dimensões do dispositivo.</p>
    </a>
  </div>
  <div className="component">
    <a href="./keyboardavoidingview">
      <h3>KeyboardAvoidingView</h3>
      <p>Fornece uma view que redimenciona para sair da frente do teclado virtual automaticamente.</p>
    </a>
  </div>
  <div className="component">
    <a href="./linking">
      <h3>Linking</h3>
      <p>Fornece uma interface geral para interagir com links de aplicativos de entrada e saída.</p>
    </a>
  </div>
  <div className="component">
    <a href="./modal">
      <h3>Modal</h3>
      <p>Fornece uma maneira simples de apresentar o conteúdo sobre uma visualização existente.</p>
    </a>
  </div>
  <div className="component">
    <a href="./pixelratio">
      <h3>PixelRatio</h3>
      <p>Provides access to the device pixel density.</p>
    </a>
  </div>
  <div className="component">
    <a href="./refreshcontrol">
      <h3>RefreshControl</h3>
      <p>Este componente é usado dentro de um <code>ScrollView</code> para adicionar uma funcionalidade de atualização por pull.</p>
    </a>
  </div>
  <div className="component">
    <a href="./statusbar">
      <h3>StatusBar</h3>
      <p>Componente para controlar a barra de status do aplicativo.</p>
    </a>
  </div>
</div>
