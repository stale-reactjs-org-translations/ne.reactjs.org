---
id: lists-and-keys
title: Lists and Keys
permalink: docs/lists-and-keys.html
prev: conditional-rendering.html
next: forms.html
---

पहिले, javascript मा तपाईले List हरू कसरी रूपान्तरण गर्नुहुन्छ भनेर समीक्षा गरौं।

तलको कोडमा, हामी [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) method प्रयोग गर्छौं 'संख्याहरू' र तिनीहरूको मानहरू दोब्बर निकालना । हामी `map()` द्वारा फर्काइएको नयाँ array variable `डबल` मा असाइन गर्छौं र यसलाई लग गर्छौं:

```javascript{2}
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled);
```

यो कोडले कन्सोलमा `[2, 4, 6, 8, 10]` लग गर्छ।

React मा, array लाई [elements](/docs/rendering-elements.html) को listमा रूपान्तरण गर्नु लगभग समान छ।

### मल्टीपल componentहरु render गरने {#rendering-multiple-components}

तपाईंले ऐलिमेनटको सङ्ग्रह निर्माण गर्न सक्नुहुन्छ र [यसलाई JSX मा समावेश गर्नुहोस्](/docs/introducing-jsx.html#embedding-expressions-in-jsx) कर्ली ब्रेसेस `{}` प्रयोग गरेर।

तल, हामी JavaScript [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) method प्रयोग गरेर `numbers` array मार्फत लुप गर्छौं। । हामी प्रत्येक वस्तुको लागि `<li>` ऐलिमेन्ट फर्काउँछौं। अन्तमा, हामी ऐलिमेन्टहरूको परिणामस्वरूप array लाई `listItems` मा असाइन गर्छौं:

```javascript{2-4}
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);
```

हामी एक `<ul>` तत्व भित्र सम्पूर्ण `listItems` array समावेश गर्छौं, र [यसलाई DOM मा render गर्छौं](/docs/rendering-elements.html#rendering-an-element-into-the-dom):

```javascript{2}
ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/GjPyQr?editors=0011)

यो कोडले 1 र 5 बीचको नम्बरहरूको बुलेट list देखाउँछ।

### बेसिक लिस्ट component {#basic-list-component}

सामान्यतया तपाईंले [component](/docs/components-and-props.html) भित्र listहरू render गर्नुहुनेछ।

हामी अघिल्लो उदाहरणलाई componentमा refactor गर्न सक्छौं जसले `number` को array स्वीकार गर्छ र ऐलिमेन्टको list आउटपुट गर्छ।

```javascript{3-5,7,13}
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

जब तपाइँ यो कोड चलाउनुहुन्छ, तपाइँलाई एक चेतावनी दिइनेछ कि list वस्तुहरु को लागी एक key प्रदान गरिनु पर्छ। "key" एक विशेष स्ट्रिङ विशेषता हो जुन तपाईंले तत्वहरूको list सिर्जना गर्दा समावेश गर्न आवश्यक छ। हामी अर्को खण्डमा यो किन महत्त्वपूर्ण छ भनेर छलफल गर्नेछौं।

'numbers.map()' भित्र रहेका हाम्रा list वस्तुहरूमा `key` नियुक्त गरौं र missing key समस्या समाधान गरौं।

```javascript{4}
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/jrXYRR?editors=0011)

## Keys {#keys}

keyहरूले कुन वस्तुहरू परिवर्तन भएका छन्, थपिएका छन् वा हटाइएका छन् भनी थहापाउन् Reactलाई मद्दत गर्दछ। तत्वहरूलाई स्थिर पहिचान दिनको लागि एरे भित्रका तत्वहरूलाई keyहरू दिइनुपर्छ

```js{3}
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```


key छनोट गर्ने सबैभन्दा राम्रो तरिका भनेको येस्तो स्ट्रिङ प्रयोग गर्नु हो जसले आफ्ना siblingsहरू बीचको list वस्तुलाई अद्वितीय रूपमा पहिचान गर्छ। प्रायः तपाईले आफ्नो डाटाबाट आईडीहरू keyहरूको रूपमा प्रयोग गर्नुहुनेछ:

```js{2}
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```

जब तपाईंसँग रेन्डर गरिएका वस्तुहरूका लागि स्थिर आईडीहरू छैनन्, तपाईंले अन्तिम उपायको रूपमा वस्तु अनुक्रमणिकालाई keyको रूपमा प्रयोग गर्न सक्नुहुन्छ:

```js{2,3}
const todoItems = todos.map((todo, index) =>
  // Only do this if items have no stable IDs
  <li key={index}>
    {todo.text}
  </li>
);
```

यदि वस्तुहरूको क्रम परिवर्तन हुन सक्छ भने हामी keyहरूको लागि अनुक्रमणिका प्रयोग गर्न सिफारिस गर्दैनौं। यसले कार्यसम्पादनमा नकारात्मक असर पार्न सक्छ र component स्टेटसँग समस्या निम्त्याउन सक्छ। [keyको रूपमा सूचकांक प्रयोग गर्दा हुने नकारात्मक प्रभावहरूमा गहिरो व्याख्या](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-) को लागि रोबिन पोकोर्नीको लेख हेर्नुहोस्। pattern-e0349aece318)। यदि तपाईंले वस्तुहरू listमा स्पष्ट key तोक्न नदिने छनौट गर्नुभयो भने, प्रतिक्रिया keyहरूको रूपमा अनुक्रमणिका प्रयोग गर्न पूर्वनिर्धारित हुनेछ।

यदि तपाइँ थप सिक्न चाहनु हुन्छ भने यहाँ [keyहरू किन आवश्यक छ भन्ने बारे गहिरो व्याख्या](/docs/reconciliation.html#recursing-on-children) छ।

### keyहरूसँग अवयवहरू निकाल्दै {#extracting-components-with-keys}

keyहरूले वरपरको सरणीको सन्दर्भमा मात्र अर्थ दिन्छ।

For example, if you [extract](/docs/components-and-props.html#extracting-components) a `ListItem` component, you should keep the key on the `<ListItem />` elements in the array rather than on the `<li>` element in the `ListItem` itself.

उदाहरणका लागि, यदि तपाईँले एक `ListItem` component [extract](/docs/components-and-props.html#extracting-components) गरनुहुन्छ भने, तपाईँले `ListItem` मा रहेको `<li>` तत्वमा भन्दा एरे मा रहेको `<ListItem />` तत्वहरूमा key राख्नुपर्छ।

**उदाहरण: गलत key प्रयोग**

```javascript{4,5,14,15}
function ListItem(props) {
  const value = props.value;
  return (
    // Wrong! There is no need to specify the key here:
    <li key={value.toString()}>
      {value}
    </li>
  );
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Wrong! The key should have been specified here:
    <ListItem value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

**उदाहरण: सही key प्रयोग**

```javascript{2,3,9,10}
function ListItem(props) {
  // Correct! There is no need to specify the key here:
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Correct! Key should be specified inside the array.
    <ListItem key={number.toString()} value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/ZXeOGM?editors=0010)

A good rule of thumb is that elements inside the `map()` call need keys.

औंठाको राम्रो नियम भनेको  `map()` कल भित्रका तत्वहरूलाई keyहरू चाहिन्छ।

### keyहरू siblingsहरूमाझ मात्र अद्वितीय हुनुपर्छ {#keys-must-only-be-unique-among-siblings}

Keys used within arrays should be unique among their siblings. However they don't need to be globally unique. We can use the same keys when we produce two different arrays:

एरेहरु भित्र प्रयोग गरिएका keyहरू तिनीहरूका siblingsहरू बीच अद्वितीय हुनुपर्छ। यद्यपि तिनीहरू विश्वव्यापी रूपमा अद्वितीय हुन आवश्यक छैन। हामीले एउटै keyहरू प्रयोग गर्न सक्छौं जब हामी दुई फरक एरेहरू उत्पादन गर्छौं:

```js{2,5,11,12,19,21}
function Blog(props) {
  const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
  const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );
  return (
    <div>
      {sidebar}
      <hr />
      {content}
    </div>
  );
}

const posts = [
  {id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
  {id: 2, title: 'Installation', content: 'You can install React from npm.'}
];
ReactDOM.render(
  <Blog posts={posts} />,
  document.getElementById('root')
);
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/NRZYGN?editors=0010)

keyहरूले प्रतिक्रियाको लागि संकेतको रूपमा काम गर्दछ तर तिनीहरू तपाईंको componentहरूमा पास हुँदैनन्। यदि तपाइँलाई तपाइँको componentमा समान मान चाहिन्छ भने, यसलाई फरक नामको साथ प्रोपको रूपमा स्पष्ट रूपमा पास गर्नुहोस्:

```js{3,4}
const content = posts.map((post) =>
  <Post
    key={post.id}
    id={post.id}
    title={post.title} />
);
```

With the example above, the `Post` component can read `props.id`, but not `props.key`.

माथिको उदाहरणको साथ, `post` componentले `props.id` पढ्न सक्छ, तर `props.key` होइन।

### JSX मा map() इम्बेड गर्ने {#embedding-map-in-jsx}

माथिका उदाहरणहरूमा हामीले छुट्टै `listItems` चल घोषणा गर्यौं र JSX मा समावेश गर्यौं:

```js{3-6}
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

JSX ले अनुमति दिन्छ [कुनै पनि अभिव्यक्ति इम्बेड गर्ने](/docs/introducing-jsx.html#embedding-expressions-in-jsx) ताकि हामी `map()` परिणाम इनलाइन गर्न सक्छौं:

```js{5-8}
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
      )}
    </ul>
  );
}
```

[**CodePen मा प्रयास गर्नुहोस्**](https://codepen.io/gaearon/pen/BLvYrB?editors=0010)

कहिलेकाहीँ यसले स्पष्ट कोडमा परिणाम दिन्छ, तर यो शैली पनि दुरुपयोग हुन सक्छ। JavaScript मा जस्तै, यो तपाइँले निर्णय गर्न को लागी छ कि यो पढ्न योग्यता को लागी एक चर निकाल्न लायक छ कि छैन। ध्यान राख्नुहोस् कि यदि `map()` मुख्य भाग धेरै नेस्टेड छ भने, यो [एक घटक निकाल्न](/docs/components-and-props.html#extracting-components) को लागि राम्रो समय हुन सक्छ।
