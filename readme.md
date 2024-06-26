## mailchannels(.js)

***[mailchannels announced](https://support.mailchannels.com/hc/en-us/articles/26814255454093-End-of-Life-Notice-Cloudflare-Workers) that their free tier and the API to send email from Cloudflare Workers will reach its end of life on June 30th.***

> [!NOTE]  
> This SDK is meant for Cloudflare Workers' integration of mailchannels, which doesn't require authentication.

### Setup

```bash
npm i mailchannels
```

```ts
import { sendMail } from 'mailchannels'
```

### Usage

Add the below TXT records for SPF and Domain Lock to work correctly. Replace `WORKER_ID` with either

- your unique subdomain for workers, e.g. `username.workers.dev`
- or the (sub)domain you're using for the worker, e.g. `example.com`.

| Name | Content |
| --- | --- |
| @ | v=spf1 a mx include:relay.mailchannels.net ~all |
| _mailchannels | v=mc1 cfid=`WORKER_ID` |

```ts
const { success } = await sendMail({
  subject: 'An example',
  message: 'This is an example email sent from Cloudflare Workers.',
  from: {
    name: 'You',
    email: 'you@your.domain'
  },
  to: 'somebody@some.domain'
})
```
