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

अघिल्लो सेक्सन मध्ये एकबाट [टिक्ने घडीको उदाहरण](/docs/rendering-elements.html#updating-the-rendered-element)लाई विचार गर्नुहोस्। [रेन्डरिंग एलिमेन्ट्स](/docs/rendering-elements.html#rendering-an-element-into-the-dom)मा हामीले युआई अपडेट गर्न केवल एक मात्र तरीका सिकेका छौं। रेन्डर्ड आउटपुट परिवर्तन गर्न हामी `ReactDOM.render()` कल गर्छौं।

```js{8-11}
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/gwoJZk?editors=0010)

यस सेक्सनमा हामी कसरी `Clock` कम्पोनेन्टलाई पुन: प्रयोज्य र encapsulated बनाउन सिक्ने छौं। यसले आफ्नै टाइमर सेटअप गर्नेछ र प्रत्येक सेकेन्डमा अपडेट हुनेछ।

हामी घडी कस्तो देखिन्छ encapsulate गरेर शुरू गर्न सक्दछौं

```js{3-6,12}
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/dpdoYR?editors=0010)

यद्यपि यसले महत्त्वपूर्ण आवश्यकतालाई वेवास्ता गर्दछ, तथ्य यो छ कि `Clock`ले एक टाइमर सेट अप गर्दछ र UI लाई प्रत्येक सेकेन्ड अपडेट गर्दछ भन्ने तथ्य `Clock`को कार्यान्वयन विवरण हुनुपर्दछ।

आदर्श रूपमा हामी यसलाई एक पटक लेख्न चाहन्छौं र `Clock` आफैंले अपडेट भएको चाहान्छौं।

```js{2}
ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

यसलाई कार्यान्वयन गर्न हामीले `Clock`कम्पोनेन्टमा "state" थप्न आवश्यक छ।

State Props जस्तै छ तर यो निजी हुन्छ​ र पूरै कम्पोनेन्टद्वारा नियन्त्रित हुन्छ​।

## एउटा functionलाई classमा रूपान्तरण गर्ने तरिका{#converting-a-function-to-a-class}

तपाईं `Clock` जस्तो function कम्पोनेन्टलाई classमा पाँच चरणमा रूपान्तरण गर्न सक्नुहुन्छ।

1. [ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes) सिर्जना गर्नुहोस् उही नामको साथ जसले `React.Component` विस्तार गर्दछ।

2. यसमा `render()` नाम भएको एक खाली खाली मेथड थप्नुहोस्।

3. `render()` मेथडमा functionको body सार्नुहोस्।

4. `render()`को bodyमा `props`लाई `this.props`ले बदल्नुहोस्.

5. बाँकी खाली functionको घोषणा मेटाउनुहोस्।

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

प्रत्येक चोटि अपडेट हुने बित्तिकै `render` मेथड चल्नेछ, तर जबसम्म हामी उहि DOM नोडमा `<Clock />` रेन्डर गर्दछौं `Clock` classको एक मात्र instance पप्रयोग गरिने छ। यसले हामीलाई थप सुविधाहरू जस्तै लोकल state र लाइफसाइकल मेथडहरू प्रयोग गर्न दिन्छ।

## Classमा लोकल State थप्ने विधि {#adding-local-state-to-a-class}

हामी `date`लाई propsबाट stateमा तीन चरणमा सार्नेछौं।

1) `render()` मेथडमा `this.props.date`लाई `this.state.date`ले बदल्नुहोस्।

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

2) [Class constructor](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes#Constructor) थप्नुहोस् जसले प्रारम्भिक `this.state` प्रदान गर्दछ।

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
हामी कसरी base कन्स्ट्रक्टरमा `props` पास गर्छौं नोट गर्नुहोस्।

```js{2}
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
```

Class कम्पोनेन्टहरू सँधै base कन्स्ट्रक्टरलाई `props`को साथ कल गर्नुपर्दछ।

3) `<Clock />` एलिमेन्टबाट `date` prop हटाउनुहोस्:

```js{2}
ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

हामी पछि टाइमर कोड कम्पोनेन्टमा फिर्ता थप्नेछौं।

परिणाम यस्तो देखिन्छ

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

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/KgQpJd?editors=0010)

अर्को, हामी `Clock` लाई यसको आफ्नै टाइमर सेटअप गर्नेछौं र प्रत्येक सेकेन्डमा आफैं अपडेट गर्ने बनाउनेछौं।

## Classमा लाइफसाइकल मेथड थप्ने विधि {#adding-lifecycle-methods-to-a-class}

धेरै कम्पोनेन्टहरू सहितको Applicationहरूमा कम्पोनेन्टहरू नष्ट हुने बित्तिकै कम्पोनेन्टहरू द्वारा लिइएको स्रोतहरू खाली गर्न यो धेरै महत्त्वपूर्ण छ।

हामी एक [टाइमर सेट अप गर्न](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) चाहन्छौं जब `Clock` पहिलो पटक DOM लाई रेन्डर गरिन्छ। यसलाई Reactमा "Mounting" भनिन्छ।

हामी पनि [टाइमर खाली गर्न](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/clearInterval) चाहन्छौं जब `Clock` द्वारा निर्मित DOM हटाईन्छ। यसलाई Reactमा "Unmounting" भनिन्छ।

कम्पोनेन्ट classमा केहि कोडहरू चलाउन हामी विशेष मेथडहरू घोषणा गर्न सक्दछौं जब एक कम्पोनेन्टले माउन्ट र अनमाउन्ट गर्दछ:

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

यी मेथडहरूलाई "लाइफसाइकल मेथड" भनिन्छ।

कम्पोनेन्ट आउटपुट DOMमा रेन्डर गरिसकेपछि `componentDidMount()` मेथड चल्छ। यो टाइमर सेटअप गर्नको लागि राम्रो स्थान हो

```js{2-5}
  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
```

नोट गर्नुहोस् हामी `this`मा टाइमर आईडी कसरी भण्डारण गर्छौं। (`this.timerID`)

जबकि `this.prop` आफैं Reactद्वारा सेट अप गरिएको छ र` this.state` को एक विशेष अर्थ छ, यदि तपाईले डेटा प्रवाहमा भाग नलिएको कुरा भण्डारण गर्नुपर्छ भने तपाई classमा म्यानुअल तरीकाले थप फाईलहरू थप्न स्वतन्त्र हुनुहुन्छ (एक टाईमर आईडी जस्तै)।

हामी टाइमरलाई `componentWillUnmount()` लाइफसाइकल मेथडमा फाल्नेछौं

```js{2}
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
```

अन्तमा हामी `tick()` भनिने मेथड निर्माण गर्नेछौं ताकि `Clock` कम्पोनेन्ट प्रत्येक सेकेन्डमा चल्नेछ।

यसले कम्पोनेन्टको लोकल stateमा अपडेटहरू अनुसूची गर्न `this.setState()` प्रयोग गर्दछ

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

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/amqdNA?editors=0010)

अब प्रत्येक सेकेन्डमा घडी टिक्दछ।

चाँडै के हुँदैछ र कुन क्रममा मेथडहरू चल्नेछ भनेर पुन: संक्षेप गरौं

1) जब `<Clock />` लाई `ReactDOM.render()` मा पठाइन्छ, React ले `Clock` कम्पोनेन्टको कन्स्ट्रक्टरलाई कल गर्दछ। किनकि `<Clock />`मा वर्तमान समय प्रदर्शन गर्न आवश्यक छ, यसले `this.state` वर्तमान समय सहितको objectको साथमा आरम्भ गर्छ। हामी पछि यो state अपडेट गर्नेछौं।

2) React तब `Clock` कम्पोनेन्टको `render()` मेथड कल गर्दछ। Reactले स्क्रिनमा प्रदर्शन हुने कुरा यसरी सिक्छ। `Clock`को रेन्डर आउटपुटसँग मेल गर्न Reactले तब DOM अपडेट गर्दछ।

3) जब `Clock` आउटपुट DOM मा सम्मिलित हुन्छ, Reactले `componentDidMount()` लाइफसाइकल विधिलाई कल गर्दछ। यस भित्र `Clock` कम्पोनेन्टले सेकेन्डको एक पटक कम्पोनेन्टको `tick()` विधि कल गर्न ब्राउजरलाई टाइमर सेट अप गर्न सोध्दछ।

4) प्रत्येक सेकेन्ड ब्राउजरले `tick()` विधि कल गर्दछ। यसको भित्र `Clock` कम्पोनेन्टले हालको समय समावेश गरेको objectसँग `setState()` कल गरेर UI अपडेट अनुसूची गर्छ। यो `setState()` कलको कारण Reactलाई थाहा छ state परिवर्तन भएको छ र स्क्रिनमा के हुनुपर्दछ भनेर जान्न उसले फेरि `render()` विधिलाई कल गर्दछ। यस पटक `this.state.date`को `render()` विधि फरक हुनेछ र त्यसैले रेन्डर आउटपुटमा अपडेट गरिएको समय समावेश हुनेछ। React तदनुसार DOM अपडेट गर्दछ।

5) यदि `Clock` कम्पोनेन्ट कहिले पनि DOM बाट हटाइन्छ, Reactले `componentWillUnmount()` लाइफसाइकल विधि कल गर्दछ त्यसैले टाइमर रोकिन्छ।

## कसरी Stateको सही प्रयोग गर्ने {#using-state-correctly}

त्यहाँ तीनवटा कुरा छन् जुन तपाईले `setState()`को बारेमा जान्नुपर्दछ।

### Stateको सिधा परिमार्जन नगर्नुहोस् {#do-not-modify-state-directly}

उदाहरण को लागी, यसले कम्पोनेन्ट पुन रेंडर गर्दैन।

```js
// गलत
this.state.comment = 'Hello';
```

यसको सट्टा `setState()` प्रयोग गर्नुहोस्:

```js
// सही
this.setState({comment: 'Hello'});
```

The only place where you can assign `this.state` is the constructor.

### State Updates May Be Asynchronous {#state-updates-may-be-asynchronous}

React may batch multiple `setState()` calls into a single update for performance.

Because `this.props` and `this.state` may be updated asynchronously, you should not rely on their values for calculating the next state.

For example, this code may fail to update the counter:

```js
// गलत
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

To fix it, use a second form of `setState()` that accepts a function rather than an object. That function will receive the previous state as the first argument, and the props at the time the update is applied as the second argument:

```js
// सही
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

We used an [arrow function](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions) above, but it also works with regular functions:

```js
// सही
this.setState(function(state, props) {
  return {
    counter: state.counter + props.increment
  };
});
```

### State Updates are Merged {#state-updates-are-merged}

When you call `setState()`, React merges the object you provide into the current state.

For example, your state may contain several independent variables:

```js{4,5}
  constructor(props) {
    super(props);
    this.state = {
      posts: [],
      comments: []
    };
  }
```

Then you can update them independently with separate `setState()` calls:

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

The merging is shallow, so `this.setState({comments})` leaves `this.state.posts` intact, but completely replaces `this.state.comments`.

## The Data Flows Down {#the-data-flows-down}

Neither parent nor child components can know if a certain component is stateful or stateless, and they shouldn't care whether it is defined as a function or a class.

This is why state is often called local or encapsulated. It is not accessible to any component other than the one that owns and sets it.

A component may choose to pass its state down as props to its child components:

```js
<h2>It is {this.state.date.toLocaleTimeString()}.</h2>
```

This also works for user-defined components:

```js
<FormattedDate date={this.state.date} />
```

The `FormattedDate` component would receive the `date` in its props and wouldn't know whether it came from the `Clock`'s state, from the `Clock`'s props, or was typed by hand:

```js
function FormattedDate(props) {
  return <h2>It is {props.date.toLocaleTimeString()}.</h2>;
}
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/zKRqNB?editors=0010)

This is commonly called a "top-down" or "unidirectional" data flow. Any state is always owned by some specific component, and any data or UI derived from that state can only affect components "below" them in the tree.

If you imagine a component tree as a waterfall of props, each component's state is like an additional water source that joins it at an arbitrary point but also flows down.

To show that all components are truly isolated, we can create an `App` component that renders three `<Clock>`s:

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

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/vXdGmd?editors=0010)

Each `Clock` sets up its own timer and updates independently.

In React apps, whether a component is stateful or stateless is considered an implementation detail of the component that may change over time. You can use stateless components inside stateful components, and vice versa.
