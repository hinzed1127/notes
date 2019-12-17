# Intro

This is a quick summary of the main ideas behind web performance, as detailed by [this article](https://calibreapp.com/blog/get-started-with-performance).

## Definition

> Web performances is the speed in which the requested content is downloaded, rendered, and ready to be interacted with

**Why is this hard?**

- We have to balance **objective** metrics we choose to collect with the **subjective** experience of tthe user.
  - Metrics benchmark our assumptions, which users help validate or disprove.

**What technical things fall under web performance?**

- Front-end
  - This is what we usually think of (HTML/CSS/JS)
- Optimising queries
  - Slow searches propogate down to the website level
- App internals
  - (E.g., mobile apps)
- Other infrastructure that can have an effect
  - Hosting, CDN, etc

## Key Terms

**Paint** - Metrics that describe changes during page load

- First Paint, First Contentful Paint, First Meaningful Paint, Largest Contentful Paint, etc

**Runtime** - Derived from active on the Javascript main thread

- Heavily reliant on hardware
- Examples: Total Blocking Time, JavaScript Parse & Compile, Time to Interactive, First CPU Idle

**Request** - Size of assets, the time responses take

- Time to First Byte, Total Page Transferred, Total JavaScript Transferred, Total Image Transferred

**Byte Size** - The _uncompressed_ size of assets post-delivery to users.

- Total Page Size in Bytes, Total Image Size in Bytes, Total CSS Size in Bytes

**Lighthouse** - Web performance auditing tool from Google.

- Performance Score, Accessibility Score, SEO Score, Best Practices Score

A good starting point for metrics which balances overall performance with UX:

- Time to Interactive
- Largest Contentful Paint
- Total Blocking Time
- First Contentful Paint
- Time to First Byte
- Lighthouse Performance Score

## Biggest Performance Issues

### Javascript

JS is almost always the biggest perforance issue in a variety of ways:

- Size
  - Script download/execution are costly, moreso on mobile
  - Uncompressed is often 2-3x larger
    - Download might be faster, but execution times worsen
  - 3rd party resources are harder to optimise, if at all
  - Progressive loading
  - Manage and prioritize critical requests

## Monitoring

### Choose a monitoring tool, and stick with it.

This leads to consistency in results long term.
