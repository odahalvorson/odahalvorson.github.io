# pingloop.me

Static marketing site for PingLoop. No build step, no dependencies.

## Files
- index.html, about.html, pricing.html, contact.html, privacy.html, terms.html, 404.html
- assets/styles.css, assets/favicon.svg
- robots.txt, sitemap.xml

## Before you deploy — replace every [BRACKETED] placeholder
- [YOUR LEGAL COMPANY NAME]  (or your own name if not incorporated)
- [YOUR FULL NAME], [CITY, COUNTRY], [DATE]
- The LinkedIn URL in about.html
- The "Where we are today" paragraph in about.html — make it accurate

## Deploy on AWS (recommended: S3 + CloudFront, HTTPS + custom domain)

1. Create an S3 bucket named `pingloop.me`.
2. Upload every file, keeping the `assets/` folder structure.
3. Enable Static website hosting on the bucket (index: index.html, error: 404.html).
4. Request a public TLS certificate in AWS Certificate Manager in **us-east-1** for
   `pingloop.me` and `www.pingloop.me`.
5. Create a CloudFront distribution pointing at the S3 website endpoint.
   Set the alternate domain names and attach the certificate.
   Set the default root object to `index.html`.
   Add a custom error response: 404 → `/404.html`, status 404.
6. In your .me DNS, point the apex and www to CloudFront (Route 53 alias records
   if the domain is in Route 53, otherwise CNAME for www and an ALIAS/ANAME for apex).
7. Add a CloudFront Function or S3 redirect so HTTP → HTTPS.

## Faster alternative
AWS Amplify Hosting: connect a Git repo, it handles HTTPS, domain and deploys on push.

## After deploy, verify
- https://pingloop.me loads with a padlock
- https://www.pingloop.me redirects to the apex (or vice versa — pick one)
- Every nav link and footer link works
- admin@pingloop.me receives mail (test it)
- https://pingloop.me/robots.txt and /sitemap.xml resolve
