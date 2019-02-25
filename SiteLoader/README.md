## SiteLoader

### What is SiteLoader?

Siteloader is kind of middleware that help browser access metanet website.

A website loader prepare pages, scripts and other resources from blockchain.

Generally, a siteloader

1. Acquire latest sitemap from blockchain. 
2. Preload scripts and resources.
3. Handle path and redirection.

### Why Siteloader?

For metanet, bitcoin network itself is wrapped public database which is immutable.

It still needs abstraction and middleware to build something complicated. 

> e.g. on-chain or not on chain, you still need name service for a human readable address. 

Basically, gateways like bico.media are also siteloader, but you may want more.

And, maybe most important, siteloader can be the unchanging entrance for a metanet website.

### How to  Build/Use SiteLoader?

#### Endpoint

BitDB or Insight-api , you need decide how to access blockchain from browser.

Bisides, endpoint may not always be trustworthy, so relying a single endpoint is not recommended.

I use BitDB, cause it's easy to query, you can build and verify query on BitDB explorer.

#### Acquring Latest Sitemap

There are several  ways to acquire latest sitemap.

A basic approach is to wrap it into a signed on-chain data  that can be queried.

So the on-chain data model contains 3 parts:

1. Prefix for query, cryptic prefix or non-cryptic prefix.
2. Sitemap data, encrypted or not encrypted.
3. Signature, ECDSA or non-ECDSA.

Then you can build the OP_RETURN data model.

~~~javascript
function buildScript(prefixbuf, databuf, signaturebuf) {
    var script = bsv.Script.buildDataOut(prefixbuf)
   	script.add(databuf)
    script.add(signaturebuf)
    return script
}

function bitdbQuery(prefix){
    return {
        "q": {
          "find": { "out.s1": prefix}
        },
        "r": {
          "f": "[ .[] | {data: .out[0].s2, signature: .out[0].s3, blk:.blk.i} ]"
        }
    }
}

//Don't forget to verify signature.
//Signature should include prefix.
~~~

#### Using Sitemap

It's for your convenience that using sitemap.

Basically, you redirect browser to index page, which is quite simple. 

There are multiple approach, like iframe, document, service worker.

~~~javascript
  function renderPage (txid){
      // clean up the old page.
      document.open()
      // load new page from tx
      fetch("./"+txid).then(res=>res.text()).then(html=>document.write(html))
  }
~~~

Then you may want to preload your script. An AMD module loader may be great, but eval is ok.

~~~javascript
// Eval is OK here, for on-chain script are trustworthy.
window.eval(script)
~~~

For other resources, you may want to have a service worker, but using TXID directly is also fine.

#### Mapping URL to TXID

That will need service worker

### Demo

#### RSA-signature based Siteloader

The reason why using RSA instead of ECDSA is because 

1. BSV library is relatively heavy.
2. ASN.1 format Key is immigration candidate for traditional certificate.

##### The Siteloader

See RSA_SiteLoader.html

##### The SiteUpdater

SiteUpdater commits sitemap to blockchain.

See RSA_SiteUpdater.html

##### Secondary SiteLoader

Used as sitemap in BitDiary.

Actually is a siteloader loaded by siteloader.







































