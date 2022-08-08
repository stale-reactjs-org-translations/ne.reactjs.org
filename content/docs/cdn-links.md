---
id: cdn-links
title: CDN लिङ्कहरू
permalink: docs/cdn-links.html
prev: create-a-new-react-app.html
next: release-channels.html
---

दुबै React र ReactDOM हरु CDN मा उपलब्ध छन्।

```html
<script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
```

माथिको संस्करणहरू केवल डेभलपमेन्टका लागि मात्र हुन्, र प्रोडक्सनको लागि उपयुक्त छैन। React को संकुचित र अनुकूलित बनाईएको संस्करणहरू यहाँ उपलब्ध छन्:

```html
<script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
```

<<<<<<< HEAD
<<<<<<< HEAD
`react` र `react-dom` को विशेष संस्करण प्रयोग गर्नको लागि, `16` लाई संस्करण अंकले बदल्नुहोस।
=======
To load a specific version of `react` and `react-dom`, replace `17` with the version number.
>>>>>>> 6682068641c16df6547b3fcdb7877e71bb0bebf9
=======
To load a specific version of `react` and `react-dom`, replace `18` with the version number.
>>>>>>> 4808a469fa782cead9802619b0341b27b342e2d3

### हामीलाई `crossorigin` Attribute किन चाहिन्छ? {#why-the-crossorigin-attribute}

यदि तपाइँ CDN बाट React सेवा लिनुहुन्छ भने, हामी [`crossorigin`](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_settings_attributes) attribute प्रयोग गर्न सल्लाह दिन्छौं:

```html
<script crossorigin src="..."></script>
```

हामी तपाईंलाई यो प्रमाणित गर्न सल्लाह दिन्छौ कि तपाईंले प्रयोग गर्नुभएको CDN ले `Access-Control-Allow-Origin: *` HTTP हेडर सेट गरेको छ।

![Access-Control-Allow-Origin: *](../images/docs/cdn-cors-header.png)

यसले React १६ र पछिका संस्करणहरुमा [त्रुटिहरु अझ राम्रोसंग सम्हाल्ने अनुभव](/blog/2017/07/26/error-handling-in-react-16.html) प्रदान गर्दछ।
