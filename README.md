# gtm-adobe-client-data-layer-ga4

Client uses AEM for their website. That means they get the [Adobe Client Data Layer and its Core Components out of the box](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=en#installation-activation). 

However, the client uses GA4 and GTM. Not Adobe Launch/Analytics/CJA. Can we still leverage the integration? 

## ACDL x AEM Core Components - How does it work?
The AEM Core Components x ACDL integration means that all AEM elements will be added to the data layer as components. These components have properties like click text, click URL, and parent element. 



