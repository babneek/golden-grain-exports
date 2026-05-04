# DNS Configuration Guide for Gauri Agro Website

## Domain Setup Instructions for gauriagro.in

This document provides step-by-step instructions for configuring your domain DNS settings to point to your Vercel-hosted website.

---

## Overview

You need to add DNS records at your domain registrar (where you purchased gauriagro.in) to connect your domain to Vercel.

**Your Domains:**
- `gauriagro.in` (root domain)
- `www.gauriagro.in` (www subdomain)

---

## Step 1: Verify Domain Ownership

Before configuring DNS, you need to verify domain ownership with Vercel.

### For gauriagro.in

Add this TXT record to verify ownership:

| Type | Name | Value |
|------|------|-------|
| TXT | `_vercel` | `vc-domain-verify-gauriagro.in.9484135cca f0676f133a` |

**Note:** Remove spaces from the value when adding (shown with space for readability)

### For www.gauriagro.in

Add this TXT record to verify ownership:

| Type | Name | Value |
|------|------|-------|
| TXT | `_vercel` | `vc-domain-verify-www.gauriagro.in.0b84365bf36a0aed2df4` |

---

## Step 2: Configure DNS Records

After verification is complete, add these DNS records to point your domain to Vercel.

### Option A: Using A Records (Recommended)

Add these A records for both root domain and www subdomain:

#### For gauriagro.in (Root Domain)

| Type | Name | Value | TTL |
|------|------|-------|-----|
| A | `@` | `76.76.21.21` | 3600 |

#### For www.gauriagro.in (WWW Subdomain)

| Type | Name | Value | TTL |
|------|------|-------|-----|
| CNAME | `www` | `cname.vercel-dns.com` | 3600 |

### Option B: Using CNAME (Alternative)

If your DNS provider supports CNAME flattening for root domains:

| Type | Name | Value | TTL |
|------|------|-------|-----|
| CNAME | `@` | `cname.vercel-dns.com` | 3600 |
| CNAME | `www` | `cname.vercel-dns.com` | 3600 |

---

## Step 3: Where to Add These Records

### Common DNS Providers

#### GoDaddy
1. Log in to your GoDaddy account
2. Go to **My Products** → **Domains**
3. Click **DNS** next to your domain
4. Click **Add** to add new records
5. Select record type (A, CNAME, or TXT)
6. Enter Name, Value, and TTL
7. Click **Save**

#### Namecheap
1. Log in to Namecheap
2. Go to **Domain List** → Click **Manage** next to your domain
3. Go to **Advanced DNS** tab
4. Click **Add New Record**
5. Select Type, enter Host, Value, and TTL
6. Click the checkmark to save

#### Cloudflare
1. Log in to Cloudflare
2. Select your domain
3. Go to **DNS** tab
4. Click **Add record**
5. Select Type, enter Name, Content (Value), and TTL
6. Click **Save**

#### Google Domains
1. Log in to Google Domains
2. Click on your domain
3. Go to **DNS** in the left menu
4. Scroll to **Custom resource records**
5. Add records with Name, Type, TTL, and Data (Value)
6. Click **Add**

#### Hostinger
1. Log in to Hostinger
2. Go to **Domains** → Select your domain
3. Click **DNS / Nameservers**
4. Click **Add Record**
5. Select Type, enter Name, Points to (Value), and TTL
6. Click **Add Record**

---

## Complete DNS Configuration Example

Here's what your final DNS records should look like:

```
Type    Name        Value                                           TTL
----    ----        -----                                           ---
TXT     _vercel     vc-domain-verify-gauriagro.in.9484135ccaf0676f133a    3600
A       @           76.76.21.21                                     3600
CNAME   www         cname.vercel-dns.com                            3600
```

---

## Important Notes

### 1. **Remove Conflicting Records**
Before adding new records, remove any existing A or CNAME records for:
- `@` (root domain)
- `www` (www subdomain)

### 2. **DNS Propagation Time**
- DNS changes can take **24-48 hours** to propagate globally
- Most changes are visible within **1-2 hours**
- Use https://dnschecker.org to check propagation status

### 3. **SSL Certificate**
- Vercel automatically provisions SSL certificates
- SSL will be active within **24 hours** after DNS is configured
- Your site will be accessible via `https://gauriagro.in` and `https://www.gauriagro.in`

### 4. **Email Configuration**
If you have email services (like Google Workspace or Zoho Mail), **DO NOT remove** these records:
- MX records (for email)
- SPF records (TXT records starting with `v=spf1`)
- DKIM records
- DMARC records

Only modify A, CNAME, and the Vercel TXT verification records.

---

## Verification Steps

### 1. Check DNS Records
After adding records, verify them using command line:

```bash
# Check A record
nslookup gauriagro.in

# Check CNAME record
nslookup www.gauriagro.in

# Check TXT record
nslookup -type=TXT _vercel.gauriagro.in
```

### 2. Check in Browser
Once DNS propagates:
- Visit `http://gauriagro.in` - should redirect to `https://gauriagro.in`
- Visit `http://www.gauriagro.in` - should redirect to `https://www.gauriagro.in`
- Both should show your Gauri Agro website with SSL (padlock icon)

### 3. Check SSL Certificate
- Click the padlock icon in browser address bar
- Certificate should be issued by "Let's Encrypt" or "Vercel"
- Valid for both `gauriagro.in` and `www.gauriagro.in`

---

## Troubleshooting

### Issue: "Domain not verified" in Vercel
**Solution:** 
- Double-check TXT record is added correctly
- Wait 10-15 minutes for DNS to update
- Click "Refresh" in Vercel dashboard

### Issue: Website not loading after 24 hours
**Solution:**
- Verify A record points to `76.76.21.21`
- Verify CNAME for www points to `cname.vercel-dns.com`
- Check for conflicting records
- Clear browser cache (Ctrl+Shift+Delete)

### Issue: SSL certificate not working
**Solution:**
- Wait 24 hours after DNS configuration
- Ensure both domains are verified in Vercel
- Check that DNS records are propagated globally

### Issue: www works but root domain doesn't (or vice versa)
**Solution:**
- Ensure both A record (@) and CNAME (www) are added
- Check that both domains are added in Vercel project settings

---

## Quick Reference Card

**Copy this to your DNS provider:**

### Verification Records (Add First)
```
TXT | _vercel | vc-domain-verify-gauriagro.in.9484135ccaf0676f133a
```

### Production Records (Add After Verification)
```
A     | @   | 76.76.21.21
CNAME | www | cname.vercel-dns.com
```

---

## Support Contacts

### Vercel Support
- Documentation: https://vercel.com/docs/concepts/projects/domains
- Support: https://vercel.com/support

### DNS Provider Support
Contact your domain registrar's support team if you need help accessing DNS settings.

---

## Checklist

Use this checklist to track your progress:

- [ ] Log in to domain registrar
- [ ] Access DNS management panel
- [ ] Add TXT record for `_vercel.gauriagro.in`
- [ ] Wait for verification in Vercel (click Refresh)
- [ ] Remove conflicting A/CNAME records for @ and www
- [ ] Add A record for @ pointing to 76.76.21.21
- [ ] Add CNAME record for www pointing to cname.vercel-dns.com
- [ ] Wait 1-2 hours for DNS propagation
- [ ] Test gauriagro.in in browser
- [ ] Test www.gauriagro.in in browser
- [ ] Verify SSL certificate is active (padlock icon)
- [ ] Test on mobile device
- [ ] Confirm email still works (if applicable)

---

## Document Information

**Created:** May 4, 2026  
**Website:** Gauri Agro - Premium Basmati Rice Exporters  
**Hosting:** Vercel  
**Repository:** https://github.com/babneek/golden-grain-exports

**For technical support, contact your web developer or Vercel support.**

---

**Note:** Keep this document safe. You may need it for future reference or if you change DNS providers.
