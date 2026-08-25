# DevArt Business for Joomla

Modern business directory package for Joomla 6, designed for companies,
municipalities, organizations, associations, tourism portals, local directories,
and high-traffic websites.

![Joomla](https://img.shields.io/badge/Joomla-6.x-blue)
![PHP](https://img.shields.io/badge/PHP-8.3%2B-green)
![Release](https://img.shields.io/badge/Version-1.1.5-orange)
![License](https://img.shields.io/badge/License-GPL--2.0%2B-red)

---

## Overview

DevArt Business is a modern Joomla 6 business directory package designed for
performance, security, stability, and scalability.

It allows administrators to create and manage professional business directories
with categories, tags, locations, galleries, maps, videos, opening hours, and
structured business information while remaining lightweight and easy to maintain.

The package includes a Joomla component and a frontend module.

---

## Features

### Business Directory

Create and manage:

- Business listings
- Categories with unlimited hierarchy
- Tags
- Locations with primary location support
- Featured businesses
- Company logos and main business images
- Contact information
- Website, email, telephone, and social links
- Business descriptions and publication windows
- Access levels and language assignments

### Maps

Integrated map support for listings, business detail pages, and the site module.

Features:

- Leaflet-based frontend maps with CDN Subresource Integrity
- Latitude and longitude with shared geo validation
- Google Maps geocoding and preview in the administrator
- Interactive location display
- Responsive map layouts

### Opening Hours

Business opening hours management.

Features:

- Per-day schedules
- Open / closed status
- 24-hour mode
- Flexible opening and closing times

### Gallery Integration

Native integration with DevArt Gallery.

Features:

- Select indexed galleries from the administrator
- Display galleries on business pages
- Consumer-only integration through DevArt Gallery APIs
- Manual gallery media support when DevArt Gallery is not used

### Videos

Business video support.

Features:

- YouTube
- Vimeo
- Validated embed rendering on the frontend

### Frontend

Included frontend views:

- Business listing with search and filters
- Business detail
- Category listing
- Tag listing

Features:

- Responsive layouts
- SEO-friendly URLs and menu routing
- Category and tag filtering
- Featured businesses
- Full-text business search
- LocalBusiness JSON-LD structured data
- Open Graph and social metadata

### Site Module

Lightweight frontend module with multiple display sources:

- Latest, featured, category, categories, tag, tags
- Single business, selected businesses, random
- Category listing and map views

### Image Upload Optimization

Built-in image optimization during upload.

Features:

- Automatic resize
- Configurable maximum width and height
- Optional WebP conversion
- JPEG and WebP quality control
- Automatic safe filename generation
- Aspect ratio preservation
- No upscaling
- Existing Media Manager images remain untouched

### Import / Export

Portable business directory management.

Features:

- CSV category import
- CSV business import
- CSV export with spreadsheet formula hardening
- Complete JSON backup with streaming export
- Complete JSON restore with import limits
- Safe validation and portable configuration

### Maintenance Tools

Built-in administrator tools.

Features:

- Category tree rebuild
- Default category installer and removal
- Import and export tools
- JSON backup and restore

### Joomla Native Updates

Supports Joomla native package updates via GitHub.

Update server:

https://raw.githubusercontent.com/devartgr/joomla-devart-business/main/update.xml

Changelog:

https://raw.githubusercontent.com/devartgr/joomla-devart-business/main/changelog.xml

Install and update with the **package ZIP** (`pkg_devartbusiness`). Component and
module always update together through the package.

---

## Included Extensions

This package installs:

- `com_devartbusiness`
- `mod_devartbusiness`

---

## Requirements

- Joomla 6.0+
- PHP 8.3.0+

---

## Languages

Packaged administrator and frontend languages (15 locales):

- en-GB
- el-GR
- fr-FR
- de-DE
- es-ES
- it-IT
- pt-PT
- cs-CZ
- nl-NL
- pl-PL
- ru-RU
- uk-UA
- ja-JP
- tr-TR
- zh-CN

---

## Performance

Designed for production environments.

Features:

- Joomla native MVC architecture
- Optimized database queries
- Cache-friendly component and module output
- Cloudflare friendly
- CDN friendly
- Large directory ready
- Low frontend overhead

Suitable for:

- Municipal directories
- Tourism portals
- Chamber of Commerce websites
- Local business guides
- Editorial websites
- High-traffic Joomla websites

---

## SEO

Built with search engines in mind.

Features:

- SEO-friendly URLs
- LocalBusiness structured data (Schema.org)
- Canonical URLs
- Open Graph metadata
- Social sharing metadata
- Clean HTML output

---

## Security Highlights

- Joomla ACL support
- CSRF protection
- Public visibility enforcement (access, language, publish windows)
- Prepared SQL statements
- Secure JSON import and export
- Safe file upload validation and image limits
- Safe output escaping and sanitised settings HTML
- Joomla native architecture

---

## Compatibility

Supported:

- Joomla 6.x
- PHP 8.3, 8.4, and 8.5
- Joomla native package updates
- Modern Joomla MVC architecture

Not supported:

- Joomla 3, 4, or 5
- PHP 7.x or PHP 8.0–8.2

Optional integration:

- DevArt Gallery (`com_devartgallery`) when gallery features are used

---

## Current Version

1.1.5

---

## What's New in 1.1.5

Administrator UX polish and expanded language coverage for production
deployments.

### Added

- DevArt hub-style administrator dashboard (New Business, Business list,
  Categories, Tags, Business Settings, Options)
- Business Settings option groups with bordered fieldset / legend sections
- Languages: cs-CZ, nl-NL, pl-PL, ru-RU, uk-UA, ja-JP, tr-TR, zh-CN
  (15 locales total)

### Improved

- Language packs keep en-GB key parity and preserve string formatting
  placeholders (`%s`, `%d`, `%1$s`, and related tokens)

### Notes

- Install or update with the package ZIP once; later updates use Joomla native package updates
- Requires Joomla 6.0+ and PHP 8.3.0+
- First public release: 1.0.2 (June 2026)

---

## Author

Kostas Stathopoulos  
DevArt

https://devart.gr

GitHub repository:

https://github.com/devartgr/joomla-devart-business

---

## License

GNU General Public License version 2 or later (GPL-2.0-or-later)

---

## Disclaimer / Limitation of Liability

This software is provided "as is", without warranty of any kind.

DevArt shall not be held liable for any damages, data loss, downtime, security
incidents, business interruption, loss of profits, or other consequences arising
from the use or inability to use this software.

Always test updates in a staging environment before deploying to production
systems.

---

## Development

This repository is the source of truth for DevArt Business.

- Editable source: `source/`
- Generated packages: `builds/`
- Operational status: `PROJECT_STATUS.md`

Validate and build:

```shell
php scripts/validate.php
php scripts/build.php
```

Manual QA template: `qa/checklist.md`
