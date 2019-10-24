---
id: tutorial
title: "ट्यूटोरियल: React को परिचय"
layout: tutorial
sectionid: tutorial
permalink: tutorial/tutorial.html
redirect_from:
  - "docs/tutorial.html"
  - "docs/why-react.html"
  - "docs/tutorial-ja-JP.html"
  - "docs/tutorial-ko-KR.html"
  - "docs/tutorial-zh-CN.html"
---

यो ट्यूटोरियलले React संग सम्बन्धित ज्ञान अवस्थित छ भन्ने मान्दैन। 

## ट्यूटोरियल सुरु गर्नु अघि {#before-we-start-the-tutorial}

ट्यूटोरियलको दौरानमा हामी सानो खेलको निर्माण गर्ने छौ। **सायद तपाई यसलाई पढ्न चाहनुहुन्न किनकी तपाइलाई खेलहरु निर्माण गर्नु छैन -- तर एक चोटी पढ्नुहोस।** तपाइले यो ट्यूटोरियलमा सिक्नुहुने तरिकाहरु जुनसुकै React apps बनाउन चाहिने आधारभूत कुराहरु हुन, र यो कुराहरुमा माहिर हुनु भयो भने तपाइले React गहनरुपमा बुझ्न सक्नु हुनेछ।

>सुझाव
>
>जो मानिसले **गरेर सिक्न** चाहान्छ यो ट्यूटोरियल उसको लागि बनाइएको हो। यदि तपाइ आधारभूत कुराहरु सिक्न चाहनुहुन्छ भने, यो [एकपछि अर्को मार्गदर्शक](/docs/hello-world.html) हेर्नुहोस। तपाइले यो ट्यूटोरियल र मार्गदर्शन एक अर्कामा परिपुरक भएको मान्न सक्नु हुन्छ। 

ट्यूटोरियल धेरै भागहरु मा विभाजित छ:

* [ट्यूटोरियलको लागि सेटअप गर्नुहोस्](#setup-for-the-tutorial) ले तपाइलाई ट्यूटोरियल पछ्याउन **सुरुवात बिन्दु** दिनेछ।
* [अवलोकन](#overview) ले तपाइलाई React कम्पोनेंट, props र state को आधारभूत कुरा सिकाउछ।
* [गेम पूरा गर्दै](#complexting-the-game) ले तपाइलाई React को विकासको लागि **एकदमै साधारण तरिकाहरु** सिकाउछ।
* [समय यात्रा थप्दै](#adding-time-travel) ले तपाइलाई React को अलग बलियो पक्षहरुको **गहिरो दृष्टि** दिन्छ।

यो ट्यूटोरियलबाट लाभ पाउन तपाइले सबै खण्ड एकै चोटी पुरा गर्नु पर्छ भन्ने छैन। तपाइले सक्ने जति प्रयास गर्नु होला -- एउटा अथवा दुइटा खण्डहरु भए पनि पुरा गर्नुहोस। 

### हामी के निर्माण गर्दैछौं? {#what-are-we-building}

यो ट्यूटोरियलमा, हामी कसरी React बाट एक पारस्परिक tic-tac-toe खेल बनाउने भनेर देखाउनेछौं।

हामी यहाँ के बनाउन गइरहेको छौ तेस्को **[अन्तिम परिणाम](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)** तपाई देख्न सक्नु हुन्छ। यदि तपाई कोड बुझ्न सक्नु हुन्न भने, अथवा यदि तपाई कोड को स्य्न्तक्ष संग अपरचित हुनु हुन्छ भने पनि न आतिनुहोस! यो ट्युटोरियलको अन्तिम लक्ष्य भनेको तपाइलाई React र यसको syntax बुझ्न मदत पुराउनु हो।

यो ट्यूटोरियल सुरु गर्नु भन्दा पहिले तपाई tic-tac-toe खेल खेलेर हेर्न हामी सुझाब दिन्छौ। तपाइले विचार गर्न सक्नु हुन्छ खेलको सुविधाहरु मध्ये एउटा चाही, खेल बोर्डको दायाँमा अंकहरुको सुची छ। यो सुचीले तपाइले  खेलमा चालेको  पहिलेको  चालहरुको  रेकर्ड दिन्छ, र यो सुची खेलको प्रगतिसंगै अद्यावधिक हुन्छ। 

तपाईं एक पटक  परिचित भएपछि  tic-tac-toe खेल बन्द गर्न सक्नुहुन्छ। हामी यो ट्यूटोरियलमा एक सरल template बाट सुरू गर्नेछौ। हाम्रो अर्को चरण तपाईंलाई सेटअप गर्नु हो ताकि तपाईं खेल निर्माण गर्न सक्नुहुनेछ।

### आवश्यकताहरु {#prerequisites}

हामी मान्दछौं कि तपाईंलाई  HTML  र  Javascript  बारे  केहि थाहा छ , तर तपाईं एक फरक Programming  भाषाबाट आउँदै हुनुहुन्छ भनेपनि  तपाई पछ्याउन सक्षम हुनुपर्दछ। हामी यो पनि मान्दछौं कि तपाइँ Programming  अवधारणाहरू जस्तै functions, objects, arrays, र कम हदसम्म भए पनि classes सँग परिचित हुनुहुन्छ।

यदि तपाइलाई Javascript पढ्नु पर्ने छ भने, हामी [यो मार्गदर्शक](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript) पढ्न सुझाब दिन्छौ। नोट गर्नुहोस कि हामी ES6 को सुविधाहरु प्रयोग गर्ने छौ -- जुन भर्खरै आएको Javascript को version हो। यो ट्यूटोरियलमा, हामी [arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions), [classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes), [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let), र [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) statements प्रयोग गर्छौ। तपाई ES6 कोड कसरि compile हुन्छ भनेर हेर्न चाहनुहुन्छ भने  [Babel REPL](babel://es5-syntax-example) प्रयोग गर्न सक्नु हुन्छ। 

## ट्यूटोरियलको लागि सेटअप गर्नुहोस् {#setup-for-the-tutorial}

यस ट्यूटोरियल पूरा गर्ने दुई तरिकाहरू छन्: तपाईले तपाइँको ब्राउजरमा कोड लेख्न सक्नुहुन्छ, वा तपाइँ आफ्नो कम्प्यूटरमा डेभलपमेन्ट वातावरण बनाउन सक्नुहुनेछ।

### विकल्प १ सेटअप गर्नुहोस्: ब्राउजरमा कोड लेख्नुहोस् {#setup-option-1-write-code-in-the-browser}

यो सुरू गर्न सबैभन्दा छिटो तरिका हो!

पहिलो, यो **[स्टार्टर कोड](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)** नयाँ ट्याबमा खोल्नुहोस्। नयाँ ट्याबले खाली tic-tac-toe खेल बोर्ड र React कोड प्रदर्शन गर्नुपर्छ। हामी यस ट्यूटोरियलमा React कोड सम्पादन गर्नेछौं।

अब तपाइँ दोस्रो सेटअप विकल्प छोड्न सक्नुहुन्छ, र React को [अवलोकन](#overview) प्राप्त गर्न अवलोकन सेक्शनमा जानुहोस्।

### विकल्प २ सेटअप गर्नुहोस्: कम्प्यूटरमा डेभलपमेन्ट वातावरण {#setup-option-2-local-development-environment}

यो पुरा तरिकाले वैकल्पिक छ र यो ट्यूटोरियलको लागि आवश्यक छैन!

<br>

<details>

<summary><b>वैकल्पिक: कम्प्युटरमा तपाइलाई मन पर्ने  इडिटर  प्रयोग गरेर निर्देशनहरू पछयाउनुहोस्</b></summary>

यो सेटअपलाई थप कार्य चाहिन्छ तर तपाई आफ्नो रोजाईको एडिटर प्रयोग गरेर ट्यूटोरियल पुरा गर्न सक्नु हुन्छ। यहाँ पछ्याउन पर्ने चरणहरू छन्: 

1. सुनिश्चित गर्नुहोस् कि तपाईंको हालको संस्करण [Node.js](https://nodejs.org/en/) इन्स्टल छ।
2. Create React App बाट नयाँ प्रोजेक्ट बनाउन [installation  निर्देशहरू](/docs/create-a-new-react-app.html#create-react-app) पछ्याउनुहोस्।

```bash
npx create-react-app my-app
```

3. नयाँ प्रोजेक्टको `src/` फोल्डरमा भएको सबै फाइलहरू मेटाउनुहोस्

> नोट:
>
>**सम्पूर्ण `src` फोल्डर नमेटाउनुहोस्, भित्र भित्रको मूल स्रोत फाइलहरू मात्र।** हामी अर्को चरणमा यस प्रोजेक्टको लागि उदाहरणहरूको साथ पहिलेको स्रोत फाइलहरूको  ठाउमा राख्नेछौ।
```bash
cd my-app
cd src

# यदि तपाईं Mac वा Linux प्रयोग गर्दै हुनुहुन्छ भने:
rm -f *

# वा, यदि तपाइँ windows मा हुनुहुन्छ भने:
del *

# त्यसपछि, प्रोजेक्ट फोल्डरमा फर्कनुहोस्
cd ..
```

4. यो [CSS कोडको](https://codepen.io/gaearon/pen/oWWQNa?editors=0100) साथ `src /` फोल्डरभित्र  `index.css` नामकरण गरिएको फाईल थप्नुहोस्।

5. यो [JS कोडको](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)  साथ `src /` फोल्डरमा 'index.js` नामकरण गरिएको फाइल थप्नुहोस्।.

6. `Src /` फोल्डरमा `index.js` को शीर्षमा यी तीन लाइन कोड थप्नुहोस्:

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
```

अब यदि तपाईंले प्रोजेक्ट फोल्डरमा `npm start ` रन गर्नुहुन्छ  र ब्राउजरमा `http://localhost:3000` खोल्नुहोस्, तपाईंले खाली tic-tac-toe फिल्डलाई हेर्नु पर्दछ।

हामी तपाइको सम्पादकको लागि syntax hightlighting मिलाउनको लागि [यी निर्देशनहरू](https://babeljs.io/docs/editors/) पछ्याउन सुझाब दिन्छौ। 

</details>

### गाह्रो पर्यो, मलाई सहयोग गर्नुहोस! {#help-im-stuck}

यदि तपाईं अड्कनुभयो भने, [समुदाय समर्थन स्रोतहरू](/community/support.html) हेर्नुहोस्। विशेष गरी, [Reactiflux Chat](https://discord.gg/0ZcbPKXt5bZjGY5n) मद्दत छिटो प्राप्त गर्न एक राम्रो तरिका हो। यदि तपाईंले जवाफ प्राप्त गर्नुभएन भने, वा तपाईं अड्कनु भएको छ भने, कृपया एउटा issue  फाइल गर्नुहोस्, र हामी तपाईंलाई मद्दत गर्नेछौं।

## अवलोकन {#overview}

अब तपाईं सेट अप गर्दै हुनुहुन्छ, React को अबलोकन पाउनुहोस!

### React भनेको के हो? {#what-is-react}

React एक व्याख्यात्मक, कुशल, र प्रयोगकर्ता इन्टरफेस निर्माण गर्न बनेको Javascript लाइब्रेरी हो। यसले तपाईँलाई जटिल प्रयोगकर्ता इन्टरफेसहरु रचना गर्न सानो र अलग टुक्रा टुक्राहरूबाट बनेको कोडबाट मदत गर्छ जसलाई हामी "components" भन्छौ।

React मा धेरै प्रकारका components हरु हुन्छन, तर हामी `React.Component` subclasses हरु बाट सुरुवात गर्नेछौ। 

```javascript
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// उदाहरण उपयोग: <ShoppingList name="Mark" />
```

हामी चाँडै रमाइलो  XML जस्तो ट्यागहरू प्राप्त गर्नेछौं। हामी स्क्रीनमा के हेर्न चाहन्छौं भन्ने कुरा बताउन हामी React components  प्रयोग गर्दछौं। जब हाम्रो डेटा परिवर्तन हुन्छ, React ले  हाम्रो component हरुलाई  कुशलतापूर्वक अपडेट र पुन: प्रस्तुत गर्नेछ।

यहाँ, ShoppingList **React component class**, वा **React component type** हो।  Component ले parameters लिन्छ, जसलाई हामी `props` भन्छौ ("properties" को छोटकरी रुप), र `render` method मार्फत देखाउन views क्रमानुसार फ़र्काउछ। 

`render` method ले स्क्रीनमा हेर्न चाहानु भएको एक *विवरण* लाई फर्काउँछ। React ले विवरण लिन्छ र परिणाम प्रदर्शन गर्दछ। विशेष गरी, `render` ले  **React element** फर्काउँछ, जो render  गर्न को लागि हल्का विवरण हो। सबै भन्दा बढी React बिकाशकर्ताहरुले  "JSX" नामक एक विशेष सिन्ट्याक्स प्रयोग गर्दछन जसले कोडको  संरचनाहरू लेख्न सजिलो बनाउँछ। निर्माणको समयमा `<div />` syntax `React.createElement ('div')` को रूपमा बदलिन्छ। माथिको उदाहरण यो जस्तै छ:

```javascript
return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
```

[पूर्ण विस्तारित संस्करण हेर्नुहोस्।](babel://tutorial-expanded-version)

यदि तपाइँ उत्सुक हुनुहुन्छ भने, `createElement ()` को बारेमा थप विवरण [API reference](/docs/react-api.html#createelement) मा वर्णन गरिएको छ, तर हामी यसलाई यो ट्यूटोरियलमा प्रयोग गर्दैनौं। बरु, हामी JSX प्रयोग गरिरहनेछौं।

JSX ले Javascript लाई शक्तिशाली बनाउछ। तपाईले कुनै Javascript expressions मझौला कोस्टभित्र रहने JSX भित्र राख्न सक्नुहुन्छ। प्रत्येक React element Javascript object  हो जुन तपाईं variable मा राख्न सक्नुहुन्छ वा तपाईंको program वरिपरि राख्न सक्नुहुन्छ।

माथिको `ShoppingList` component ले निर्मित DOM components जस्तै `<div />` र `<li />` लाई render गर्दछ। तर तपाईले आफ्नै React components पनि रचना गरेर render गर्न सक्नुहुन्छ। उदाहरणको लागि, हामी अब सबै shopping list लाई `<ShoppingList  />` लेखेर जनाउन सक्छौ। प्रत्येक React component गुप्त छ र छुट्टै पनि चलाउन मिल्छ; यसले तपाईंलाई साधारण component हरु बाट जटिल युजर इन्टरफेसहरु निर्माण गर्न दिन्छ।

## सुरुवातको कोड निरीक्षण गर्दा {#inspecting-the-starter-code}

यदि तपाईं ट्यूटोरियल **तपाईको ब्राउजरमा** मा काम गर्न जाँदै हुनुहुन्छ भने  यो कोड नयाँ ट्याबमा खोल्नुहोस्: **[सुरुवाती कोड](https://codepen.io/gaearon/pen/oWWQNa?editors=0010 )**। यदि तपाइँ ट्यूटोरियलमा **locally** काम गर्न जाँदै हुनुहुन्छ भने, यसको सट्टामा आफ्नो project फोल्डरमा `src/index.js` खोल्नुहोस (तपाईंले यो फाइल सेटअप [setup](#setup-option-2-local-development-environment) को बेलामा हेरी सक्नु भएको छ)।

यो सुरुवाती कोड हामीले निर्माण गर्न लागेको खेलको आधार हो। हामीले CSS स्टाइल तपाइलाई प्रदान गर्यौं ताकि तपाईलाई  tic-tac-toe खेलको React र programming सिक्नको लागि ध्यान केन्द्रित गर्न आवश्यक छ।

कोड निरीक्षण गरेर, तपाईलाई थाहा छ कि हामीसँग तीन React components छन्:

* Square
* Board
* Game

Square component ले  एउटा `<button>` render गर्छ र Board component ले ९ वटा वर्ग render गर्छ। Game Component ले  प्लेसहोल्डर मानहरूको साथ बोर्ड render गर्दछ जुन हामी पछि परिमार्जन गर्नेछौं। हाल कुनै अन्तरक्रियात्मक components छैनन्।

### Props बाट डाटा पठाउनुहोस {#passing-data-through-props}

सुरुवात गर्नको लागि, कृपया केहि डाटा हाम्रो Board Component  बाट Square component मा पठाउन प्रयास गर्नुहोस। 

Board component को  `renderSquare` method मा, `value` prop Square component मा पास गर्न कोड परिवर्तन गर्नुहोस्:

```js{3}
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
```

value prop देखाउनको लागि Square को `render` method को `{/* TODO */}` लाई हटाएर `{this.props.value}` ले परिबर्तन गर्नुहोस। 

```js{5}
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```

पहिले:

![React Devtools](../images/tutorial/tictac-empty.png)

पछि: तपाईंले rendered आउटपुटमा प्रत्येक वर्गमा नम्बर देख्नुपर्छ।

![React Devtools](../images/tutorial/tictac-numbers.png)

**[यो बिन्दुमा पूर्ण कोड हेर्नुहोस्](https://codepen.io/gaearon/pen/aWWQOG?editors=0010)**

बधाई छ! तपाईले केवल अभिभावक Board component बाट बाल Square component मा  "prop पठाउनुभयो"। props पठाउनु भनेको React apps मा अभिभावक component बाट बाल component मा जानकारी कसरि जान्छ भन्ने जनाउछ।

### एक अन्तरक्रियात्मक Component बनाउदै {#making-an-interactive-component}

जब हामी Square component क्लीक गर्छौ तब एस्लाई "X" ले परिबर्तन गरौ। 
पहिले, button ट्याग परिवर्तन गर्नुहोस् जुन Square component को  `render()` function बाट फर्काइएको छ:

```javascript{4}
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={function() { alert('click'); }}>
        {this.props.value}
      </button>
    );
  }
}
```

यदि तपाइँ अहिले एक Square component मा क्लिक गर्नुहुन्छ भने, तपाइँले तपाइँको ब्राउजरमा अलर्ट देख्नुपर्दछ।

>नोट
>
>टाइपिङ सुरक्षित गर्न र यो [`this` को भ्रामक व्यवहार](https://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/)बाट जोगिन, हामी [arrow function syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) event handlers को लागि यहाँ र तल प्रयोग गर्छौ:
>
>```javascript{4}
>class Square extends React.Component {
>  render() {
>    return (
>      <button className="square" onClick={() => alert('click')}>
>        {this.props.value}
>      </button>
>    );
>  }
>}
>```
>
>
>याद गर्नुहोस `onClick={() => alert('click')}`, हामीले कसरि *एउटा function* `onClick` लाई props को रुपमा पठाई राखेका छौ। React ले click गरेपछि मात्रै यो function लाई कल गर्छ। `() =>` लाई बिर्सेर `onClick={alert('click')}` लेख्नु साधारण गल्ति हो, र जसले गर्दा component re-render हुने बित्तिकै जहिले पनि अलर्ट कल हुन्छ।

अर्को चरणको रूपमा, हामी Square component क्लिक भएको छ भनी "सम्झाउन" चाहन्छौ, र यसलाई "X" चिन्हले भरिनेछ। त्यो चिजहरु "सम्झनको" लागि, component हरुले state को  प्रयोग गर्छन्।

React components हरुको constructors मा `this.state` लाई सेटिङ गरेपछि state बन्छ।  `this.state` लाई React component को निजी state को रुपमा विचार गर्नु पर्छ जुन उक्त component मा परिभाषित गरिएको हुन्छ। अब Square को हालको मान `this.state` मा भण्डार गरौ, अनि जब Square क्लिक भएपछि परिबर्तन गरौ। 

सर्बप्रथम, state प्रारम्भ गर्न हामीले class मा constructor थप्नेछौ:

```javascript{2-7}
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button className="square" onClick={() => alert('click')}>
        {this.props.value}
      </button>
    );
  }
}
```

>नोट
>
>[JavaScript class](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)हरुमा, तपाइले जहिले पनि `super` कल गर्नु पर्छ जब तपाइले subclass मा constructor परिभाषित गर्नु हुन्छ। सबै React component classes संग भएको `constructor` मा `super(props)` कल बाट सुरुवात हुन्छ। 

अब हामी क्लिक गरेको बेलाको state को प्रदर्शन गर्न Square को `render` मेथोड़ परिबर्तन गर्छौ:

* `this.props.value` लाई `<button>` ट्याग भित्र `this.state.value` ले बदल्नुहोस्।
* `OnClick = {...}` event handler लाई `onClick = {() => this.setState ({value: 'X'}}}` ले बदल्नुहोस्।
* कोड राम्रो देखाउनको लागि अलग-अलग लाइनहरूमा `className` र `onClick` प्रोप्स राख्नुहोस्।

यी परिवर्तनहरू पछि, Square को  `render` मेथोडबाट फर्काइएको `<button>` ट्याग यो जस्तो देखिन्छ:

```javascript{12-13,15}
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button
        className="square"
        onClick={() => this.setState({value: 'X'})}
      >
        {this.state.value}
      </button>
    );
  }
}
```

Square को `render` मेथोड मा `onClick` handler बाट `this.setState` कल गरेर, जब `<button>` क्लिक हुन्छ, हामीले React मा त्यो Square लाई पुन:render गर्न भनेका हौ। अद्यावधिक पछि, Square को  `this.state.value` को मान `'X'` हुनेछ, त्यसैले हामी गेम बोर्डमा `X` देख्नेछौं। यदि तपाइँ कुनै पनि Square मा क्लिक गर्नुहुन्छ भने, `X` देख्नु पर्दछ।

जब तपाइँ एक component मा `setState` कल गर्नुहुन्छ, React ले स्वचालित रूपमा यसको भित्रको बच्चा component हरु  पुनः अपडेट पनि गर्छ।

**[यो बिन्दुमा पूर्ण कोड हेर्नुहोस्](https://codepen.io/gaearon/pen/VbbVLg?editors=0010)**

### विकासकर्ता उपकरणहरू {#developer-tools}

[Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) र [Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)को लागि React Devtools एक्सटेन्सनले तपाईंलाई आफ्नो ब्राउजरको विकासकर्ता उपकरणको साथ एक React component  tree को  निरीक्षण गर्न दिन्छ।

<img src="../images/tutorial/devtools.png" alt="React Devtools" style="max-width: 100%">

React DevTools ले तपाईंलाई props र तपाईंको React components को  अवस्था जाँच गर्न दिन्छ।

React  DevTools स्थापना पछि, तपाईं पृष्ठको कुनैपनि भागमा दायाँ क्लिक गर्न सक्नुहुन्छ, विकासकर्ता उपकरण खोल्नका लागि "inspect" मा क्लिक गर्नुहोस्, र React ट्याबहरू ("⚛️ Components" र "⚛️ Profiler") अन्तिम ट्याबको रूपमा दायाँतिर देखा पर्नेछ। Component रूख निरीक्षण गर्न "⚛️ Components" क्लिक गर्नुहोस्।.

**तथापि, नोट CodePen सँग काम गर्न केही थप चरणहरू छन्:**

1. Login वा दर्ता गर्नुहोस् र तपाईंको इमेलको पुष्टि गर्नुहोस् (स्प्याम रोक्न आवश्यक छ)।
2. "Fork" बटन क्लिक गर्नुहोस्।
3. "Change View" क्लिक गर्नुहोस् र त्यसपछि "Debug mode" चयन गर्नुहोस्।
4. नयाँ ट्याबमा खोलिएको हुन्छ, devtools सँग अहिले एउटा React ट्याब सक्रिय हुनुपर्छ।

## गेम पूरा गर्दै {#completing-the-game}

अहिले हामीसँग हाम्रो tic-tac-toe खेलको आधारभूत आधारभूत ब्लकहरू छन्। एक पूर्ण खेल गर्न को लागि, हामी अब "X" र "0" लाई एकपछि अर्को देखाउनको लागि, र हामीलाई एक विजेता को निर्धारण गर्ने तरीका चाहिएको छ।

### state लाई माथि लैजादा {#lifting-state-up}

हाल, प्रत्येक Square component ले खेलको state लाई राख्दछ। विजेता जाँच गर्नको लागि, हामी प्रत्येक 9 वर्गहरुको को मान एक स्थानमा राख्दछौं। 

हामी सोच्न सक्छौं कि Board ले प्रत्येक Square लाई Square को state को लागि सोध्नुपर्दछ। यद्यपि यो दृष्टिकोण React मा सम्भव छ, हामी एस्तो नगर्न सल्लाह गर्छौं किनभने कोड बुझ्न गाह्रो हुन्छ, बगहरू आउने सम्भावना हुन्छ, र रिफैक्टर गर्न गाह्रो हुन्छ। बरु, सबै भन्दा राम्रो तरीका प्रत्येक Square को सट्टामा अभिभाबक Board component मा खेलको state भण्डारण गर्नु हो। Board component ले प्रत्येक Square लाई prop पास गरेर कुन मान प्रदर्शन गर्ने भन्न सक्छ, [जस्तै हामी जतिबेला हामीले प्रत्येक Square मा एक अंक पठायौ](#passing-data-through-props)।

**धेरै बच्चा component हरु बाट डाटा जम्मा गर्न, वा दुई बच्चा component हरू एकआपसमा कुराकानी गर्न, छुट्टा छुट्टै राख्नुभन्दा तपाइँलाई साझा state उनीहरूको अभिभावकको  भागमा राख्न आवश्यक छ। अभिभावक component ले props प्रयोग गरी बच्चाहरुलाई state फिर्ता गर्न सक्दछ; यसले बच्चाहरूलाई एकअर्कासँग र अभिभावक component सँग सिङ्कमा राख्छ।**

जब React component हरु सुधार्नुपर्छ अभिभावक component मा state सार्नु सामान्य हो - यो मौकाको फाइदा उठाउदै यसलाई  प्रयास गरौ।

Board मा एउटा constructor थप्नुहोस् र Board को सुरुवाती state सेट गर्नुहोस् जसमा ९ सून्य मानको array ९ बर्गहरु संग सम्बन्धित हुन्छ:

```javascript{2-7}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
    };
  }

  renderSquare(i) {
    return <Square value={i} />;
  }
```

जब हामीले पछि बोर्ड भर्छौं, `this.state.squares` array यो जस्तै केहि हुन्छ:

```javascript
[
  'O', null, 'X',
  'X', 'X', 'O',
  'O', null, null,
]
```

Board को `renderSquare` मेथोड हाल यो जस्तो देखिन्छ:

```javascript
  renderSquare(i) {
    return <Square value={i} />;
  }
```

सुरुमा, हामीले Board बाट हरेक स्क्वायरमा 0 देखि 8 सम्मको नम्बर देखाउनलाई [`value` prop तल पठायौ](#passing-data-through-props)। फरक अघिल्लो चरणमा, हामीले [Square को आफ्नै state निर्धारण गरिएको](#making-an-interactive-component) संख्याहरू "X" चिन्हसँग प्रतिस्थापित गर्यो। यसैले स्क्वायरले Board द्वारा पास गरिएको `value` propलाई बेवास्ता गर्छ।

हामी फेरी अब prop पठाउने तरिका प्रयोग गर्नेछौं। हामी प्रत्येक Square को वर्तमान मान(`'X'`,`' O'`, वा `null`) को बारेमा निर्देशित गर्न Board लाई परिबर्तन गर्नेछौ। हामीले Board को  constructorमा `squares` array परिभाषित गरिसकेका छौ, र हामी यसलाई पढ्नको लागि Board को `renderSquare` मेठोड परिमार्जन गर्नेछौं:

```javascript{2}
  renderSquare(i) {
    return <Square value={this.state.squares[i]} />;
  }
```

**[यो बिन्दुमा पूर्ण कोड हेर्नुहोस्](https://codepen.io/gaearon/pen/gWWQPY?editors=0010)**

प्रत्येक Square ले अब एक `value` prop प्राप्त गर्छ जुन रिक्त वर्गहरूको लागि कि `'X'`, `'O'` वा `null` हुनेछ।

अर्को, हामी Squareमा क्लिक गर्दा के हुन्छ भनेर परिवर्तन गर्न आवश्यक छ। Board componentले अब कुन वर्गहरू भरिएको छ थाहा पाउछ। हामी Boardको state Square मार्फत अद्यावधिक गर्ने तरिका सिर्जना गर्न आवश्यक छ।  component मा परिभाषित गरेको state यसको  निजी हुन्छ, हामीले Boardको state Squareबाट सीधा अपडेट गर्न सक्दैनौं।

यसको सट्टा, हामी Boardबाट Squareमा एक functionलाई तल पठाउनेछौं, र जब स्क्वायरमा क्लिक गरिन्छ हामी Square बाट function कल गर्नेछौ। हामी `renderSquare` मेथोडलाई बोर्डमा परिवर्तन गर्नेछौं:

```javascript{5}
  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }
```

>नोट
>
>
हामीले पढ्न सजिलो बनाउनको लागि returned element लाई धेरै लाइनहरुमा कोड बिभाजन गर्दछौ, र parentheses थप्छौ  जसले गर्दा Javascript ले `return` पछि semicolon थप्दैन र कोड बिग्रिदैन। 

अब हामी दुई ओटा props Board बाट Square मा  पठाउछौ: `value` र `onClick`। `OnClick` prop एक function हो जुन क्लिक गर्दा क्लिक गरिएको Squareले कल गर्न सक्छ। हामी निम्न परिवर्तनहरू Squareमा बनाउनेछौं:

* `this.state.value` लाई Square को `render` method मा `this.props.value` ले बदल्नुहोस्
* `this.setState()` लाई Square को `render` method मा `this.props.onClick()` ले बदल्नुहोस्
* Square बाट `constructor` मेटाउनुहोस् किनकि Square ले खेलको state लाई नियन्त्रण गर्दैन

यी परिवर्तन पछि, Square component यस्तो देखिन्छ:

```javascript{1,2,6,8}
class Square extends React.Component {
  render() {
    return (
      <button
        className="square"
        onClick={() => this.props.onClick()}
      >
        {this.props.value}
      </button>
    );
  }
}
```

जब एक Square क्लिक गरिन्छ, बोर्ड द्वारा प्रदान गरिएको `onClick` function कल हुन्छ। यहाँ यो कसरी हासिल भएको छ यसको समीक्षा:

1. निर्मित DOM `<button>` मा  भएको `OnClick` prop लाई component ले React लाइ क्लिक event listener सेट अप गर्न को लागी भन्छ।
2. जब बटन क्लिक गरिन्छ, React ले `onClick` event handler लाई कल गर्नेछ जुन Square को `render()` method मा परिभाषित गरिएको छ।
3. यो event handler ले `this.props.onClick()` लाई कल गर्दछ। Square को  `onclick` prop लाई Board द्वारा निर्दिष्ट गरिएको थियो।
4. बोर्डले `onClick = {() => this.handleClick (i)}` लाई Square मा पठायो, Square क्लिक गरे पछि`this.handleClick (i)` लाई कल गर्छ।
5. हामीले अझै `handleClick()` method परिभाषित गरेको छैनौ, त्यसैले हाम्रो कोड बिग्रिन्छ। यदि तपाइँ अहिले एउटा Square मा क्लिक गर्नुहुन्छ भने, तपाईंले रातो त्रुटि भएको एस्तो खालको स्क्रीन देख्नु पर्दछ "this.handleClick is not a function"।

>नोट
>
>DOM `<button>` element को `onClick` attribute सँग React को लागि एक विशेष अर्थ छ किनकि यो एक निर्मित component हो। Square जस्तै आफैले बनाउने  component हरूको लागि, नामकरण तपाईंले नै गर्न सक्नु हुन्छ। हामी Square को `onClick` prop वा Board को `handleClick` method को लागि जुनसुकै नाम दिन सक्दछौं, र कोडले पहिले जस्तै काम गर्नेछ। React मा, `on[Event]` नाम prop को लागी नाम राख्ने चलन छ जुन event हरु को प्रतिनिधित्व गर्दछ र `handle[Event]` method event हरु को सम्हाल्नको लागी को प्रयोग हुन्छ।

जब हामी Square मा क्लिक गर्न प्रयास गर्छौं, हामीले एउटा त्रुटि पाउनुपर्छ किनभने हामीले `handleClick` परिभाषित गरेको छैनौ। हामी अब Board class मा `handleClick` थप्छौ:

```javascript{9-13}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = 'X';
    this.setState({squares: squares});
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = 'Next player: X';

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

**[यो बिन्दुमा पूर्ण कोड हेर्नुहोस्](https://codepen.io/gaearon/pen/ybbQJX?editors=0010)**

यी परिवर्तनहरू पछि, हामी पुन: भित्री Square हरूमा क्लिक गरेर मान भर्नको लागि सक्षम भयौ, हामी संग पहिले पनि यस्तै थियो। तथापि, अब state व्यक्तिगत Square component हरुको सट्टा Board component मा भण्डारमा भण्डारण गरिएको छ। जब बोर्डको state परिवर्तन हुन्छ, Square को state स्वचालित रूपमा पुन: render गर्दछ। Board component मा सबै वर्गहरूको state राख्नाले भविष्यमा विजेता निर्धारण गर्न सजिलो हुन्छ।

Square component हरूले अब state लाई सुरक्षित राख्दैन किनकि, Square component ले Board component बाट मानहरू प्राप्त गर्दछ र Square हरू क्लिक गर्नुहुँदा बोर्डलाई सूचित गर्दछ। React को चलनचल्तीमा, Square component हरू अहिले **controlled components** हुन। Board मा उनीहरूको पूर्ण नियन्त्रण छ।

नोट गर्नुहोस् कि `handleClick` मा, हामी अवस्थित array परिमार्जन गर्न को सट्टा `squares` array को प्रतिलिपि सिर्जना गर्न `.slice()` लाई कल गर्दछौ। `squares` array को प्रतिलिपि हामी किन बनाउँछौं भनेर अर्को खण्डमा वर्णन गर्नेछौं।

### किन Immutability महत्त्वपूर्ण छ {#why-immutability-is-important}

अघिल्लो कोड उदाहरणमा, हामीले सुझाव दिएको छ कि तपाइँ  array लाई  परिमार्जन गर्नको लागि अवस्थित array परिबर्तन गर्नुको सट्टा  `.slice()` अपरेटर को उपयोग गरेर `squares` array को एक प्रतिलिपि निर्माण गर्न सक्नु हुन्छ। हामी अहिले immutability को बारेमा र किन immutability सिक्न महत्त्वपूर्ण छ भन्ने बारेमा छलफल गर्नेछौं।

सामान्यतया data परिवर्तन गर्न दुईवटा दृष्टिकोणहरू छन्। पहिलो दृष्टिकोण data को मानहरू परिवर्तन गरेर data *mutate* गर्नु हो। दोस्रो दृष्टिकोणले नयाँ प्रतिलिपिको साथ data लाई इच्छित रुपमा परिवर्तन गर्नु हो।

#### Mutation गरेर Data परिबर्तन  {#data-change-with-mutation}
```javascript
var player = {score: 1, name: 'Jeff'};
player.score = 2;
// Now player is {score: 2, name: 'Jeff'}
```

#### Mutation बिना data परिबर्तन {#data-change-without-mutation}
```javascript
var player = {score: 1, name: 'Jeff'};

var newPlayer = Object.assign({}, player, {score: 2});
// Now player is unchanged, but newPlayer is {score: 2, name: 'Jeff'}

// Or if you are using object spread syntax proposal, you can write:
// var newPlayer = {...player, score: 2};
```
अन्त परिणाम एकै हो तर mutate नगरेर (या अन्तर्निहित data परिवर्तन गरेर) सीधा, हामी तल वर्णन गरिएका धेरै फाइदाहरू प्राप्त गर्छौं।

#### जटिल सुविधाहरू सरल बनाउनुहोस् {#complex-features-become-simple}

Immutability ले जटिल सुविधाहरू लागू गर्न सजिलो बनाउँछ। पछि यो ट्यूटोरियलमा, हामी "समय यात्रा" सुविधा लागू गर्नेछौं जसले हामीलाई tic-tac-toe मा खेलको इतिहास समीक्षा गर्न र अघिल्लो चालहरूमा "फिर्ता जान" लाई अनुमति दिन्छ। यो कार्यक्षमता खेलहरूको लागि विशेष होइन - केही कार्यहरू पूर्ववत गर्न र केहि कार्यहरू पुन: प्रयास गर्ने क्षमताहरू अनुप्रयोगहरूमा एक सामान्य आवश्यकता हो। प्रत्यक्ष data mutation बाट जोगाउन हामीलाई खेलको इतिहासको अघिल्लो संस्करणहरू सहि राख्न सक्दछ, र पछि तिनीहरूलाई पुन: प्रयोग गर्न दिन्छ।

#### परिवर्तन पत्ता लगाउँदै {#detecting-changes}

mutable object हरूमा परिवर्तन पत्ता लगाउन गाह्रो हुन्छ किनभने तिनीहरू सीधा परिमार्जित गरिन्छ। यो पत्ता लगाउन को लागी mutable object को आफु को पछिल्लो प्रतिलिपि  र सम्पूर्ण object tree उल्टो रुपमा तुलना को आवश्यकता पर्छ।

Immutable object हरूमा भएको परिवर्तन पत्ता लगाउन एकदम सजिलो छ। यदि उल्लिखित immutable object अघिल्लो object भन्दा फरक छ भने, तेस्तो भएमा object परिवर्तन भएको छ।

#### React मा Re-Render गर्ने कहिले निर्धारण गर्ने {#determining-when-to-re-render-in-react}

Immutability को मुख्य लाभ यो हो कि यसले तपाईंलाई React मा _pure components_ निर्माण गर्न मद्दत गर्दछ। Immutable data सजिलैसँग निर्धारण गर्न  सकिन्छ यदि परिवर्तनहरू गरिएका छन् जसले component re-rendering आवश्यक भएको निर्धारण गर्न मद्दत गर्दछ।

तपाईँले `shouldComponentUpdate()` र *pure components* निर्माण गर्ने बारेमा  [Optimizing Performance](/docs/optimizing-performance.html#examples) पढेर धेरै सिक्न सक्नु हुन्छ। 

### Function Components {#function-components}

हामी अब Square लाई  **function component** मा  परिवर्तन गर्नेछौ। 

React मा, **function components** component हरू लेख्ने सरल तरिका हो जसले केवल `render` method समावेश गर्दछ र तिनीहरूको आफ्नै state हुदैन। एक class परिभाषित गर्नको सट्टा जसले `React.Component` extends गर्छ, हामी एउटा function लेख्न सक्छौ जसले `props` input को रुपमा लिन्छ र rendered हुनु पर्ने कुरा फ़र्काउछ। class हरू भन्दा Function component हरू लेख्नका लागि बढी सजिलो छ, र धेरै component हरू यस तरिकाले व्यक्त गर्न सकिन्छ।

Square class लाई यो function ले बिस्थापित गरौ:

```javascript
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```

हामीले `this.props` बाट `props` मा परिवर्तन गर्यौं यो दुइ पटक देखिन्छ।

**[यो बिन्दुमा पूर्ण कोड हेर्नुहोस्](https://codepen.io/gaearon/pen/QvvJOv?editors=0010)**

>नोट
>
>जब हामी Square लाई function component मा परिमार्जन गर्यौँ, हामीले `onClick = {() => this.props.onClick ()}` लाई छोटो `onClick = {props.onClick}` मा परिवर्तन गर्यौं (*दुवै* पक्षहरूमा parentheses कमीलाई ध्यान दिनुहोस्)।

### पालो लिदा {#taking-turns}

अब हामी हाम्रो tic-tac-toe खेलमा स्पष्ट दोषलाइ ठीक गर्न आवश्यक छ: अहिले "O" बोर्डमा चिन्ह लगाउन सकिँदैन।

हामी पहिलो कदम पूर्वनिर्धारित रूपमा "X" हुन सेट गर्दछौं। हामी यो पूर्वनिर्धारित सेट गर्न  हाम्रो Board constructor मा सुरुवाती state लाई परिमार्जन गर्न सक्दछौं:

```javascript{6}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }
```

प्रत्येक पल्ट एक खेलाडीले चल्छ, `xIsNext` (a boolean) फ्लिप गरिने छ कुन खेलाडी अगाडी जान्छ थाहा पाउनको लागि र खेलको state बचत हुनेछ। हामी `xIsNext` को मान] फ्लिप गर्नको लागि बोर्डको `handleClick` function लाई अद्यावधिक गर्नेछौं:

```javascript{3,6}
  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

यस परिवर्तनको साथ, "X" र "O" ले पालैपालो बदल्न सक्छ। एकचोटी हेर्नुहोस!

आउनुहोस् Board को `render` मा "status" पाठलाई पनि परिवर्तन गरौ ताकि यसले कुन खेलाडी अर्को पङ्क्तिमा छ भनेर प्रदर्शन गर्दछ:

```javascript{2}
  render() {
    const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      // the rest has not changed
```

यी परिवर्तनहरू लागू गरेपछि, तपाईंसँग Board component मा यो हुनु पर्छ:

```javascript{6,11-16,29}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

**[यो बिन्दुमा पूर्ण कोड हेर्नुहोस्](https://codepen.io/gaearon/pen/KmmrBy?editors=0010)**

### विजेता घोषणा गर्दै {#declaring-a-winner}

अहिले हामीले कुन खेलाडीको पालो आउदैछ भनेर देखायौ, हामी खेल जित्दा पनि देखाउनै पर्दछ र त्यहाँ कुनै अरु पालो आउदैन। यो helper function प्रतिलिपि गर्नुहोस् र फाइलको अन्त्यमा राख्नुहोस:

```javascript
function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

9 वर्गहरूको array लाई दिइएको छ, यो function ले  विजेताको लागि जाँच गर्नेछ र उपयुक्त `'X'`,`'O'`, वा `null` फर्काउँछ।

यदि खेलाडीले जितेको छ भनी जाँच गर्नका लागि हामी बोर्डको `render` function मा `calculateWinner(squares)` कल गर्नेछौं। यदि खेलाडीले जित्यो भने, हामी "Winner: X" वा "Winner: O" जस्ता पाठ प्रदर्शन गर्न सक्छौं। हामीले Board को render function मा भएको status घोषणालाई यस कोडले बदल्छौ।

```javascript{2-8}
  render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      // the rest has not changed
```

यदि कसैले खेल जित्यो वा कुनै Square पहिले नै भरिएको छ भने हामीले Board को  `handleClick` function लाई परिवर्तन गरेर पहिले नै  क्लिक लाई बेवास्ता गरेर चाडै नै फर्काउन सक्छौ:

```javascript{3-5}
  handleClick(i) {
    const squares = this.state.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

**[यो बिन्दुमा पूर्ण कोड हेर्नुहोस्](https://codepen.io/gaearon/pen/LyyXgK?editors=0010)**


बधाई छ! तपाईं सँग अहिले काम गर्ने tic-tac-toe खेल छ। र तपाईंले पनि भखरै React को आधारभूत कुराहरू सिक्नुभयो। त्यसैले *तपाईं* शायद यहाँ वास्तविक विजेता हुनुहुन्छ।

## समय यात्रा थप्दै {#adding-time-travel}

अन्तिम अभ्यासको रूपमा, खेलको अघिल्लो चालहरूको "पुरानो समयमा फर्कन" सम्भव बनाऊ।

### चालहरुको अभिलेख भण्डारण गर्दै {#storing-a-history-of-moves}

यदि हामी `squares` array लाई mutate गर्दछौ भने, समय यात्रा लागू गर्न धेरै गाह्रो हुन्छ।


यद्यपि, हामीले प्रत्येक चाल पछि `squares` को नयाँ प्रति सिर्जना गर्न `slice()` प्रयोग गर्यौं, र [यसलाई immutable गरायौ](#why-immutability-is-important)। यसले हामीलाई `squares` array को प्रत्येक विगतको संस्करण भण्डार गर्न अनुमति दिन्छ, र पहिले भै-सकेको चालहरु बीच जान मिल्छ।


हामी पुरानो `squares` arrays लाई अर्को array मा भण्डार गर्नेछौ जसको नाम `history` छ। `history` array ले सबै board state हरूलाई प्रतिनिधित्व गर्दछ, पहिलेबाट अन्तिम चालसम्म, र आकार यस्तो खालको छ:

```javascript
history = [
  // Before first move
  {
    squares: [
      null, null, null,
      null, null, null,
      null, null, null,
    ]
  },
  // After first move
  {
    squares: [
      null, null, null,
      null, 'X', null,
      null, null, null,
    ]
  },
  // After second move
  {
    squares: [
      null, null, null,
      null, 'X', null,
      null, null, 'O',
    ]
  },
  // ...
]
```

अब हामी `history` state कुन component मा राख्ने हो निर्णय गर्न आवश्यक छ।

### फेरि, state लाई माथि लैजादा {#lifting-state-up-again}

हामी पहिलेका चालहरूको सूची प्रदर्शन गर्न शीर्ष-स्तरीय Game component चाहन्छौ। एस्तो गर्नको लागि `history` को पहुँचको आवश्यकता पर्दछ, त्यसैले हामी `history` state लाई शीर्ष स्तरको Game component मा राख्नेछौं।


Game component मा `history` state राख्दा बच्चा Board component बाट `squares` state हटाउन  मद्दत गर्दछ। Square component बाट  Board component मा ["lifted state up"](#lifting-state-up) जस्तै, हामी अब Board बाट शीर्ष स्तरको Game component मा पठाउदै छौं। यसले गर्दा Board को data मा Game component ले  पूर्ण नियन्त्रण प्रदान गर्दछ, र एसले Board लाई `history` बाट अघिल्लो मोडहरू प्रदान गर्न निर्देशन दिन्छ।

पहिलो, हामी यसको  Game component को constructor मा प्रारम्भिक state  सेट अप गर्नेछौं:

```javascript{2-10}
class Game extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      history: [{
        squares: Array(9).fill(null),
      }],
      xIsNext: true,
    };
  }

  render() {
    return (
      <div className="game">
        <div className="game-board">
          <Board />
        </div>
        <div className="game-info">
          <div>{/* status */}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
}
```

अर्को, हामीसँगको Board component ले Game component बाट  `squares` र `onClick` props प्राप्त गर्दछ। अहिले हाम्रो Board मा हामीसंग धेरै Square हरुको लागि एउटा मात्र click handler छ, कुन स्क्वायरमा क्लिक गरियो भनी सुचित गर्न हामी प्रत्येक स्क्वायरको स्थानमा `onClick` handler पठाउन आवश्यक छ। Board component परिवर्तन गर्न आवश्यक चरणहरू यहाँ छन्:

* बोर्डको `constructor` मेटाउनुहोस्।
* Board को `renderSquare` मा `this.state.squares[i]` लाई `this.props.squares[i]` ले बिस्थापित गर्नुहोस। 
* Board को  `renderSquare` मा `this.handleClick(i)` लाई `this.props.onClick(i)` ले बिस्थापित गर्नुहोस।

Board component अब यो जस्तो देखिन्छ:

```javascript{17,18}
class Board extends React.Component {
  handleClick(i) {
    const squares = this.state.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.props.squares[i]}
        onClick={() => this.props.onClick(i)}
      />
    );
  }

  render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```
हामी खेलको स्थिति निर्धारण गर्न र प्रदर्शन गर्न सबैभन्दा हालको history को प्रवेश प्रयोग गर्नको लागि Game component को `render` function लाई अपडेट गर्नेछौं:

```javascript{2-11,16-19,22}
  render() {
    const history = this.state.history;
    const current = history[history.length - 1];
    const winner = calculateWinner(current.squares);

    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div className="game">
        <div className="game-board">
          <Board
            squares={current.squares}
            onClick={(i) => this.handleClick(i)}
          />
        </div>
        <div className="game-info">
          <div>{status}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
```

Game component अहिले खेलको स्थिति rendering गर्दै छ, हामी सम्बन्धित कोडलाई Board को `render` विधिबाट हटाउन सक्छौं। refactoring पछि, Board को `render` function यस्तो देखिन्छ:

```js{1-4}
  render() {
    return (
      <div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
```

अन्तमा, हामीले `handleClick` method लाई Board component बाट Game component मा सार्न आवश्यक छ।  हामीले `handleClick` लाई परिमार्जन गर्न आवश्यक छ किनकि Game component को state फरक रूपमा संरचित छ। Game को `handleClick` method भित्र, हामी नयाँ history लाई `history` मा समेट्छौं।

```javascript{2-4,10-12}
  handleClick(i) {
    const history = this.state.history;
    const current = history[history.length - 1];
    const squares = current.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      history: history.concat([{
        squares: squares,
      }]),
      xIsNext: !this.state.xIsNext,
    });
  }
```

>नोट
>
>array `push()` method को विपरीत तपाईँ अधिक परिचित हुन हुन्छ होला, `concat ()` method ले original array लाई mutate  गर्दैन, त्यसैले हामी यो मन पराउछौ।

यस समय सम्म आइ पुग्दा, Board component लाई  `renderSquare` र  `render` method हरुको  मात्र आवश्यकता छ। खेलको state र `handleClick` method चाही Game component मा हुनुपर्छ।

**[यो बिन्दुमा पूर्ण कोड हेर्नुहोस्](https://codepen.io/gaearon/pen/EmmOqJ?editors=0010)**

### अघिल्लो चालहरू देखाउँदै {#showing-the-past-moves}

हामी tic-tac-toe मा खेलको history रेकर्ड गर्दैछौँ, अब हामी त्यसलाई पहिलेका चालहरूको सूचीको रूपमा खेलाडीमा देखाउन सक्छौं।

हामीले पहिले सिक्यौ कि React element हरू first-class JavaScript object हरू होईनन; हामी उनीहरूलाई हाम्रो application हरूमा बिचमा पास गर्न सक्छौं। React मा धेरै item हरू प्रस्तुत गर्न, हामी React element हरूको array प्रयोग गर्न सक्छौं।

Javascript मा, arrays सँग [`map()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) हुन्छ जुन सामान्यतया data बाट अन्य data मा म्यापिङ गर्नको लागि प्रयोग गरिन्छ, उदाहरणका लागि:

```js
const numbers = [1, 2, 3];
const doubled = numbers.map(x => x * 2); // [2, 4, 6]
```

`map` method प्रयोग गरेर, हामी हाम्रो पहिलेको React element हरुको चालहरू स्क्रीन मा बटनहरु देखाउन map गर्न सक्छौ, र अघिल्लो चालहरूमा "jump" गर्न बटनहरूको सूची प्रदर्शन गर्दछौ।

Game को `render` method मा `history` लाई `map` गरौं।

```javascript{6-15,34}
  render() {
    const history = this.state.history;
    const current = history[history.length - 1];
    const winner = calculateWinner(current.squares);

    const moves = history.map((step, move) => {
      const desc = move ?
        'Go to move #' + move :
        'Go to game start';
      return (
        <li>
          <button onClick={() => this.jumpTo(move)}>{desc}</button>
        </li>
      );
    });

    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div className="game">
        <div className="game-board">
          <Board
            squares={current.squares}
            onClick={(i) => this.handleClick(i)}
          />
        </div>
        <div className="game-info">
          <div>{status}</div>
          <ol>{moves}</ol>
        </div>
      </div>
    );
  }
```

**[यो बिन्दुमा पूर्ण कोड हेर्नुहोस्](https://codepen.io/gaearon/pen/EmmGEa?editors=0010)**

Tic-tac-toe खेलको history मा प्रत्येक चालको लागि, हामी एक सूची वस्तु `<li>` बनाउछौ जसमा एउटा बटन हुन्छ  `<button>`। बटनमा `onClick` ह्यान्डलर छ जसले `this.jumpTo()` भनिने method कल गर्छ। हामीले अहिलेसम्म `jumpTo()` method लागू गरेको छैनौ। अहिलेको लागि, हामी खेलमा भएको चालहरुको सुची  र विकासकर्ता उपकरण console मा एउटा चेतावनी हेर्नुपर्छ जसले यसो भन्छ:

>  Warning:
>  Each child in an array or iterator should have a unique "key" prop. Check the render method of "Game".

आउनुहोस् माथि उल्लिखित चेतावनीको बारेमा छलफल गरौं।

### Key छान्दै {#picking-a-key}

जब हामी एक list  render गर्छौं, React ले प्रत्येक rendered list item बारे केहि जानकारी भण्डारण गर्दछ। जब हामी एउटा list अपडेट गर्छौं, React ले के परिवर्तन भएको छ थाहा पाउन आवश्यक छ। हामी थप्न, हटाउन, पुन:मिलाउन वा list को चीजहरू अद्यावधिक गर्न सक्थ्यौं।

transitioning कल्पना गर्नुहोस्

```html
<li>Alexa: 7 tasks left</li>
<li>Ben: 5 tasks left</li>
```
बाट 

```html
<li>Ben: 9 tasks left</li>
<li>Claudia: 8 tasks left</li>
<li>Alexa: 5 tasks left</li>
```
मा

अद्यावधिक गरिएका गणनाहरूको अतिरिक्त, एक मानव पढाइले शायद हामी Alexa र Ben को क्रम परिवर्तन र Alexa र Ben बीच Claudia घुमाएको छ भनेर भन्न सक्नेछ। यद्यपि, React एउटा कम्प्यूटर प्रोग्राम हो र हामी के गर्न चाहन्छौ त्यो React ले थाहा पाउदैन। किनकि React ले हाम्रो अभिप्रायहरू थाहा पाउन सक्दैन, हामीले प्रत्येक list item को लागि *key* property निर्दिष्ट गर्न आवश्यक छ किनकि प्रत्येक list item  siblings हरूसंग अलग हुनुपर्छ। एक विकल्प strings `alexa`,` ben`, `claudia` को प्रयोग गर्ने हुनेछ। यदि हामीले डेटाबेसबाट data प्रदर्शन गर्दै छौ भने, Alexa, Ben, र Claudia को डेटाबेस ID  हरु  keys को  रूपमा प्रयोग गर्न सकिन्छ।

```html
<li key={user.id}>{user.name}: {user.taskCount} tasks left</li>
```
जब list  पुन: render गरिएको हुन्छ, React ले प्रत्येक list item को key लिन्छ र मिल्दो key को लागि अघिल्लो list को item हरू खोजी गर्दछ।  यदि हालको list मा एक key छ जुन आघिल्लोमा अवस्थित छैन भने, React ले एक component बनाउछ। यदि हालको list मा  अघिल्लो list मा अवस्थित key हराइरहेको छ भने, React ले अघिल्लो component नष्ट गर्दछ। यदि दुई key हरू मेल खान्छ भने, सम्बन्धित component सारिन्छ। key हरुले React लाई प्रत्येक component को पहिचानको बारेमा बताउँछन जसले React लाई पुन: render हुदा state लाई मिलाएर राख्न सहयोग पुर्याउँछ। यदि component को key परिबर्तनहरु हुन्छ भने, component नाश गरिनेछ र नयाँ state को साथमा पुन: सिर्जना गरिनेछ।

`key` React मा एक विशेष र सुरक्षित property हो (`ref` सहित, एक थप उन्नत सुविधा)। जब एक element बनाइन्छ, React ले `key` property निकाल्छ र key लाई सीधा फर्काइएको element मा भण्डार गर्दछ। यद्यपि `key` चाही `props` मा पर्न सक्छ जस्तो लाग्न सक्छ, `key` लाई `this.props.key` प्रयोग गरी गर्न सकिँदैन। कुन component अद्यावधिक गर्ने भनि निर्णय गर्न React ले स्वचालित रूपमा `key` प्रयोग गर्दछ। Component ले यसको `key` को बारेमा सोध्न सक्दैन।

**यो दृढतापूर्वक सिफारिस गरिएको छ कि जब तपाइँ dynamic list हरू बनाउनुहुन्छ तपाईले सही key हरू प्रदान गर्नुहुन्छ।** यदि तपाईंसँग उपयुक्त key छैन भने, तपाइँ आफ्नो data फेरी बनाउने विचार गर्न चाहानुहुन्छ होला जुन तपाईंले गर्नुपर्छ।

यदि key निर्दिष्ट गरिएको छैन भने, React ले चेतावनी प्रस्तुत गर्नेछ र पूर्वनिर्धारित रूपमा array index को key प्रयोग गर्नेछ। key को रूपमा array index प्रयोग गर्दा list को item पुन:क्रम मिलाउने वा list item हरू हाल्ने/हटाउने प्रयास गर्दा समस्याग्रस्त हुन्छ।  स्पष्ट रूपमा `key = {i}` लाई पठाउदा चेतावनीलाइ रोक्छ तर array indices मा पहिलेको जस्तै समस्या छ र धेरै परिस्थितिहरूमा सिफारिस गरिएको छैन।

Key हरू सबै component मा अद्वितीय हुन आवश्यक छैन; तिनीहरू केवल component र तिनीहरूका sibling हरूको बीचमा अद्वितीय हुनु आवश्यक छ।


### समय यात्रा कार्यान्वयन{#implementing-time-travel}

tic-tac-toe खेलको history मा, प्रत्येक विगतको चालसँग सम्बन्धित कुनै अद्वितीय ID छ: यो चालको अनुक्रमिक संख्या हो। चालहरू कहिल्यै पुन:क्रम, मेटाउने वा बीचमा हाल्ने गरिएको छैन, त्यसैले यो चाल index लाई key को रूपमा प्रयोग गर्न सुरक्षित छ।

Game component को `render` method मा, हामी key को रूपमा `<li key = {move}>`  थप्न सक्दछौ र key हरूको लागि आएको React को चेतावनी गायब हुनुपर्छ:

```js{6}
    const moves = history.map((step, move) => {
      const desc = move ?
        'Go to move #' + move :
        'Go to game start';
      return (
        <li key={move}>
          <button onClick={() => this.jumpTo(move)}>{desc}</button>
        </li>
      );
    });
```

**[यो बिन्दुमा पूर्ण कोड हेर्नुहोस्](https://codepen.io/gaearon/pen/PmmXRE?editors=0010)**

कुनै list item को बटन क्लिक गर्नाले error फाल्छ किनभने `jumpTo` method अपरिभाषित छ। `JumpTo` लाई लागू गर्नु अघि, हामी Game component को state मा `stepNumber` थप्ने छौ जसले गर्दा हामी कुन चरण हेर्दै छौं भन्ने थाहा हुन्छ।

सर्बप्रथम, Game को `constructor` मा प्रारम्भिक state मा `stepNumber: 0` थप गर्नुहोस्:

```js{8}
class Game extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      history: [{
        squares: Array(9).fill(null),
      }],
      stepNumber: 0,
      xIsNext: true,
    };
  }
```

अर्को, हामी `stepNumber` लाई अपडेट गर्नको लागि `jumpTo` method Game मा परिभाषित गर्नेछौं। हामीले `XIsNext` लाई पनि true सेट गर्छौ यदि हामीले `stepNumber` मा परिवर्तन गरेको नम्बर जोर छ भने:

```javascript{5-10}
  handleClick(i) {
    // this method has not changed
  }

  jumpTo(step) {
    this.setState({
      stepNumber: step,
      xIsNext: (step % 2) === 0,
    });
  }

  render() {
    // this method has not changed
  }
```

हामी अब Game को `handleClick` method मा केहि परिवर्तनहरू गर्नेछौं जुन method तपाईले square मा क्लिक गर्दा कल हुन्छ।

हामीले थपेको `StepNumber` state ले अहिले प्रयोगकर्तालाई देखाइएको चाललाई प्रतिबिम्बित गर्दछ।  हामी नयाँ चाल चलेपछि, `stepNumber: history.length` लाइ `this.setState` argument को भागको रूपमा राखेर `stepNumber` लाई अपडेट गर्न आवश्यक छ। यसले हामी एक नयाँ चाल पछि फेरी पहिलेको चालमा नै अड्किदैन भन्ने सुनिश्चित गर्दछ।

हामी `this.state.history` लाई पनि `this.state.history.slice(0, this.state.stepNumber + 1)` ले प्रतिस्थापित गर्नेछौ।  यसले यो सुनिश्चित गर्दछ कि यदि हामी "पहिलेको समयमा फिर्ता जान्छौ" र त्यस बिंदु बाट एक नया चाल चल्छौ भने, हामी सबै "future" history पर फ्याकिदिन्छौ जसले गर्दा future history गलत हुनेछ।

```javascript{2,13}
  handleClick(i) {
    const history = this.state.history.slice(0, this.state.stepNumber + 1);
    const current = history[history.length - 1];
    const squares = current.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      history: history.concat([{
        squares: squares
      }]),
      stepNumber: history.length,
      xIsNext: !this.state.xIsNext,
    });
  }
```

अन्ततः, हामी `stepNumber` को अनुसार अन्तिम चरण render गरेर हालै चयन गरिएको चाल render गर्न  Game component को `render` method परिमार्जन गर्नेछौं:

```javascript{3}
  render() {
    const history = this.state.history;
    const current = history[this.state.stepNumber];
    const winner = calculateWinner(current.squares);

    // the rest has not changed
```

यदि हामी खेलको history मा कुनै पनि चरणमा क्लिक गर्छौं भने, tic-tac-toe board ले चरण पछि बोर्ड कस्तो देखिन्छ भनेर देखाउन तुरुन्तै अद्यावधिक गर्नैपर्छ।

**[यो बिन्दुमा पूर्ण कोड हेर्नुहोस्](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**

### टुङ्गाउदै {#wrapping-up}

बधाई छ! तपाईंले एउटा tic-tac-toe खेल बनाउनु भएको छ:

* तपाइँले tic-tac-toe खेल खेल्नुहोस,
* खेलाडीले खेल जितेको बेला सूचित गर्दछ,
* खेलको प्रगतिको रूपमा खेलको इतिहास भण्डार गर्दछ,
* खेलाडीहरूलाई खेलको इतिहास समीक्षा गर्न र खेलको बोर्डको अघिल्लो संस्करणहरू हेर्न अनुमति दिन्छ।

राम्रो काम! हामी आशा गर्छौं कि तपाई अब React ले कसरी काम गर्दछ भनेर उचित ज्ञान पाउनुभयो।

अन्तिम परिणाम यहाँ जाँच गर्नुहोस्: **[अन्तिम परिणाम](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**.


यदि तपाईंसँग अतिरिक्त समय छ वा तपाईंको नयाँ React कुशलताहरू अभ्यास गर्न चाहनुहुन्छ भने, यहाँ केहि सुझावहरू छन् जुन तपाइँले tic-tac-toe खेलमा सुधार गर्न सक्नुहुनेछ जुन कठिनाइ बढ्दो रुपमा क्रमबद्ध गरिएको छ:

1. प्रत्येक चालको लागि सार्दा इतिहास सूचीमा ढाँचा (col, row) मा स्थान प्रदर्शन गर्नुहोस्।
2. चाल सूचीमा हालै चयन गरिएको item लाई बोल्ड गर्नुहोस्।
3. hardcoding गर्नुको सट्टा दुई loops प्रयोग गर्न squares बनाउनुहोस तेस्को लागि Board पुन: लेख्नुहोस।
4. एक toggle बटन बनाउनुहोस जसले तपाईंलाई बढ्दो वा घट्दो क्रममा चालहरू क्रमबद्ध गर्दछ।
5. जब कसैले जीत्यो भने, तीनवटा squares जसबाट खेल जितेको छ तिनीहरुलाई हाइलाइट गर्नुहोस।
6. जब कसैले पनि जित्दैन, कसैले जित्न नसकेको नतिजाको बारेमा जानकारी प्रदर्शन गर्नुहोस्।

यस ट्यूटोरियलको दौरान, हामी element हरू, component हरू, prop हरू, र state सहित React अवधारणाहरूमा ध्यान दियौ। यी प्रत्येक विषयहरूको थप विस्तृत व्याख्याको लागि, जाँच गर्नुहोस् [बाँकी documentation](/docs/hello-world.html)। component परिभाषित गर्ने बारेमा बढी जान्नको लागि, [`React.Component` API reference](/docs/react-component.html) जाँच गर्नुहोस्।
