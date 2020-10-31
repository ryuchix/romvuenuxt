<template>
  <div id="privacy">
    <v-app>
      <div class="content">
        <h1 class="mb-3">Privacy Policy</h1>
        <h3>What information do we collect?</h3>
        <p>We collect information from you when you register on our site. When ordering or registering on our site, as appropriate, you may be asked to enter your: name or e-mail address. You may, however, visit our site anonymously.</p>
        <h3>What do we use your information for?</h3>
        <p>Any of the information we collect from you may be used in one of the following ways:</p>
        <ul>
          <li>To personalize your experience (your information helps us to better respond to your individual needs)</li>
          <li>To improve our website (we continually strive to improve our website offerings based on the information and feedback we receive from you)</li>
          <li>To improve customer service (your information helps us to more effectively respond to your customer service requests and support needs)</li>
        </ul>
        <h3 class="mt-3">How do we protect your information?</h3>
        <p>We implement a variety of security measures to maintain the safety of your personal information when you access your personal information.</p>
        <h3>Do we use cookies?</h3>
        <p>Yes (Cookies are small files that a site or its service provider transfers to your computers hard drive through your Web browser (if you allow) that enables the sites or service providers systems to recognize your browser and capture and remember certain information We use cookies to understand and save your preferences for future visits and compile aggregate data about site traffic and site interaction so that we can offer better site experiences and tools in the future.</p>
        <h3>Do we disclose any information to outside parties?</h3>
        <p>We do not sell, trade, or otherwise transfer to outside parties your personally identifiable information. This does not include trusted third parties who assist us in operating our website, conducting our business, or servicing you, so long as those parties agree to keep this information confidential. We may also release your information when we believe release is appropriate to comply with the law, enforce our site policies, or protect ours or others rights, property, or safety. However, non-personally identifiable visitor information may be provided to other parties for marketing, advertising, or other uses.</p>
        <h3>Third party links</h3>
        <p>Occasionally, at our discretion, we may include or offer third party products or services on our website. These third party sites have separate and independent privacy policies. We therefore have no responsibility or liability for the content and activities of these linked sites. Nonetheless, we seek to protect the integrity of our site and welcome any feedback about these sites.</p>
        <h3>Cookies &amp; 3rd Party Advertisements</h3>
        <p>Google, as a third party vendor, uses cookies to serve ads on your site. Google's use of the DART cookie enables it to serve ads to your users based on their visit to your sites and other sites on the Internet. Users may opt out of the use of the DART cookie by visiting the Google ad and content network privacy policy.</p>
        <p>We allow third-party companies to serve ads and/or collect certain anonymous information when you visit our web site. These companies may use non-personally identifiable information (e.g., click stream information, browser type, time and date, subject of advertisements clicked or scrolled over) during your visits to this and other Web sites in order to provide advertisements about goods and services likely to be of greater interest to you. These companies typically use a cookie or third party web beacon to collect this information. To learn more about this behavioral advertising practice or to opt-out of this type of advertising, you can visit http://www.networkadvertising.org/managing/opt_out.asp.</p>
        <h3>Online Privacy Policy Only</h3>
        <p>This online privacy policy applies only to information collected through our website and not to information collected offline.</p>
        <h3>Your Consent</h3>
        <p>By using our site, you consent to our privacy policy.</p>
        <h3>Changes to our Privacy Policy</h3>If we decide to change our privacy policy, we will post those changes on this page.
        <h3 class="mt-3">Contact Us</h3>
        <p>If you have any questions about this Privacy Policy, please contact us: support@ragnarokmobile.net</p>
      </div>
    </v-app>
  </div>
</template>
<script>
export default {
  name: "PrivacyPolicy",
  layout: 'default',
  head() {
    let title_ = "Privacy Policy | Ragnarok Mobile - Guide, Quest, Build and Database for Ragnarok M Eternal Love"
    let url_ = 'https://www.ragnarokmobile.net/privacy-policy'
    let keywords_ = 'ragnarok mobile privacy policy, ROM, ROM Exchange price, market finance, Ragnarok, online, RO, ragnarok mobile, ragnarok m, ragnarok eternal love, database, guide, job, quest, headgear quest, monster drops, item information, skill description, skill simulator, stat calculator, ragnarok tools, ragnarok mobile english'
    let description_ = 'Your ultimate guide for Ragnarok Mobile Eternal Love. Your source for Ragnarok M Monsters, Cards, Quests, Database, Headwears, Blueprints, Items, Market Prices, Exchange Price List and Stats and Skills calculator. ROM'
    return {
      title: title_,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: description_
        },
        {
          hid: 'keywords',
          name: 'keywords',
          content: keywords_
        },
        {
          hid: 'og:title',
          name: 'og:title',
          content: title_
        },
        {
          hid: 'og:description',
          name: 'og:description',
          content: description_
        },
        {
          hid: 'og:url',
          name: 'og:url',
          content: url_
        },
        {
          hid: 'og:image',
          name: 'og:image',
          content: 'https://www.ragnarokmobile.net/img/louyang.webp'
        },
        {
          hid: 'twitter:description',
          name: 'twitter:description',
          content: description_
        },
        {
          hid: 'twitter:title',
          name: 'twitter:title',
          content: title_
        },
      ],
      link: [
        {
          rel: 'canonical',
          href: url_
        }
      ]
    }
  },
};
</script>