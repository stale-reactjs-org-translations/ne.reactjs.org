---
id: state-and-lifecycle
title: State and Lifecycle
permalink: docs/state-and-lifecycle.html
redirect_from:
  - "docs/interactivity-and-dynamic-uis.html"
prev: components-and-props.html
next: handling-events.html
---

यस पृष्ठले React कम्पोनेंटमा state र lifecycle को अवधारणा प्रस्तुत गर्दछ। तपाइँ [यहाँ विस्तृत कम्पोनेंट API सन्दर्भ](/docs/react-component.html) भेट्टाउन सक्नुहुन्छ।

<<<<<<< HEAD
अघिल्लो अंश मध्ये एकबाट [टिक टिक गर्ने घडीको उदाहरण](/docs/rendering-elements.html#updating-the-rendered-element)लाई विचार गर्नुहोस्। [Elements render](/docs/rendering-elements.html#rendering-an-element-into-the-dom)गर्दा हामीले UI अद्यावधिक गर्न केवल एक मात्र तरीका सिकेका छौं। Render भएको आउटपुट परिवर्तन गर्न हामी `ReactDOM.render()` कल गर्छौं।
=======
Consider the ticking clock example from [one of the previous sections](/docs/rendering-elements.html#updating-the-rendered-element). In [Rendering Elements](/docs/rendering-elements.html#rendering-an-element-into-the-dom), we have only learned one way to update the UI. We call `root.render()` to change the rendered output:
>>>>>>> c7d858947f832d1ba4e78caebc391fd964ff6de6

```js{10}
const root = ReactDOM.createRoot(document.getElementById('root'));
  
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  root.render(element);
}

setInterval(tick, 1000);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/gwoJZk?editors=0010)

यस अंशमा हामी `Clock` कम्पोनेंटलाई कसरी पुन: प्रयोज्य बनाउन र encapsulate गर्न सकिन्छ भन्ने बारे सिक्ने छौं। यसले आफ्नै टाइमर सेटअप गर्नेछ र प्रत्येक सेकेन्डमा अद्यावधिक हुनेछ।

सुरुवातमा, हामीले घडी को बाहिरी रुप encapsulate गर्न सक्छौँ:

```js{5-8,13}
const root = ReactDOM.createRoot(document.getElementById('root'));

function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  root.render(<Clock date={new Date()} />);
}

setInterval(tick, 1000);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/dpdoYR?editors=0010)

यद्यपि यसले महत्त्वपूर्ण आवश्यकतालाई वेवास्ता गर्दछ, `Clock`ले एक टाइमर सेट अप गर्दछ र UI लाई प्रत्येक सेकेन्ड अद्यावधिक गर्दछ भन्ने तथ्य `Clock`को कार्यान्वयन विवरण भित्र रहनुपर्छ।

आदर्श रूपमा हामी यसलाई एक पटक लेख्न चाहन्छौं र `Clock` आफैंले अद्यावधिक भएको चाहान्छौं:

```js{2}
root.render(<Clock />);
```

यसलाई कार्यान्वयन गर्न हामीले `Clock`कम्पोनेंटमा "state" थप्न आवश्यक छ।

State Props जस्तै छ तर यो निजी हुन्छ​ र पूरै कम्पोनेंटद्वारा नियन्त्रित हुन्छ​।

## Functionलाई classमा रूपान्तरण गर्ने तरिका{#converting-a-function-to-a-class}

तपाईं `Clock` जस्तो function कम्पोनेंटलाई classमा पाँच चरणमा रूपान्तरण गर्न सक्नुहुन्छ।

१. उही नामको [ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes) जसले `React.Component` extend गर्दछ।

२. यसमा `render()` नाम भएको एक खाली खाली method थप्नुहोस्।

३. `render()` methodमा functionको body सार्नुहोस्।

४. `render()` method भित्र `props`लाई `this.props`ले बदल्नुहोस्.

५. बाँकी खाली functionको घोषणा मेटाउनुहोस्।

```js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/zKRGpo?editors=0010)

`Clock` अब functionको सट्टा classको रूपमा परिभाषित गरिएको छ।

प्रत्येक चोटि अद्यावधिक हुने बित्तिकै `render` method चल्नेछ, तर जबसम्म हामी उहि DOM नोडमा `<Clock />` render गर्दछौं `Clock` classको एक मात्र instance प्रयोग गरिने छ। यसले हामीलाई थप सुविधाहरू जस्तै स्थानिय state र लाइफसाइकल methodहरू प्रयोग गर्न दिन्छ।

## Classमा स्थानिय State थप्ने तरिका {#adding-local-state-to-a-class}

हामी `date`लाई propsबाट stateमा तीन चरणमा सार्नेछौं:

१) `render()` methodमा `this.props.date`लाई `this.state.date`ले बदल्नुहोस्:

```js{6}
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

२) [Class constructor](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes#Constructor) थप्नुहोस् जसले प्रारम्भिक `this.state` प्रदान गर्दछ:

```js{4}
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

हामी कसरी base constructorमा `props` पास गर्छौं, टिपोट गर्नुहोस्:

```js{2}
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
```

Class कम्पोनेंटहरूले सँधै base constructorलाई `props`को साथमा कल गर्नुपर्दछ।

३) `<Clock />` एलिमेन्टबाट `date` prop हटाउनुहोस्:

```js{2}
root.render(<Clock />);
```

हामी पछि टाइमर कोड कम्पोनेंटमा थप्नेछौं।

परिणाम यस्तो देखिन्छ:

```js{2-5,11,18}
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Clock />);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/KgQpJd?editors=0010)

अब, हामीले `Clock` लाई आफ्नै टाइमर सेटअप गर्ने योग्य र प्रत्येक सेकेन्डमा आफैं अद्यावधिक हुने बनाउनेछौं।

## Classमा लाइफसाइकल method थप्ने तरिका {#adding-lifecycle-methods-to-a-class}

धेरै कम्पोनेंटहरू सहितको Applicationहरूमा कम्पोनेंटहरू नष्ट हुने बित्तिकै कम्पोनेंटहरू द्वारा लिइएको resourcesहरू खाली गर्न यो धेरै महत्त्वपूर्ण छ।

जब `Clock` पहिलो पटक DOM मा render हुन्छ, हामी एक [टाइमर सेट अप गर्न](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) चाहन्छौं। यसलाई Reactमा "Mounting" भनिन्छ।

जब `Clock` द्वारा निर्मित DOM हटाईन्छ, हामी [टाइमर खाली गर्न](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/clearInterval) पनि चाहन्छौं। यसलाई Reactमा "Unmounting" भनिन्छ।

कम्पोनेंट classमा हामी विशेष methodहरू घोषणा गर्न सक्दछौं जसले एक कम्पोनेंट माउन्ट अथवा अनमाउन्ट हुने बेला कुनै कोड चलाउन सक्छ:

```js{7-9,11-13}
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {

  }

  componentWillUnmount() {

  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

यी methodहरूलाई "लाइफसाइकल method" भनिन्छ।

कम्पोनेंट आउटपुट DOMमा render गरिसकेपछि `componentDidMount()` method चल्छ। यो टाइमर सेटअप गर्नको लागि राम्रो स्थान हो:

```js{2-5}
  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
```

नोट गर्नुहोस् हामी `this`मा टाइमर आईडी कसरी भण्डारण गर्छौं। (`this.timerID`)

जबकि `this.prop` आफैं Reactद्वारा सेट अप गरिएको छ र` this.state` को एक विशेष अर्थ छ, यदि तपाईले डेटा प्रवाहमा भाग नलिएको कुरा भण्डारण गर्नुपर्छ भने तपाई classमा हातले अरु फिल्डहरू थप्न स्वतन्त्र हुनुहुन्छ (एक टाईमर आईडी जस्तै)।

हामी टाइमरलाई `componentWillUnmount()` लाइफसाइकल method नस्ट गर्नेछौ:

```js{2}
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
```

अन्तमा हामी `tick()` भनिने method निर्माण गर्नेछौं ताकि `Clock` कम्पोनेंट प्रत्येक सेकेन्डमा चल्नेछ।

यसले कम्पोनेंटको स्थानिय stateमा अद्यावधिकहरू अनुसूची गर्न `this.setState()` प्रयोग गर्दछ:

```js{18-22}
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Clock />);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/amqdNA?editors=0010)

अब प्रत्येक सेकेन्डमा घडी टिक टिक गर्दछ।

चाँडै के हुँदैछ र कुन क्रममा methodहरू चल्नेछ भनेर पुन: संक्षेप गरौं:

<<<<<<< HEAD
१) जब `<Clock />` लाई `ReactDOM.render()` मा पठाइन्छ, React ले `Clock` कम्पोनेंटको constructorलाई कल गर्दछ। किनकि `<Clock />`मा वर्तमान समय प्रदर्शन गर्न आवश्यक छ, यसले `this.state` वर्तमान समय सहितको objectको साथमा आरम्भ गर्छ। हामी पछि यो state अद्यावधिक गर्नेछौं।
=======
1) When `<Clock />` is passed to `root.render()`, React calls the constructor of the `Clock` component. Since `Clock` needs to display the current time, it initializes `this.state` with an object including the current time. We will later update this state.
>>>>>>> c7d858947f832d1ba4e78caebc391fd964ff6de6

२) React तब `Clock` कम्पोनेंटको `render()` method कल गर्दछ। Reactले स्क्रिनमा प्रदर्शन हुने कुरा यसरी सिक्छ। `Clock`को render भएको आउटपुटसँग मेल गर्न Reactले तब DOM अद्यावधिक गर्दछ।

३) जब `Clock` आउटपुट DOM मा सम्मिलित हुन्छ, Reactले `componentDidMount()` लाइफसाइकल लाई कल गर्दछ। यस भित्र `Clock` कम्पोनेंटले सेकेन्डको एक पटक कम्पोनेंटको `tick()` method कल गर्न ब्राउजरलाई टाइमर सेट अप गर्न सोध्दछ।

४) प्रत्येक सेकेन्ड ब्राउजरले `tick()` method कल गर्दछ। यसको भित्र `Clock` कम्पोनेंटले हालको समय समावेश गरेको objectसँग `setState()` कल गरेर UI अद्यावधिक अनुसूची गर्छ। यो `setState()` कलको कारण Reactलाई थाहा छ state परिवर्तन भएको छ र स्क्रिनमा के हुनुपर्दछ भनेर जान्न उसले फेरि `render()` methodलाई कल गर्दछ। यस पटक `render()` methodमा`this.state.date` फरक हुनेछ र त्यसैले render गरिएको आउटपुटमा अद्यावधिक भएको समय समावेश हुनेछ। React तदनुसार DOM अद्यावधिक गर्दछ।

५) यदि `Clock` कम्पोनेंट कहिले पनि DOM बाट हटाइन्छ, Reactले `componentWillUnmount()` लाइफसाइकल method कल गर्दछ त्यसैले टाइमर रोकिन्छ।

## कसरी Stateको सही प्रयोग गर्ने {#using-state-correctly}

त्यहाँ तीनवटा कुरा छन् जुन तपाईले `setState()`को बारेमा जान्नुपर्दछ।

### Stateको सिधा परिमार्जन नगर्नुहोस् {#do-not-modify-state-directly}

उदाहरण को लागी, यसले कम्पोनेंट पुन: render गर्दैन:

```js
// गलत
this.state.comment = 'Hello';
```

यसको सट्टा `setState()` प्रयोग गर्नुहोस्

```js
// सही
this.setState({comment: 'Hello'});
```

Constructor एक मात्र स्थान जहाँ तपाईं `this.state`मा मान प्रदान गर्न सक्नुहुन्छ।

### State अद्यावधिकहरू Asynchronous हुन सक्छ {#state-updates-may-be-asynchronous}

Reactले कार्यसम्पादन क्षमताको लागि धेरै `setState()` कलहरूलाई एक अद्यावधिकमा ब्याच गर्न सक्दछ।

किनकि `this.prop` र `this.state` asynchronous तरिकाले अद्यावधिक हुन सक्छ, तपाईंले अर्को state गणना गर्न उनीहरूको मानहरूमा भर पर्नुहुन्न।

उदाहरण को लागी, यो कोड काउन्टर अद्यावधिक गर्न असफल हुन सक्छ

```js
// गलत
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

यसलाई ठीक गर्नका लागि `setState()` को एक दोस्रो रुप प्रयोग गर्नुहोस् जुन एक objectको सट्टा function स्वीकार गर्दछ। त्यो functionले पहिलो आर्गुमेन्टको रूपमा अघिल्लो state प्राप्त गर्दछ र अद्यावधिक लागू भएको बेलाको propsहरू दोस्रो आर्गुमेन्टको रूपमा प्राप्त गर्दछ:

```js
// सही
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

हामीले माथि [arrow function](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions) प्रयोग गर्‍यौं, तर यसले regular functions सँग पनि काम गर्दछ:

```js
// सही
this.setState(function(state, props) {
  return {
    counter: state.counter + props.increment
  };
});
```

### State अद्यावधिकहरू मर्ज हुन्छन् {#state-updates-are-merged}

जब तपाइँ `setState()` कल गर्नुहुन्छ, Reactले तपाईले प्रदान गर्नु भएको objectलाई हालको stateमा मर्ज गर्दछ।

उदाहरण को लागी, तपाइँको state मा धेरै स्वतन्त्र variablesहरु हुन सक्छ:

```js{4,5}
  constructor(props) {
    super(props);
    this.state = {
      posts: [],
      comments: []
    };
  }
```

त्यसो भएपछि तपाईं तिनीहरूलाई अलग-अलग `setState()` कलहरूको साथ स्वतन्त्र रूपमा अद्यावधिक गर्न सक्नुहुनेछ:

```js{4,10}
  componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts
      });
    });

    fetchComments().then(response => {
      this.setState({
        comments: response.comments
      });
    });
  }
```

मर्जिंग सतही हुन्छ, त्यसैले `this.setState({comments})`ले `this.state.posts`लाई अक्षुण्ण छोडिदिन्छ तर पूर्ण रूपमा `this.state.comments`लाई प्रतिस्थापन गर्दछ।

## डाटा तल बग्दछ {#the-data-flows-down}

न त parent न त child कम्पोनेंटले थाहा पाउँदछन् कि यदि एक निश्चित कम्पोनेंट स्टेटफुल वा स्टेटलेस छ, र तिनीहरूले मतलब गर्नु हुँदैन कि यो एक function वा classको रूपमा परिभाषित गरिएको छ।

यसैकारण stateलाई प्राय जसो स्थानिय वा encapsulated भनिन्छ। यसलाई सेट गर्ने यसको स्वामित्व भएको कम्पोनेंट बाहेक यो कुनै अन्य कम्पोनेंटमा पहुँचयोग्य हुँदैन।

एक कम्पोनेंटले आफ्नो stateलाई propsको रूपमा त्यसको child कम्पोनेंटहरूमा पास गर्न छनौट गर्न सक्छ:

```js
<<<<<<< HEAD
<h2>It is {this.state.date.toLocaleTimeString()}.</h2>
```

यसले प्रयोगकर्ता-परिभाषित कम्पोनेंटहरूको लागि पनि काम गर्दछ:

```js
=======
>>>>>>> c9b990070fc35d31b56957263e1ea9fe2fe67b40
<FormattedDate date={this.state.date} />
```

`FormattedDate` कम्पोनेंटले आफ्नो propsमा `date` प्राप्त गर्दछ र त्यसलाई थाहा हुँदैन कि यो `Clock`को stateबाट आएको थियो कि यो `Clock`को propsबाट आएको थियो वा हातले टाइप गरिएको थियो:

```js
function FormattedDate(props) {
  return <h2>It is {props.date.toLocaleTimeString()}.</h2>;
}
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/zKRqNB?editors=0010)

यसलाई सामान्यतया "टप​-डाउन" वा "युनिडेरेक्शनल" डाटा प्रवाह भनिन्छ। कुनै पनि state सँधै केही खास कम्पोनेंटको स्वामित्वमा हुन्छ र stateबाट व्युत्पन्न कुनै पनि डाटा वा UI ले treeमा तिनीहरूभन्दा "मुनि"को कम्पोनेंटहरूमा मात्र प्रभाव पार्न सक्दछ।

यदि तपाईं कम्पोनेंट treeलाई झर्ने झरनाको रूपमा कल्पना गर्नुहुन्छ भने प्रत्येक कम्पोनेंटको state अतिरिक्त पानी स्रोत जस्तै हुन्छ जुन यसलाई एक मनमानी बिन्दुमा मिल्छ तर तल बग्दछ।

सबै कम्पोनेंटहरू साँच्चिकै पृथक छन् देखाउनका लागि हामी एक `App` कम्पोनेंट सिर्जना गर्न सक्दछौं जसले तिनओटा `<Clock>` render गर्दछ:

```js{4-6}
function App() {
  return (
    <div>
      <Clock />
      <Clock />
      <Clock />
    </div>
  );
}
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/vXdGmd?editors=0010)

प्रत्येक `Clock` ले आफ्नै टाइमर सेट अप गर्दछ र स्वतन्त्र रूपमा अद्यावधिक हुन्छ।

React appsहरूमा, एक कम्पोनेंट स्टेटफुल वा स्टेटलेस छ त्यो कम्पोनेंटको कार्यान्वयन विवरण मानिन्छ जुन समयको साथ परिवर्तन हुन सक्छ। तपाईं स्टेटफुल कम्पोनेंटहरू भित्र स्टेटलेस कम्पोनेंटहरू प्रयोग गर्न सक्नुहुनेछ र स्टेटलेस कम्पोनेंटहरूभित्र स्टेटफुल कम्पोनेंटहरू प्रयोग गर्न सक्नुहुनेछ।
