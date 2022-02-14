---
id: rendering-elements
title: Rendering Elements
permalink: docs/rendering-elements.html
redirect_from:
  - "docs/displaying-data.html"
prev: introducing-jsx.html
next: components-and-props.html
---

Element हरू React एप्सको निर्माण ब्लकहरु हुन्।

एक element ले तपाइँ स्क्रीनमा हेर्न चाहनुहुन्छ वर्णन गर्दछ:

```js
const element = <h1>Hello, world</h1>;
```

ब्राउजरको DOM element हरूको विपरीत, React element हरु सादा objects हुन्, र बनाउदा सस्तो हुन्छ। React DOM ले React element हरूसँग मिलाउन DOM लाई अद्यावधिक गर्न हेरचाह गर्दछ।

>**नोट:**
>
>"components" को अधिक व्यापक रूपमा ज्ञात अवधारणा हुनाले elements बाट भ्रमित हुन सकिन्छ। हामी [अर्को खण्डमा](/docs/components-and-props.html) component हरूको परिचय गर्नेछौं। element हरूबाट component हरु  "बनेको हुन्छन", र हामी अघि बढ्नु अघि यो खण्ड पढ्न प्रोत्साहन गर्दछौं।

## एउटा Element DOM मा render गर्दै {#rendering-an-element-into-the-dom}

हेरौ त्यहाँ एउटा  `<div>` तपाईको HTML फाइल भित्र कतै छ:

```html
<div id="root"></div>
```

हामी यसलाई एक "root" DOM node भन्छौं किनभने यसको भित्र सबै चीजहरू React DOM द्वारा व्यवस्थित गरिनेछ।

प्राय: React मात्र प्रयोग गरी निर्मित Application हरुमा  एउटा root DOM node हुन्छ। यदि तपाइँ एक अवस्थित app मा React प्रयोग गर्नु भएको छ भने, तपाईंलाई जस्तो मनपर्छ तेस्तो धेरै अलग root DOM node हरू हुन सक्दछ।

<<<<<<< HEAD
root DOM node मा एक react element render गर्न, दुवै लाई  `ReactDOM.render()` मा पास गर्नुहोस:
=======
To render a React element into a root DOM node, pass both to [`ReactDOM.render()`](/docs/react-dom.html#render):
>>>>>>> fb382ccb13e30e0d186b88ec357bb51e91de6504

`embed:rendering-elements/render-an-element.js`

<<<<<<< HEAD
[कोडपेनमा यो प्रयास गर्नुहोस्](codepen://rendering-elements/render-an-element)
=======
**[Try it on CodePen](https://codepen.io/gaearon/pen/ZpvBNJ?editors=1010)**
>>>>>>> 71cc6be6182418dec43b72f2a9ef464619cb7025

यसले पेजमा "Hello, world" देखाउँछ।

## Render गरिएको Element अपडेट गर्दै {#updating-the-rendered-element}

React elements [immutable](https://en.wikipedia.org/wiki/Immutable_object) हुन्छन। एकपटक तपाईंले एक element बनाएपछि, तपाईं एस्को child वा attributes परिवर्तन गर्न सक्नुहुन्न। चलचित्रमा हुने एक एकल फ्रेम जस्तै एक element हो: यो निश्चित समयमा UI को प्रतिनिधित्व गर्दछ।

<<<<<<< HEAD
अहिले सम्मको ज्ञान बाट यो कुरा थाहा पाउछौ कि, UI अद्यावधिक गर्न को लागि एकमात्र तरीका एक नयाँ element बनाउनु हो, र यसलाई `ReactDOM.render ()` मा पठाउनु पर्छ।
=======
With our knowledge so far, the only way to update the UI is to create a new element, and pass it to [`ReactDOM.render()`](/docs/react-dom.html#render).
>>>>>>> fb382ccb13e30e0d186b88ec357bb51e91de6504

यो चालु घडीको उदाहरणलाई विचार गर्नुहोस्:

`embed:rendering-elements/update-rendered-element.js`

<<<<<<< HEAD
[कोडपेनमा यो प्रयास गर्नुहोस्](codepen://rendering-elements/update-rendered-element)
=======
**[Try it on CodePen](https://codepen.io/gaearon/pen/gwoJZk?editors=1010)**
>>>>>>> 71cc6be6182418dec43b72f2a9ef464619cb7025

<<<<<<< HEAD
यसले `ReactDOM.render()` लाई हरेक सेकेन्डमा [`setInterval()`](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) callback बाट कल गर्दछ।
=======
It calls [`ReactDOM.render()`](/docs/react-dom.html#render) every second from a [`setInterval()`](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) callback.
>>>>>>> fb382ccb13e30e0d186b88ec357bb51e91de6504

>**नोट:**
>
<<<<<<< HEAD
>धेरैजसो, अधिकांश React app हरुले `ReactDOM.render()` एक पटक मात्र कल गर्छ।अर्को खण्डमा हामी यो कोडले [stateful components](/docs/state-and-lifecycle.html) मा कसरी encapsulated हुन्छ भन्ने सिक्छौं।
=======
>In practice, most React apps only call [`ReactDOM.render()`](/docs/react-dom.html#render) once. In the next sections we will learn how such code gets encapsulated into [stateful components](/docs/state-and-lifecycle.html).
>>>>>>> fb382ccb13e30e0d186b88ec357bb51e91de6504
>
>हामी तपाईलाई विषयहरू नछोड्न सिफारिस गर्दछौं किनकि तिनीहरू एकअर्कामा बनेको हुन्छन।

## React ले जे आवश्यक छ त्यहि अपडेट गर्छ {#react-only-updates-whats-necessary}

React DOM ले element र यसको बच्चाहरूलाई अघिल्लो DOM संग तुलना गर्दछ, र केवल  DOM लाई चाहिएको state मा ल्याउन आवश्यक पर्ने DOM मात्र अद्यावधिक हुन्छ।

<<<<<<< HEAD
तपाइँ ब्राउजर उपकरणहरूसँग [अन्तिम उदाहरण](codepen://rendering-elements/update-rendered-element) निरीक्षण गरेर प्रमाणित गर्न सक्नुहुन्छ:
=======
You can verify by inspecting the [last example](https://codepen.io/gaearon/pen/gwoJZk?editors=1010) with the browser tools:
>>>>>>> 71cc6be6182418dec43b72f2a9ef464619cb7025

![DOM inspector showing granular updates](../images/docs/granular-dom-updates.gif)

<<<<<<< HEAD
यद्यपि हामी प्रत्येक tick मा पुरा UI रूख वर्णन गर्दै एक तत्व सिर्जना गर्छौं, केवल text node जसको सामग्रीहरू परिवर्तन भएको हुन्छ त्यही मात्र React DOM द्वारा अद्यावधिक हुन्छ।
=======
Even though we create an element describing the whole UI tree on every tick, only the text node whose contents have changed gets updated by React DOM.
>>>>>>> 821e20726266bc8113353d0c2b6d885f82e584a8

<<<<<<< HEAD
हाम्रो अनुभवमा, UI लाई केहि समयपछि कसरी परिबर्तन गर्ने सोच्नुको सट्टा UI लाई अहिले कसरि देखाउने भनेर विचार गर्ने हो भने सबै bug हरु हट्छ।
=======
In our experience, thinking about how the UI should look at any given moment, rather than how to change it over time, eliminates a whole class of bugs.
>>>>>>> fb382ccb13e30e0d186b88ec357bb51e91de6504
