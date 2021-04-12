+++
authors = ["Josh Powell"]
date = 2021-04-12T15:00:00Z
draft = true
excerpt = "Running your website in 200+ locations has never been so easy!"
hero = "/images/how-to-deploy-to-the-edge-pages-hero.png"
title = "How to deploy your website to the edge! Ft. Cloudflare Pages"

+++
Today Cloudflare have [announced ](https://blog.cloudflare.com/cloudflare-pages-ga/)that Pages, there Serverless webpage hosting service will be exiting beta and move to general release! So I thought it was about time I made a blog post on how to setup and deploy them! 

### Requirements

To setup a website on Cloudflare Pages you'll needed the following:

* A [GitHub](https://github.com/) account (other source controls are currently not supported)
* A [Cloudflare](https://cloudflare.com) account (you don't even require a domain! but I highly recommend you do)

### 1. Create a Git repository

 

### 2. Commit your website

### 3. Login to Cloudflare 

### 4. Configure Pages

### 5. Create your first Cloudflare Page!

### 6. Custom tweaks

Now there are a couple tweaks that you can apply to your workers site to make it perform that little better and more security but aren't critical to your basic Cloudflare page.

#### Page rules

#### Custom HTTP headers via Workers

Unlike your own webserver, you can't simply edit the header config on a Cloudflare page so you will need to deploy the following script on a Worker to achieve an A+ on [securityheaders.com](https://Securityheaders.com)

    javascript
    let securityHeaders = {
    	"Content-Security-Policy" : "upgrade-insecure-requests",
    	"Strict-Transport-Security" : "max-age=63072000",
    	"X-Xss-Protection" : "1; mode=block",
    	"X-Frame-Options" : "DENY",
    	"X-Content-Type-Options" : "nosniff",
    	"Referrer-Policy" : "strict-origin-when-cross-origin",
    	"Permissions-Policy": "fullscreen=(), geolocation=()",
    }
    
    let sanitiseHeaders = {
    	"Server" : "Josh",
    }
    
    let removeHeaders = [
    	"Public-Key-Pins",
    	"X-Powered-By",
    	"X-AspNet-Version",
    ]
    
    addEventListener('fetch', event => {
    	event.respondWith(addHeaders(event.request))
    })
    
    async function addHeaders(req) {
    	let response = await fetch(req)
    	let newHdrs = new Headers(response.headers)
    
    	if (newHdrs.has("Content-Type") && !newHdrs.get("Content-Type").includes("text/html")) {
            return new Response(response.body , {
                status: response.status,
                statusText: response.statusText,
                headers: newHdrs
            })
    	}
    
    	Object.keys(securityHeaders).map(function(name, index) {
    		newHdrs.set(name, securityHeaders[name]);
    	})
    
    	Object.keys(sanitiseHeaders).map(function(name, index) {
    		newHdrs.set(name, sanitiseHeaders[name]);
    	})
    
    	removeHeaders.forEach(function(name){
    		newHdrs.delete(name)
    	})
    
    	return new Response(response.body , {
    		status: response.status,
    		statusText: response.statusText,
    		headers: newHdrs
    	})
    }