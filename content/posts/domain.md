---
author: "Yang Lyu"
date: 2024-05-28
title: Setting Up a New Domain for Your Netlify Website
weight: 10
---

# Setting Up a New Domain for Your Netlify Website

Setting up a custom domain for your Netlify website helps in branding and makes it easier for users to find your site. Here’s a step-by-step guide on how to set up a new domain for your Netlify website.

## Step 1: Purchase a Domain

First, you need to purchase a domain from a domain registrar. Some popular domain registrars include:
- [Namecheap](https://www.namecheap.com/)
- [GoDaddy](https://www.godaddy.com/)
- [Google Domains](https://domains.google/)

Choose a domain name that reflects your brand or website’s purpose.

## Step 2: Add a Custom Domain in Netlify

1. **Log in to Netlify**: Go to [Netlify](https://www.netlify.com/) and log in to your account.
2. **Select Your Site**: From your Netlify dashboard, select the site you want to add a custom domain to.
3. **Go to Domain Settings**: In the site dashboard, navigate to the "Domain settings" section under "Site settings."
4. **Add Custom Domain**: Click on the "Add custom domain" button and enter your purchased domain name.

## Step 3: Configure DNS Settings

1. **Access DNS Settings in Netlify**: After adding your custom domain, Netlify will provide you with DNS records that need to be added to your domain registrar.
2. **Log in to Your Domain Registrar**: Log in to the account where you purchased your domain.
3. **Find DNS Settings**: Navigate to the DNS settings or domain management section of your registrar.
4. **Add DNS Records**: Add the DNS records provided by Netlify. These typically include an A record pointing to Netlify’s IP address and a CNAME record for `www`.

### Example DNS Records
- **A Record**:
    - Name: @
    - Value: `104.198.14.52`
- **CNAME Record**:
    - Name: www
    - Value: `your-site.netlify.app`

## Step 4: Verify DNS Configuration

1. **Wait for Propagation**: DNS changes can take some time to propagate (usually up to 48 hours, but often much quicker).
2. **Check Status**: Return to the Netlify dashboard and check the status of your domain under the "Domain settings" section. Netlify will verify the DNS configuration.
3. **HTTPS Configuration**: Once your DNS is configured correctly, Netlify will automatically provision an SSL certificate for your domain, enabling HTTPS.

## Step 5: Redirect Non-www to www (or vice versa)

1. **Domain Aliases**: In the "Domain settings," you can set up domain aliases to ensure both `www.yourdomain.com` and `yourdomain.com` point to your site.
2. **Primary Domain**: Choose your primary domain in the Netlify settings to redirect traffic from the non-primary domain to the primary one.

## Conclusion

Setting up a custom domain for your Netlify website enhances your brand's credibility and makes your site more accessible to your audience. By following these steps, you can easily configure and manage your domain settings, ensuring your site is live and secure.

