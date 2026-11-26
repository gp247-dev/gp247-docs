> 🌐 **Language:** [🇻🇳 Tiếng Việt](./release_vi.md) · 🇬🇧 English (current) · [🇯🇵 日本語](./release_ja.md)

# S-Cart releases and security

## Introduction
This page is for S-Cart (3.x line) **site owners and operators**: it tells you what each release brings, which version to run
and how to update. Latest release: **S-Cart 3.12.0** (2026-11-26).

## Recommended versions
Run `php artisan gp247:info` (or `composer show "gp247/*"`) and compare each line with the **Recommended minimum** column:

| Package | Recommended minimum | Latest |
| --- | --- | --- |
| gp247/core | **3.16.0** | 3.19.0 |
| gp247/front | **3.11.0** | 3.15.0 |
| gp247/shop | **3.12.0** | 3.16.0 |
| gp247/mcp | **2.0.1** | 2.1.1 |

- **Below** the "Recommended minimum" column → [update](#how-to-update) when you can.
- **At or above it** → your site has all the important improvements, even if you have not reinstalled S-Cart.
- **Third-party libraries** → also run `composer audit`; see [Third-party libraries](#third-party-libraries).

> ⚠️ **Note:** always update **all the packages together** with the command in [How to update](#how-to-update) — Composer picks
> versions that fit each other (e.g. `gp247/shop` 3.16.0 needs `gp247/core` ≥ 3.19). Which lines are still supported: see
> [Support lifecycle](#support-lifecycle).

## Support lifecycle
| Line | Platform | Status | Security fixes until |
| --- | --- | --- | --- |
| **3.x** | Laravel 13 · PHP 8.3+ | ✅ Supported | March 2028 |
| 2.x and earlier | Laravel 12–13 | ⛔ No longer supported | — |

- **New features** go into the newest line only.
- **When a new line ships:** the previous line gets critical bug fixes for 6 more months and security fixes until the time in
  the table — never past the security support of the Laravel version that line runs on.
- **Sites still on 2.x or earlier:** they keep running but receive no more fixes. 2.1 / 2.2 sites move to 3.x with
  `composer require … -W` and `php artisan gp247:update` — see [Upgrading to the 3.x line](../install-upgrade/upgrade.md).

## Highlights
- **My data** — customers download a copy of their data and delete their own account, with time to change their mind *(S-Cart 3.12)*
- **Personal data requests** — handle every request to see or erase a customer's data on one screen, with due dates *(S-Cart 3.12)*
- **Data retention** — old data is cleaned after the number of days you set, no cron needed *(S-Cart 3.12)*
- **Province and ward picked from a list** — type to search, look up by postcode with an address plugin *(S-Cart 3.12)*

## How to update
**Step 1 —** Back up the database and the site folder.

**Step 2 —** Update the code:
```bash
composer update gp247/core gp247/front gp247/shop gp247/mcp
```
A site installed before S-Cart 3.5.0 has no MCP server yet: run `composer require gp247/mcp -W` once instead of the command above.

**Step 3 —** Apply data, configuration and cache updates:
```bash
php artisan gp247:update
```

**Step 4 —** Check the versions again with `php artisan gp247:info`.

A release may need extra steps — see its **📋 To do when updating** below.
Step-by-step details: [Updating GP247 and S-Cart](../install-upgrade/update.md).

## Releases
Newest first. An *x.**Y*** release brings new features; an *x.y.**Z*** release only fixes bugs.

### S-Cart 3.12.0 — 2026-11-26
**Customers download and delete their own data; addresses picked from a list.**

**✨ New**
- **My data** — customers download a copy of their data (a ZIP file) and delete their own account, with time to change their mind
  ([docs](../s-cart/personal-data/personal-data.md))
- **Personal data requests** — one screen for every request to see or erase a customer's data, including shoppers without an
  account through the `/privacy-request` page; overdue requests raise a warning
- **Erasing a customer erases everything** — personal data goes from every place; orders stay for the books without name or
  contact; restoring an old backup does not bring an erased customer back
- **Data retention** — abandoned carts, contact messages and old logs are cleaned after the number of days you set, no cron needed
- **Province and ward picked from a list** — customers type to search, and look up by postcode, with a country address plugin
  ([docs](../s-cart/customer-address/customer-address.md))
- **For developers:** plugins declare their tables that hold customer data so they are exported, erased and cleaned on time
  ([docs](../extension/declare-personal-data.md)); country address plugins
  ([docs](../extension/create-address-plugin.md)); the `gp247:personal-data-retention` command

**🔧 Improvements:** backups no longer pack the table copies left by an earlier restore; a plugin or template whose folder is
gone can be removed with the **Forget** button and installed again as new; Composer no longer warns that `laravel/legacy-factories` is abandoned

**📋 To do when updating**
- Run `composer update`, then `php artisan gp247:update` (creates the personal data request and retention tables; adds the customer's last sign-in column)
- Check **Security › Data retention**: the items on by default (admin activity log kept 365 days, carts 180 days…) start cleaning
  after 30 days — to keep data longer, change the days or turn the item off before then
- The admin **Delete** button for a customer now creates an erasure request that waits 3 days (it can be called off; change the days
  in **Website configuration › Personal data**)
- Link to the `/privacy-request` page from your footer or privacy policy (the page exists only when the shop sends email)
- *(Your own template)* add **My data** to the account area — the default theme and GP247-EC ≥ 1.0.7 have it
- *(Site code still calling Laravel 7 style `factory()`)* run `composer require laravel/legacy-factories`

<sub>Includes core 3.19.0 · front 3.15.0 · shop 3.16.0 · mcp 2.1.1 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.12.0)</sub>

### S-Cart 3.11.0 — 2026-11-23
**Copies no longer carry the original's SEO; new installs come named and branded S-Cart.**

**✨ New**
- **Duplicates leave SEO behind** — a copied product or page starts with an empty SEO tab, so it never reaches Google with the
  original's title ([docs](../s-cart/product/product-duplicate.md))
- **New installs named and branded S-Cart** — store name, admin, welcome text and menu set up for S-Cart; running sites unchanged
- **Save button for Custom config** — edit several rows, then save once, like the other configuration tabs
- **Facebook group in the footer** — a Facebook group icon next to Facebook in the default theme
- **For developers:** hooks for SEO plugins (content sources for the SEO check, extra JSON-LD, plugin 301s); public test suites and
  CI for core, front, shop and mcp with shared test helpers; a product built on GP247 declares its name and logo at install

**🔧 Improvements:** pages without their own description no longer repeat the store's; the SEO check runs on MariaDB; the
redirect-to-error item reports only targets still returning 404 in the last 7 days

**📋 To do when updating**
- Run `composer update`, then `php artisan gp247:update` (renames the Facebook link key to `group_url` and keeps the link you set)
- *(Custom templates)* if the Facebook link reads `fanpage_url`, read `group_url` and keep `fanpage_url` as a fallback
- *(Sites using the News plugin)* update News to 3.2.0 or later to duplicate articles

<sub>Includes core 3.18.0 · front 3.14.2 · shop 3.14.1 · mcp 2.1.1 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.11.0)</sub>

### S-Cart 3.10.0 — 2026-11-20
**Add GA4 and Meta Pixel by pasting an ID, with a cookie banner; duplicate a product in one click.**

**✨ New**
- **GA4, GTM and Meta Pixel tracking** — paste the ID; the code runs only for the cookie groups the visitor allows
  ([docs](../seo/tracking-and-cookies.md))
- **Cookie banner** — ask first, notice only, or off; visitors change their mind any time through "Cookie settings"
- **Ad revenue in GA4 and Meta** — product view, add to cart, checkout and purchase events are sent automatically
- **Security headers** — switch each header on or off and turn HSTS on step by step from the admin
  ([docs](../security/security-production-config.md#security-headers))
- **Duplicate products and pages** — one button makes a switched-off copy; change only what differs
  ([docs](../s-cart/product/product-duplicate.md))
- **Find products by name** in the admin product list; the category filter has a search box
- **For developers:** templates change the banner colours with CSS variables; import plugins write 301s from another platform's
  old addresses; plugins copy their own data when a product is duplicated ([docs](../seo/seo-for-developers.md))

**🔧 Improvements:** saving products, customers and orders no longer reports duplicate keys on sites with a lot of data; 301
redirects also work for addresses that match no page (e.g. taken from the 404 log); category pages open faster on large stores

**📋 To do when updating**
- Run `composer update`, then `php artisan gp247:update` (adds an index to the product–category table; on very large stores run
  it from the command line outside peak hours)
- After the update the site sends four security headers; if the site must be embedded (iframe) on another domain, switch
  X-Frame-Options off on the **Security headers** screen
- Tracking code and the cookie banner are **off** by default — to use them, go to **SEO › Tracking code & cookies**
  (Administrators only)
- *(Running with Docker)* take the new `docker/nginx/default.conf` from S-Cart so headers are not sent twice; if you edited that
  file, merge the change
- *(Custom templates)* keep `<x-gp247-front::meta-head>` in `<head>` to get the tracking code and the cookie banner

<sub>Includes core 3.16.0 · front 3.12.0 · shop 3.13.0 · mcp 2.1.1 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.10.0)</sub>

### S-Cart 3.9.0 — 2026-11-18
**Full SEO built in: an SEO tab for every product, automatic 301s when an address changes, an SEO check screen.**

**✨ New**
- **SEO tab for each piece of content** — your own Google title and description, share image, noindex and canonical for
  products, categories, brands and pages ([docs](../seo/seo-content.md))
- **Automatic 301 redirect when an address changes** — old links from Google, Facebook and bookmarks still take visitors to
  the new page
- **SEO check and 404 log screens** — list what is To fix / To review with a link to fix it, with a reminder in System alerts;
  AI agents can read them through MCP ([docs](../seo/seo-monitoring.md))
- **Google/Bing verification, title templates, IndexNow** right on the Meta & JSON-LD screen, with step-by-step help
  ([docs](../seo/seo-settings.md))
- **Private and filter pages hidden from Google automatically** — plus automatic hreflang and richer product JSON-LD
  ([docs](../seo/seo-automatic.md))
- **One Customize theme entry for every template** — pick a template, then open its settings page
- **For developers:** plugins/templates plug into the SEO tab, sitemap, JSON-LD and system alerts; `gp247:doctor` also prints
  package checks ([docs](../seo/seo-for-developers.md))

**🔧 Improvements:** sub-store admins can only save and delete pages, links, layout blocks, brands and categories of their own
store *(multi-store sites)*; a switched-off promotion no longer sets the selling price; the storefront shows 5 products per
row on wide screens

**📋 To do when updating**
- Run `composer update`, then `php artisan gp247:update` (creates the new SEO tables and menu)
- Grant the two new screens **SEO check** and **404 log** to admins who are not the main administrator
- *(Your own template, or an overridden `meta-head`)* follow the [template SEO contract](../seo/seo-for-developers.md#the-template-seo-contract) so robots, hreflang and verification tags are printed
- *(Sites using the News plugin)* update News to 3.1.0 or later to get the SEO tab for news

<sub>Includes core 3.15.0 · front 3.11.0 · shop 3.12.0 · mcp 2.1.0 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.9.0)</sub>

### S-Cart 3.8.0 — 2026-11-15
**Shoppers sort products their way; the extension library shows everything and which core each needs.**

**✨ New**
- **Product sorting for shoppers** — Featured, Newest, Best selling, Price low/high, Name A–Z; price sorting uses the running
  promotion price
- **Tidier product filter bar** — search and sort on one row, price range and brands on another, Enter applies the price
- **Full online extension library** — extensions that need a newer core say "Needs core X.Y+" instead of Install; group
  filters count across the whole library
- **For developers:** `gp247:shop-sample` uses the S-Cart photo set instead of random images

**🔧 Improvements:** `og:image` uses only the page image or the store's share image; extra allowed origins of the MCP server
work again; a fresh site no longer re-runs old upgrade migrations on its first `gp247:update`

**📋 To do when updating**
- Run `composer update`, then `php artisan gp247:update`
- The sample share image `org.jpg` is gone: set your own under **Website information** if you want an image when links are shared
- *(Old links with `sort_asc` / `sort_desc`)* now show the default order set in the admin

<sub>Includes core 3.14.0 · front 3.9.1 · shop 3.11.1 · mcp 2.0.3 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.8.0)</sub>

### Older releases
| Release | Date | Summary |
| --- | --- | --- |
| [S-Cart 3.7.0](https://github.com/gp247net/s-cart/releases/tag/3.7.0) | 2026-11-13 | Names and content show exactly as you type them — no more `&amp;` |
| [S-Cart 3.6.1](https://github.com/gp247net/s-cart/releases/tag/3.6.1) | 2026-11-11 | Sturdier backup and restore for live sites and shared hosting |
| [S-Cart 3.6.0](https://github.com/gp247net/s-cart/releases/tag/3.6.0) | 2026-11-09 | Backup and restore built into S-Cart, ready for shared hosting |
| [S-Cart 3.5.2](https://github.com/gp247net/s-cart/releases/tag/3.5.2) | 2026-11-07 | Improvements for sites on Docker or behind a proxy / CDN |
| [S-Cart 3.5.1](https://github.com/gp247net/s-cart/releases/tag/3.5.1) | 2026-11-05 | The admin flags unsafe settings; a simpler web installer |
| [S-Cart 3.5.0](https://github.com/gp247net/s-cart/releases/tag/3.5.0) | 2026-11-03 | Built-in MCP server: ask and manage your shop with an AI agent |
| [S-Cart 3.4.0](https://github.com/gp247net/s-cart/releases/tag/3.4.0) | 2026-11-02 | Sell through your own app and sync with your ERP over the REST API |
| [S-Cart 3.3.1](https://github.com/gp247net/s-cart/releases/tag/3.3.1) | 2026-10-29 | Contact form with an inbox; REST API switched on and off from the admin |
| [S-Cart 3.2](https://github.com/gp247net/s-cart/releases/tag/3.2) | 2026-10-23 | Japanese, standard shipping with shipments, storefront theme that updates with the package |
| [S-Cart 3.1](https://github.com/gp247net/s-cart/releases/tag/3.1) | 2026-10-03 | Payment requests outside the cart; stored passwords and payment keys encrypted |
| [S-Cart 3.0.1](https://github.com/gp247net/s-cart/releases/tag/3.0.1) | 2026-09-04 | Old `sc:*` commands removed, use the `gp247:*` commands — [command list](../cli/cli-introduction.md) |
| [S-Cart 3.0](https://github.com/gp247net/s-cart/releases/tag/3.0) | 2026-08-30 | Start of the 3.x line: a payment ledger per order, discounts taken before tax — [v3.0 notes](../system/release-notes-3.0.md) |

## Security

Keeping a site secure is more than updating — configuration, encryption keys, backups, accounts and incident response are covered in [GP247 system security](../security/security-introduction.md).

GP247 reviews security regularly, and improvements ship in every release. The simplest way to keep your site safe is to run
at least the versions in [Recommended versions](#recommended-versions) and update when a new release comes out.

## Server software (PHP, web server)
Flaws in PHP and the web server are fixed by their own vendors, not by a GP247 release — keep them up to date as well.

| Issue | Severity | Fixed in PHP |
| --- | --- | --- |
| **PHP2Shell** — remote code execution (CVE-2026-109618, CVE-2026-109619) · 2026-10-21 | Critical | 8.3.36 · 8.4.27 · 8.5.12 |

**What to do**
- **Check your PHP version:** `php -v`, or **Admin → Server info**.
- **PHP from the official releases** (php.net, the official Docker images, most control panels that let you pick a version):
  move to the fixed version of your branch, or later.
- **PHP managed by your Linux distribution (Ubuntu, Debian, RHEL…) or hosting provider:** these vendors often patch an older
  version number, so **the number alone does not tell you whether you are safe** — install the latest operating system
  updates, or ask your provider whether CVE-2026-109618 and CVE-2026-109619 are patched.
- **Cannot update yet:** set `session.upload_progress.enabled = Off` in `php.ini` (GP247 does not use this feature) and restart
  PHP. It lowers the risk; it does not replace the update.
- **Running with Docker:** follow "Security updates" in
  [DOCKER.md](https://github.com/gp247net/s-cart/blob/master/DOCKER.md).

## Third-party libraries
Flaws in libraries GP247 uses (Livewire, Symfony…) are fixed by their own maintainers; GP247 raises its minimum when needed.
GP247's own code does not use the affected features of the two flaws below, but third-party plugins may — update anyway.

| Issue | Severity | Fixed in |
| --- | --- | --- |
| **Livewire** — authorization bypass (GHSA-mhf7-xp6r-6qrc) | Medium | livewire/livewire 4.4.8 (required by core 3.10.2) |
| **symfony/mime** — email header injection (CVE-2026-45070) | Medium | symfony/mime 7.4.22 |

**What to do**
- **Update:** `composer update`, then check with `composer show livewire/livewire symfony/mime`.
- **Check every library at once:** `composer audit` lists the libraries on your site that have a published flaw.

## Reporting a vulnerability
If you find a vulnerability, please email **support@gp247.net** — **do not** open a public GitHub issue, so the problem is not
exposed before a fix is released.

---

<sub>📅 **Last updated:** 2026-11-26 · ✍️ **Author:** GP247</sub>
