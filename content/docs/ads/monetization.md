---
$title: Monetizing your AMP page with ads
$order: 1
toc: true
components:
    - youtube
---

[TOC]

This guide provides  instructions and best practices for displaying ads on your AMP pages.

## Adding ads to your page

In non-AMP pages (traditional HTML), if you want to display ads on your page, you'd include a snippet of JavaScript to serve ads from your ad network.  For performance and security reasons, you cannot include third-party JavaScript in AMP pages.  So, to display ads in AMP, you need to add the custom [`<amp-ad>`](/docs/reference/components/amp-ad.html) component to your AMP page.

Tip: See [AMP By Example for a live demo](https://ampbyexample.com/components/amp-ad/) that demonstrates adding an amp-ad tag to an AMP page.

Let's walk through the steps of adding the component so you can display ads on your AMP page.

### Step 1: Add the amp-ad script

The `<amp-ad>` component is a custom ad extension to the AMP library. Under the hood of `<amp-ad>`is custom JavaScript that's carefully designed to optimize performance. To run the `<amp-ad>` component, you must add the required JavaScript for this component in the `head` section of your AMP page:

```html
<script async custom-element="amp-ad" src="https://cdn.ampproject.org/v0/amp-ad-0.1.js"></script>
```

### Step 2: Add the amp-ad tag to your AMP page

Over 100+ [ad servers and networks]({{g.doc('/content/docs/ads/ads_vendors.md', locale=doc.locale).url.path}}) provide built-in integrations with AMP.  To add an ad for a given ad network, add the `<amp-ad>` tag, and specify the network in the `type` attribute.

In this example, we are adding an ad slot to serve ads from the a9 network:

```html
<amp-ad type="a9">
</amp-ad>
```

### Step 3: Specify the size of the ad unit

Add the `width` and `height` attributes to the `<amp-ad>`  tag.  This specifies the size of the ad on your AMP page:

```html hl_lines="2"
<amp-ad type="a9">
   width="300" height="250"
</amp-ad>
```

### Step 4: Set ad network parameters

Each network has specific data attributes they require to serve ads.  Refer to the ad network's `<amp-ad>` documentation and add the attributes that are needed In the following example,  the a9 network requires additional parameters to specify the size of the ad, and other details:

```html hl_lines="3 4 5"
<amp-ad type="a9"
    width="300" height="250"
    data-aax_size="300x250"
    data-aax_pubname="test123"
    data-aax_src="302">
</amp-ad>
```

### Step 5: (Optional) Specify a placeholder

Depending on the ad network, you can choose to show a placeholder until the ad is available for viewing. This provides a better user experience by preventing a blank space.  To specify a placeholder, add a child element with the `placeholder` attribute. Learn more in [Placeholders & fallbacks]({{g.doc('/content/docs/design/responsive_amp/placeholders.md', locale=doc.locale).url.path}}).

```html hl_lines="6"
<amp-ad type="a9"
    width="300" height="250"
    data-aax_size="300x250"
    data-aax_pubname="test123"
    data-aax_src="302">
   <amp-img placeholder src="placeholder-image.jpg"></amp-img>
</amp-ad>
```

### Step 6: (Optional) Specify a fallback

Depending on the ad network, you can choose to show a fallback element if no ad is available to serve. To specify a fallback, add a child element with the `fallback` attribute. Learn more in [Placeholders & fallbacks]({{g.doc('/content/docs/design/responsive_amp/placeholders.md', locale=doc.locale).url.path}}).

```html hl_lines="6"
<amp-ad type="a9"
    width="300" height="250"
    data-aax_size="300x250"
    data-aax_pubname="test123"
    data-aax_src="302">
   <amp-img fallback src="fallback-image.jpg"></amp-img>
</amp-ad>
```

Congratulations! You are now serving ads on your AMP page!

## Serving direct-sold AMPHTML ads

The [`amp-ad`](/docs/reference/components/amp-ad.html) component serves ads from the network you specify.  Those ads can be standard HTML ads or AMPHTML ads, provided that the ad network supports AMPHTML ads. To serve your direct-sold ads as AMPHTML ads, create the ad in AMP HTML according to the [AMPHTML ad spec]({{g.doc('/content/docs/ads/a4a_spec.md', locale=doc.locale).url.path}}) requirements and use an [ad server that serves AMPHTML ads](https://github.com/ampproject/amphtml/blob/master/ads/google/a4a/docs/a4a-readme.md#publishers).

## Augmenting targeting data on ad requests

As part of the Fast Fetch serving mechanism, the Real-Time Config (RTC) feature allows publishers to augment ad requests with first-party and third-party targeting information that's retrieved at runtime. RTC allows up to 5 callouts to targeting servers for each individual ad slot, the results of which are appended to the ad request.  To use RTC on your ads, the ad network you use must support RTC and Fast Fetch.

You can learn more about RTC from this YouTube video:

{{ youtube('mvAmvKiWPfA', 480, 270, caption='Watch Effective AMP Monetization with Header Bidding.') }}

Or, learn more from these RTC resources:

*   [AMP RTC publisher implementation guide](https://github.com/ampproject/amphtml/blob/master/extensions/amp-a4a/rtc-publisher-implementation-guide.md)
*   [AMP Real Time Config](https://github.com/ampproject/amphtml/blob/master/extensions/amp-a4a/rtc-documentation.md)


## Best practices

Here are some tips to maximize the effectiveness of ads on your AMP pages:


### Placement & controls: optimize your ad placements

*   **Place the same number of ads** on AMP Pages as your non-AMP pages to generate maximum revenue per page.
*   **Place the first ad immediately below the first viewport** ("below the fold") to provide an optimal user experience.
*   Unless you're using advanced CSS or media queries, **ensure your ad units are centered on the page** to provide your users with an optimal mobile web experience.
*   Enable [multi-size ad requests](https://github.com/ampproject/amphtml/blob/master/ads/README.md#support-for-multi-size-ad-requests) on your AMP inventory to increase ad auction pressure and drive revenue.

### Demand & pricing: get the right price for your ads

*   **Sell ad units on your AMP pages across all sales channels**, including direct and indirect to maximize competition for your inventory on AMP pages.
*   **Price your ad inventory on AMP pages** similar to your inventory on non-AMP pages. Monitor performance and adjust pricing accordingly.
*   **Ensure all ad demand channels are competing** for ad inventory on your AMP pages to drive up competition.

### Ad types: Serve the best types of ads

*   **Avoid heavy creatives** per [IAB guidelines](http://www.iab.com/wp-content/uploads/2015/11/IAB_Display_Mobile_Creative_Guidelines_HTML5_2015.pdf).
*   **Avoid interstitials** or other ad formats that cause the content to reflow on ad load.
*   **Optimize for viewability** by setting the data-loading-strategy to prefer-viewability-over-views.
*   **Place ads in your video content** via [supported players](/docs/reference/components.html#media) or [amp-iframe](https://ampbyexample.com/components/amp-iframe/) to enable revenue on all types of content.
*   **Implement native ads** to compete with display ads using multi-sized ad requests, adding demand pressure while providing your readers with a premium user experience.

### Innovation: Offer the most engaging ad products

*   **Implement ads on ancillary AMP pages** to generate incremental revenue:
    *   [Ads in a carousel](https://ampbyexample.com/amp-ads/advanced_ads/carousel_ad/)
    *   [Ads in a lightbox](https://ampbyexample.com/amp-ads/experimental_ads/lightbox_ad/)
    *   ... and [more](https://ampbyexample.com/amp-ads/#amp-ads/advanced_ads)
*   **Implement new formats for direct sold ads** to equip your sales team with high-impact, innovative ad products:
    *   [Sticky Ads](https://ampbyexample.com/components/amp-sticky-ad/)
    *   [Flying Carpet](https://ampbyexample.com/components/amp-fx-flying-carpet/)

## Additional resources

*   [AMPHTML ad templates](https://ampbyexample.com/amp-ads/#amp-ads/advanced_ads)
*   [Demo: Shows how to add amp-ad to your AMP page](https://ampbyexample.com/components/amp-ad/)
