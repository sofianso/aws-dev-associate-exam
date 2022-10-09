# Cloudfront Notes

**What is Cloudfront?**
Cloudfront is a web service that distributes content with low latency and high data transfer speeds. It can be used as `INGRESS` to upload objects or `EGRESS` to distribute content.

Cloudfront relies on 176 Edge Locations and 11 Regional Edge Caches.

**What's the difference?**

Edge Locations have a lower cache compared Regional Edge Caches meaning that when data is stored in Edge Locations, the data will "disappear" sooner. Regional Edge Caches have a higher storage cache capacity, thus making it a better option to retrieve data for when data in Edge Locations need to be refreshed or retrieved.

## Distributions & Origins

Cloudfront Origins are where the data is retrieved, for example, S3 Bucket, S3 Static Website or EC2 with ALB. Cloudfront Distribution is how they are distributed in either `Web Distribution` or `RTMP Distribution`.
