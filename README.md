> 🌐 **Language:** [🇻🇳 Tiếng Việt](./README_vi.md) · 🇬🇧 English (current) · [🇯🇵 日本語](./README_ja.md)

# GP247 Documentation (gp247-docs)

## Introduction
This is the shared documentation repo of GP247 and S-Cart. **GP247** is an open-source ecosystem on Laravel for building
business web applications. **S-Cart** is free, open-source e-commerce software built on GP247 and Laravel.

This page is the **index** listing all documents in the repo with links to each one, grouped by topic: installing & updating,
command line, API, MCP, security, SEO, backup & restore, extensions, releases, system, S-Cart, multi-store & marketplace,
purchasing & cash flow (InOut).

New to GP247? Read [About GP247](./about/gp247.md).

## Document list

### Installing & updating
| Document | Summary | Last updated |
| --- | --- | --- |
| [Installing GP247 and S-Cart](./install-upgrade/install.md) | New site: choose a package set (S-Cart, GP247 CMS, core only, inside a Laravel project); Composer, Git, Docker, hosting without a command line; adding front/shop to an existing site; security tasks right after installing | 2026-11-22 |
| [Updating GP247 and S-Cart](./install-upgrade/update.md) | 3.x site to a newer release: `composer update` per package set + `gp247:update`; Docker, hosting without a command line; `--overwrite-lang`, `--publish`; plugins updated with `git pull` | 2026-11-22 |
| [Upgrading to the 3.x line](./install-upgrade/upgrade.md) | 2.1/2.2 site to 3.x with `composer require … -W`; checking plugins, testing on a copy, rolling back; 1.x/2.0 sites | 2026-11-22 |

### Command line (CLI)
| Document | Summary | Last updated |
| --- | --- | --- |
| [GP247 command line (CLI)](./cli/cli-introduction.md) | A 7-page set on the `php artisan gp247:*` commands: look up by job, safety level of each command; install & update, extensions, templates, `gp247:doctor`, maintenance (admin password, encryption key, backups), use in scripts/CI/Docker (`--json`, error codes) | 2026-11-22 |

### API
| Document | Summary | Last updated |
| --- | --- | --- |
| [GP247 API Introduction](./api/api-introduction.md) | Entry page of the API v2 documentation: quick start, concepts, sign-in, admin, storefront, sync, troubleshooting, per-endpoint reference | 2026-11-22 |
| [API v1 (no longer developed)](./api/api-v1.md) | The old API for apps written before v2: endpoint list, turning it on, moving to v2 | 2026-11-20 |
| [How to build an API correctly](./api/create-api.md) | How to write a new API endpoint the GP247 way | 2026-11-02 |

### MCP (AI agents)
| Document | Summary | Last updated |
| --- | --- | --- |
| [Introduction to the MCP server](./mcp/mcp-introduction.md) | Entry page of the MCP documentation: let AI agents (Claude, Cursor, VS Code…) work with your shop — quick start, catalogue of 18 tools, security & permissions, administration & setup, troubleshooting | 2026-11-22 |

### Security
| Document | Summary | Last updated |
| --- | --- | --- |
| [GP247 system security](./security/security-introduction.md) | Entry page of the Security documentation: what GP247 handles and what you must do — production configuration, encryption keys & backups, accounts & permissions, updates & incident response, checklist and common mistakes | 2026-11-22 |

### SEO
| Document | Summary | Last updated |
| --- | --- | --- |
| [SEO in S-Cart](./seo/seo-introduction.md) | Entry page of the SEO documentation: what the system does by itself, store-wide settings (Google/Bing verification, robots, sitemap, title templates, IndexNow), the per-content SEO tab and automatic 301, SEO check, 404 log, AI agent, tracking code (GA4, GTM, Meta Pixel) and cookie banner, hooks for developers | 2026-11-22 |
| [SEO Pro (paid plugin)](./seo/seo-pro.md) | Bulk SEO editing, Google Search Console figures in the admin, 301 suggestions for 404 pages, broken-link finder, Google Shopping data; comparison with the built-in SEO, how to connect and limits | 2026-11-22 |

### Backup & restore
| Document | Summary | Last updated |
| --- | --- | --- |
| [Backup & restore](./backup/backup-and-restore.md) | Backup password and recovery key, three ways to make a backup, automatic schedule for any hosting (no cron needed), snapshot before a change, rights and command line | 2026-11-22 |
| [External destination](./backup/backup-offsite.md) | Copy backups to S3-compatible storage or SFTP / NAS, write-only credentials + Object Lock, bring a backup back | 2026-11-07 |
| [Restore by situation](./backup/restore-guide.md) | Choose the restore level, steps on the screen, 24-hour undo, file restore, after a security incident, backups from another site | 2026-11-22 |

### Extensions (Plugins)
| Document | Summary | Last updated |
| --- | --- | --- |
| [Creating a Plugin](./extension/create-plugin.md) | Starting point: pick the right guide for your kind of plugin, a 6-step roadmap with code (settings in the database, settings screen, install, release) | 2026-11-13 |
| [Creating a payment plugin](./extension/create-payment-plugin.md) | Step by step with code: a bank transfer plugin that works right away + a skeleton for an online gateway (money recorded once, webhook) | 2026-11-22 |
| [Creating a shipping plugin](./extension/create-shipping-plugin.md) | Step by step with code: a weight-based price plugin that works right away + a skeleton for a carrier with an API (shipments, webhook, COD) | 2026-11-22 |
| [Update-safe plugins](./extension/create-plugin-update-safety.md) | How updates run, 7 rules, the `update()` hook, own data tables | 2026-11-17 |
| [Advanced plugins](./extension/create-plugin-advanced.md) | Per-store settings, secret keys, storefront pages / blocks / hooks, coupons, menus | 2026-11-17 |
| [Creating a Template (storefront theme)](./extension/create-template.md) | Build a new storefront template; the gp247/shop view fallback mechanism | 2026-11-20 |
| [Installing Plugins & Templates](./extension/install-extension.md) | 4 methods: online (library), import (.zip), manual, CLI (`gp247:ext-*`) | 2026-11-22 |
| [Updating Plugins & Templates](./extension/update-extension.md) | Update from the library (admin, command line), copy a new version over (git pull, FTP, `.zip`), fix missing or outdated files in `public/`, restore on error | 2026-11-19 |
| [Converting a Plugin from v1 to v2](./extension/convert-plugin-v1-to-v2.md) | Upgrade a plugin from Core 1.x to Core 2.0 | 2026-11-22 |

### Releases
| Document | Summary | Last updated |
| --- | --- | --- |
| [S-Cart releases and security](./release/release.md) | Recommended versions (minimum per package); highlights; how to update; S-Cart releases (each bundling core/front/shop/mcp): what is new, bug fixes, what to do when updating; security and reporting a vulnerability | 2026-11-23 |

### System
| Document | Summary | Last updated |
| --- | --- | --- |
| [GP247 v3.0 release notes — order money](./system/release-notes-3.0.md) | Upgrading from v2.1/v3.0: payment ledger per order, cash flow counted by receipt date, payment status off-by-one fixed, **discount taken before tax**; note for plugin developers | 2026-11-07 |
| [Multi-language system](./system/language-system.md) | Using languages / i18n in GP247 | 2026-11-10 |
| [Mail system](./system/mail-system.md) | Mail sending flow (with diagrams), SMTP config, channel selection | 2026-11-22 |
| [Sensitive data encryption](./system/data-encryption.md) | At-rest secret encryption (SMTP/OAuth/license); dedicated `GP247_ENCRYPTION_KEY`; **safe key-change steps** with `gp247:encryption-key-rotate`; encrypting custom columns | 2026-11-04 |
| [Scheduler & Queue](./system/schedule-and-queue.md) | schedule:run vs queue:work; per-environment cron for mail | 2026-11-07 |
| [Cache Handling](./system/cache-system.md) | Config Cache Manager screen; what is/isn't cached; version-bump; helper functions | 2026-10-22 |
| [Custom Fields](./system/custom-fields.md) | The 4 hook links; coverage limited to customer/product; dev guide to wire other tables | 2026-10-22 |
| [Layout Blocks](./system/layout-block-system.md) | How a block renders: template-first then plugin fallback, three update-safe ways to customise, how a plugin registers a block | 2026-10-22 |
| [Permissions (Permission · Role · User)](./system/permission-and-role.md) | Admin RBAC: 3 building blocks, 2 special roles, address+method gating, strategy formula | 2026-11-22 |

### S-Cart (store)
| Document | Summary | Last updated |
| --- | --- | --- |
| [Order lifecycle](./s-cart/order-processing/order-lifecycle.md) | Every stage of an order — placing, editing, receiving money, refunding, cancelling, re-opening, deleting — with stock/money/history at each, plus flow diagrams | 2026-11-22 |
| [Payment requests](./s-cart/order-processing/payment-request.md) | Money in/out outside the cart: online payment links, hand entries, refunds; 4 money flows, order/InOut/MultiVendor purposes, pay-out rights, flow diagrams | 2026-10-22 |
| [Payments in S-Cart](./s-cart/payment/payment.md) | Store setup and day-to-day use: payment gateways (test → live, webhook), the order payment ledger, COD, the instructions customers see; developers are pointed to [Creating a payment plugin](./extension/create-payment-plugin.md) | 2026-11-22 |
| [Shipping in S-Cart](./s-cart/shipping/shipping.md) | Store setup and day-to-day use: Shipping tab, pick-up warehouse, shipments, tracking, cash on delivery (since shop 3.1.4); developers are pointed to [Creating a shipping plugin](./extension/create-shipping-plugin.md) | 2026-11-22 |
| [Currency](./s-cart/tax-and-currency/currency.md) | Explicit base currency, value-preserving rebase, money-input hint (from shop 2.1) | 2026-11-22 |
| [Tax in S-Cart](./s-cart/tax-and-currency/tax.md) | How per-product tax works and how to configure it | 2026-11-22 |
| [Product Bundle (Combo)](./s-cart/product/product-bundle.md) | Create a combo product of several child products; price & stock | 2026-11-22 |
| [Product Structure (Single/Bundle/Group)](./s-cart/product/product-structure.md) | Compare the 3 product kinds with a chart; which to choose | 2026-11-22 |
| [Product stock management](./s-cart/product/product-stock-management.md) | When stock decreases/returns; over-stock config; **cancelling returns stock, deleting no longer does** (changed in v3.0) | 2026-11-22 |
| [Product Attributes (Color/Size)](./s-cart/product/product-attribute.md) | Attribute groups & values + surcharge; admin setup; price/cart/order flow; price safety | 2026-11-22 |
| [Product keyword tags (Product Tag)](./s-cart/product/product-tag.md) | Create/assign keyword tags to products; vs Delivery type; disable vs delete (from shop 2.1.6) | 2026-11-22 |
| [Duplicating products and pages](./s-cart/product/product-duplicate.md) | One button makes a switched-off copy of a product / content page; what is copied and what is not (stock, barcodes, reviews); what to do before putting it on sale (from shop 3.13.0, front 3.12.0) | 2026-11-20 |

### Multi-store & Marketplace
> The two models are **mutually exclusive** — pick one: several stores of your own (Multi-Store), or one marketplace for many sellers (Multi-Vendor).

| Document | Summary | Last updated |
| --- | --- | --- |
| [Multi-Store — many websites, one admin](./multi-store/multi-store.md) | Several stores of one business, each with its own domain/theme/language/currency: the model, features, Free/Pro comparison; index of setup, operations and customization; screenshots of the Free and Pro screens | 2026-11-22 |
| [Multi-Vendor — multi-seller marketplace](./multi-vendor/multi-vendor.md) | Turn S-Cart into a marketplace on one domain: the model, features, Free/Pro comparison, Multi-Store comparison; index of setup, operations and customization; screenshots of the Free and Pro screens | 2026-11-22 |

### Purchasing, returns & cash flow (InOut)
| Document | Summary | Last updated |
| --- | --- | --- |
| [InOut — purchases, returns, cash flow & debts](./in-out/in-out.md) | Paid plugin that adds the buying side to S-Cart: purchase orders, return orders, cash book, two-way debts, collecting/paying debts through payment requests, period closing, Excel/PDF export; index of the 5 process guides | 2026-11-22 |

---

<sub>📅 **Last updated:** 2026-11-22 · ✍️ **Author:** GP247</sub>
