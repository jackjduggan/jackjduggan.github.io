---
layout: post
title: 'Feature Toggles in React: Integrating Unleash with a Focus on Security'
---

"*We use feature toggles to allow us to avoid maintaining multiple branches..*" my interviewer and future manager continued. I sat in an attentive trance, nodding my head, trying not to let it be known that I had absolutely no idea what he was talking about. Later that day when I reflected on what had been an overall positive call, that term sat lurking in my mind. Feature toggles. It was something I'd never heard of before; not in college, nor on my internship. I said to myself I'd Google it later, and then promptly forgot all about it.

Until I got the call, got the job, and got my first ticket: A simple ReactJS code change, replacing some methods, nothing complex. "Oh, and of course you should look to wrap this change in a toggle". My ears pricked. "Oh, and we haven't used feature toggles in the React app before, there's another challenge for you: try and integrate Unleash".

## Unleash

Let's start by installing a local version of Unleash 

`git clone git@github.com:Unleash/unleash.git`\
`cd unleash`\
`docker compose up -d`

## Early Implementation Mistakes
I was eager to jump straight in, and probably a little naive. I did a quick Google: "React Unleash integration" and say that Unleash had an SDK and setup guide specifically for React. Score! I watched a [YouTube video from the official Unleash channel](https://www.youtube.com/watch?v=-VzI0wqLDuw) and followed along.

I'll quickly showcase the process involved in doing this, and then explain why I believe you should **not** follow this approach when configuring feature toggles in a React app.

`npm install @unleash/proxy-client-react unleash-proxy-client`\
or\
`yarn add @unleash/proxy-client-react unleash-proxy-client`

In your top level component, typically `src/index.tsx`, import the `<FlagProvider>`.

{% highlight typescript %}
import { FlagProvider } from "@unleash/proxy-client-react";
{% endhighlight %}

Paste in the configuration object, replacing the `url` attribute with the address of your local Unleash instance (will likely be the same as the default). Paste your client-side API token as a value for `clientKey`. Leave the `refreshInterval` as is, and provide an arbitrary `appName`.

{% highlight typescript %}
const config = {
    url: "http://localhost:4242/api/frontend", // Your local instance Unleash API URL
    clientKey: "<client_key>", // Your client-side API token
    refreshInterval: 15, // How often (in seconds) the client should poll the proxy for updates
    appName: "cypress-realworld-app", // The name of your application. It's only used for identifying your application
};
{% endhighlight %}

Lastly, wrap the `<FlagProvider>` around the `<App />` component.

{% highlight typescript %}
<FlagProvider config={config}>
    <App />
</FlagProvider>
{% endhighlight %}