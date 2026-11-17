> 🌐 **Language:** [🇻🇳 Tiếng Việt](./release_vi.md) · 🇬🇧 English (current) · [🇯🇵 日本語](./release_ja.md)

# S-Cart releases and security

## Introduction
This page is for S-Cart (3.x line) **site owners and operators**: it tells you what each release brings, which version to run
and how to update. Latest release: **S-Cart 3.9.0** (2026-11-18).

## Recommended versions
Run `php artisan gp247:info` (or `composer show "gp247/*"`) and compare each line with the **Recommended minimum** column:

| Package | Recommended minimum | Latest |
| --- | --- | --- |
| gp247/core | **3.15.0** | 3.15.0 |
| gp247/front | **3.11.0** | 3.11.0 |
| gp247/shop | **3.12.0** | 3.12.0 |
| gp247/mcp | **2.0.1** | 2.1.0 |

- **Below** the "Recommended minimum" column → [update](#how-to-update) when you can.
- **At or above it** → your site has all the important improvements, even if you have not reinstalled S-Cart.
- **Third-party libraries** → also run `composer audit`; see [Third-party libraries](#third-party-libraries).

> ⚠️ **Note:** update **all the packages together**: `gp247/shop` 3.12.0 needs `gp247/front` ≥ 3.11, `gp247/front` 3.9.1 and `gp247/shop` 3.11.1 need `gp247/core` ≥ 3.14, `gp247/front` 3.8.1 and `gp247/shop` 3.10.1 need `gp247/core` ≥ 3.12.1, `gp247/front` 3.7.0 and `gp247/shop` 3.9.0 need `gp247/core` ≥ 3.11, `gp247/shop` 3.8.1 needs `gp247/core` ≥ 3.10.3, `gp247/mcp` 2.0.1 needs `gp247/core` ≥ 3.9, `gp247/shop` 3.6.0 needs `gp247/core` ≥ 3.7,
> `gp247/front` 3.2.3 needs `gp247/core` ≥ 3.2.3. Which lines are still supported: see [Support lifecycle](#support-lifecycle).

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
- **SEO tab for each piece of content** — your own Google title and description, share image, noindex, canonical *(S-Cart 3.9)*
- **Automatic 301 redirect when an address changes** — old links still take visitors to the new page *(S-Cart 3.9)*
- **SEO check and 404 log screens** — see right away what to fix, with a link to fix it *(S-Cart 3.9)*
- **Google/Bing verification, title templates, IndexNow** — step-by-step help right on the screen *(S-Cart 3.9)*

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

### S-Cart 3.7.0 — 2026-11-13
**Names and content show exactly as you type them — no more `&amp;`.**

**✨ New**
- **Text stored as typed** — product, category and page names with `&`, `<`, `"` show correctly in the admin, the storefront
  and the API; existing data is converted during the update
- **Passwords and secrets keep every character** — passwords with `& < > "` sign in; SMTP passwords and payment keys reach the
  server unchanged
- **Raw HTML output warning** — System alerts and `gp247:doctor` point to the site's own templates and plugins that print a
  variable with `{!! !!}` ([docs](../security/security-built-in.md))
- **Untrusted proxy warning** — alerts when admin pages come through a proxy missing from `TRUSTED_PROXIES`, with the value to
  add ([docs](../security/security-production-config.md))
- **Server info shows GP247 versions first** — compare with the "Recommended versions" table without the command line
- **For developers:** `gp247_text_plain()` replaces `gp247_clean()` (deprecated, removed in 4.0), escape on output with `{{ }}`;
  the REST API returns text as typed; shared write services for products, categories, brands, suppliers and customers

**🔧 Improvements:** text entered by customers and admins always shows as text on the storefront and order screens; list
sorting accepts only valid columns; `gp247:info` prints versions as tagged (3.12.1, no longer 3.12.1.0)

**📋 To do when updating**
- **Back up the database first** — `gp247:update` converts text stored HTML-encoded (`&amp;` → `&`) once; this cannot be undone
- Run `composer update`, then `php artisan gp247:update`
- Open **System alerts** (or `php artisan gp247:doctor`): change `{!! !!}` prints of variables in your own templates and plugins
  to `{{ }}`, except HTML written in the rich-text editor
- SMTP passwords or secret keys containing `& < > "` saved before this release: enter them again once
- *(Apps using the REST API)* strings now come back as typed (`&`, not `&amp;`) — the app must escape them when displaying

<sub>Includes core 3.12.1 · front 3.8.1 · shop 3.10.1 · mcp 2.0.2 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.7.0)</sub>

### S-Cart 3.6.1 — 2026-11-11
Backup and restore hardened for real sites and shared hosts — recommended update.

**✨ New**
- **Each backup group says what it holds** — the backup and restore screens show which data a group contains before you
  choose ([docs](../backup/backup-and-restore.md))
- **The restore preview says what is not brought back** — columns the site no longer has need a separate confirmation; a
  backup newer than the site names the missing updates ([docs](../backup/restore-guide.md))
- **Warning when no full backup is available** — the backup screen warns when there is no verified full backup, or it is old

**🔧 Improvements:** a restore left unfinished ends by itself and takes the site out of maintenance; backups handle large
tables without a primary key and tables of wide rows within 128 MB, and retention always keeps the newest full backup; admin
screens with file uploads no longer run out of memory

**📋 To do when updating**
- Run `composer update`, then `php artisan gp247:update`
- Verifying, unpinning and deleting backups, and saving backup settings, now ask you to confirm your sign-in; repeated wrong
  backup passwords are temporarily blocked
- *(Restoring from the command line)* a backup with columns the site no longer has: preview it, then run again with
  `--accept-column-loss`

<sub>Includes core 3.11.2 · front 3.7.1 · shop 3.9.1 · mcp 2.0.2 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.6.1)</sub>

### S-Cart 3.6.0 — 2026-11-09
**Backup and restore built into S-Cart, ready for shared hosting.**

**✨ New**
- **Encrypted backups built in** — back up one data group, several, or the whole site; each backup is checked right after it
  is made and opens only with the backup password or recovery key ([docs](../backup/backup-and-restore.md))
- **Restore just what you need** — one data group, deleted records, configuration or the whole database, with a preview and
  undo ([docs](../backup/restore-guide.md))
- **Automatic backups without cron** — run while an admin uses the admin area, or on cron when available; a quick snapshot
  is taken before `gp247:update` and before an extension update
- **Copy backups off the server** — S3-compatible or SFTP, with write-only credentials so an attacker cannot delete them
  ([docs](../backup/backup-offsite.md))
- **Password policy per account group** — set length and strength separately for admins and customers on one screen
  ([docs](../security/security-accounts-and-access.md))
- **Failed sign-ins screen** — see failed sign-in attempts and spot password guessing early
  ([docs](../security/security-built-in.md))
- **For developers:** `gp247:backup-*` commands (create, verify, restore, copy off-site); `gp247:admin-password` resets an
  admin password from the command line; plugins declare their tables in backup data groups

**🔧 Improvements:** list search boxes say which columns they search and ignore extra spaces; `gp247:install` shows the
admin sign-in details last; the Docker scheduler runs with `schedule:work`, with no extra queue worker every minute
*(running with Docker)*

**📋 To do when updating**
- Back up the database and the site folder, run `composer update`, then `php artisan gp247:update`
- Backup is **off** by default: open **Backup & restore**, set a backup password, keep the recovery key away from the server
- New installs use the command line only (`php artisan gp247:install`) — the web installer has been removed
  ([install guide](../install-upgrade/install.md))
- *(Sites installed before 3.6.0 that will copy backups to SFTP)* run `composer require league/flysystem-sftp-v3`
- *(Running with Docker)* `composer update` does not change your site files: take the new `docker-compose*.yml`, then run
  `docker compose up -d`

<sub>Includes core 3.11.0 · front 3.7.0 · shop 3.9.0 · mcp 2.0.2 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.6.0)</sub>

### Older releases
| Release | Date | Summary |
| --- | --- | --- |
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

<sub>📅 **Last updated:** 2026-11-18 · ✍️ **Author:** GP247</sub>
