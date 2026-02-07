[EN](./readme.md) 
[JP](./readme_jp.md)

## How to Grab the HLS/DASH URL from an e+ Streaming Page (You Still Can’t Watch)

Even if you don’t have a ticket, you can still get as far as **identifying the HLS stream URL**.  
But yeah — **you cannot actually watch the video**.

---

## Overview

On e+ (eplus) streaming pages, stream data can be fetched through their API.  
Ticket or not, the following steps let you check the **HLS (.m3u8) URL**.

---

## Steps

### 1. Check the Ticket Sales Page URL

Example:

```

https://eplus.jp/sf/detail/3480210024-P0030401P021001

```

---

### 2. Generate the Stream ID from the URL

Use the string that comes after `/detail/`.

```

3480210024-P0030401P021001

```

Convert this value into a Stream ID using the following format:

```

XXXXXX-XXXX-PXXX-XXXX-PXXX-XXX
->
XXXXXX-XXXX-XXX

```

Example:

```
348021-0024-P003-0401-P021-001
->
348021-0401-001

```

---

### 3. Access the Stream Info API

Use the generated Stream ID to hit this API endpoint:

```

https://live.eplus.jp/api/stream/{stream_id}/status

```

Example:

```

https://live.eplus.jp/api/stream/348021-0401-001/status

```

---

### 4. Get the HLS URL from the JSON Response

Inside the API response JSON, the HLS URLs are included in:

```

stream["channels"]
stream["channels_live"]

```

That’s where the `.m3u8` links live.

---

## Important Limitations

e+ streams use **CloudFront signed URLs**.  
So even if you get the HLS URL, **you can’t just play it directly**. No shortcut magic here.

The following cookies — normally issued via the official viewing page — are required:

* `Key-Pair-Id`
* `Key-Signature`
* `Key-Policy`

Without these, playback gets blocked. Straight-up denied.

If you *do* somehow know how to get around that… well, congrats I guess — you’ve basically unlocked god mode for content.

---

## Summary

| Item                          | Possible? |
|-------------------------------|-----------|
| Getting the Stream ID         | Yes       |
| Getting the HLS URL           | Yes       |
| Watching the video            | No        |
| Bypassing CloudFront signing  | No        |

---

This document is for understanding the technical structure of the streaming system.
