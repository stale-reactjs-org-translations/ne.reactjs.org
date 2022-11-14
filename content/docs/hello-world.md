---
id: hello-world
title: Hello World
permalink: docs/hello-world.html
prev: cdn-links.html
next: introducing-jsx.html
---

सानो React उदाह्रण यस्तो देखिन्छ : 

```jsx
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<h1>Hello, world!</h1>);
```

यस्ले पेजमा "Hello, world!" शिर्षक प्रद्शर्न गर्छ । 

**[Try it on CodePen](https://codepen.io/gaearon/pen/rrpgNB?editors=1010)**


माथी को लिन्क क्लिक गरी अन्लाईन सम्पादन गर्नुस ।  केहि परिवर्तन स्वतन्त्र रुपले गरेर, कसरी तिनीहरूले आउटपुट असर पर्छ हेर्नुस । यस गाइडमा प्राय पृष्ठहरू यस प्रकारको सम्पादनयोग्य उदाहरणहरू हुनेछन् ।


## यो गाइड कसरी पढ्ने {#how-to-read-this-guide}

यस गाईडमा, हामी React apps निर्माण ब्लकहरू जाँच गर्नेछौं: elements and components. एकचोटी तपाईं तिनिहरुमा मास्टर भएपछी, तपाईं साना पुन: प्रयोगयोग्य टुक्राहरूबाट जटिल apps सिर्जना गर्न सक्नुहुनेछ।.

>टिप
>
>यो गाईड व्यक्तिहरूको लागि डिजाईन गरीएको छ जसले **step by step अवधारणाहरू सिक्न खोज्छ**. यदि तपाईं गरेर सिक्न चाहानुहुन्छ भने, हाम्रो जाँच गर्नुहोस् [व्यावहारिक tutorial](/tutorial/tutorial.html). तपाइँ यो गाइड र tutorial एक अर्को को पूरक पाउन सक्नुहुन्छ ।

मुख्य React अवधारणाहरूको बारेमा चरण-देखि-चरण गाईडमा यो पहिलो अध्याय हो. तपाईंले नेभिगेशन साइडबारमा यसको सबै अध्यायहरूको सूची फेला पार्न सक्नुहुनेछ । यदि तपाईं मोबाइलबाट यो पढ्दै हुनुहुन्छ भने, तपाईंले आफ्नो स्क्रिनको तल दायाँ कुनामा बटन थिचेर नेभिगेसन पहुँच गर्न सक्नुहुनेछ । 

यस गाइडको प्रत्येक अध्यायले अघिल्लो अध्यायको ज्ञानमा आधारित छ ।  **तपाईले प्राय: React "मुख्य अवधारणाहरूको" गाईड अध्यायहरू साइडबारमा देखा पर्ने क्रममा पढेर सिक्न सक्नुहुन्छ ।** उदाहरणको लागी
, [“JSX परिचय दिदै”](/docs/introducing-jsx.html) यस पछि अर्को अध्याय हो.

## ज्ञान स्तर अनुमानहरू {#knowledge-level-assumptions}

React JavaScript Library हो, र त्यसैले हामी यो मान्दछौं कि तपाइँसँग JavaScript भाषाको आधारभूत ज्ञान छ. **यदि तपाईं धेरै आत्मविश्वास महसुस गर्नुहुन्न भने, हामी तपाईंलाई [JavaScript ट्यूटोरियलमा](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript) जानको लागि सिफारिश गर्दछौं, तपाईंको ज्ञान स्तर जाँच गर्न** र तपाईंलाई यो गाइड पछ्याउन सजिलो हुन्छ । तपाईंलाई १ घण्टा र ३० मिनेट सम्म लाग्न सक्छ, तर नतीजाको रूपमा तपाईले React र JavaScript दुबै एकै समयमा सिक्दै हुनुहुन्छ जस्तो महसुस गर्न आवश्यक छैन ।

>नोट
>
<<<<<<< HEAD
>यस गाइडले कहिलेकाँही उदाहरणहरूमा नयाँ JavaScript वाक्य संरचना प्रयोग गर्दछ । यदि तपाईंले JavaScript का साथ पछिल्ला केही बर्षहरूमा काम गर्नुभएको छैन भने, [यी तीन बिन्दुहरूले](https://gist.github.com/gaearon/683e676101005de0add59e8bb345340c) तपाईंलाई सबैभन्दा धेरै मार्गमा सहयोग गर्छ्न । 
=======
>This guide occasionally uses some newer JavaScript syntax in the examples. If you haven't worked with JavaScript in the last few years, [these three points](https://gist.github.com/gaearon/683e676101005de0add59e8bb345340c) should get you most of the way.
>>>>>>> 3bba430b5959c2263c73f0d05d46e2c99c972b1c


## सुरु गरौं! {#lets-get-started}

तल Scrolling गरी राख्नुहोस्, र तपाईं यस वेबसाइटको फुटरमा [यस गाइडको अर्को अध्यायको](/docs/introducing-jsx.html) लिंक फेला पार्नुहुनेछ । 


