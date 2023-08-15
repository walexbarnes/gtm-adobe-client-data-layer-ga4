# gtm-adobe-client-data-layer-ga4

Client uses AEM for their website. That means they get the [Adobe Client Data Layer and its Core Components out of the box](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=en#installation-activation). 

However, the client uses GA4 and GTM. Not Adobe Launch/Analytics/CJA. Can we still leverage the integration? 

## ACDL x AEM Core Components - How does it work?
The AEM Core Components x ACDL integration means that all AEM elements will be added to the data layer as components. These components have properties like click text, click URL, and parent element. 

![ACDL](https://github.com/walexbarnes/gtm-adobe-client-data-layer-ga4/blob/main/adobeDataLayer%20image.png)

When a user clicks on one of these AEM Components, a `cmp:click` event is deployed to the data layer. In that payload is a `path` to that component in the data layer. I can reference this `path` to get its information (click text, click URL, etc)

[!ACDL](https://github.com/walexbarnes/gtm-adobe-client-data-layer-ga4/blob/main/adobeDataLayer%20event%20deploy.png)

## Google Tag Manager

In GTM, I create a tag that fires on the `dl-ready` event that adds an event listener for the `cmp:click` event. When the event is triggered, this tag will take the event and its associated payload and dispatch it to Google's `dataLayer` as its own event. 

![ACDL](https://github.com/walexbarnes/gtm-adobe-client-data-layer-ga4/blob/main/Tag-ACDL-Listener.png)


Now, I can create another tag that will deliver this information to GA4. It's trigger will be the Google dataLayer's custom event `cmp:click`, since the above tag is deploying this to Googles dataLayer. Its payload will include the component's associated info - what was clicked, where it led the user, the parent element, etc. 

![ACDL](https://github.com/walexbarnes/gtm-adobe-client-data-layer-ga4/blob/main/Tag-ACDL-Delivery.png)

And now, we have fully automated click tracking across all components without any manual intervention, future proof!

![ACDL](https://github.com/walexbarnes/gtm-adobe-client-data-layer-ga4/blob/main/end-result.png)
