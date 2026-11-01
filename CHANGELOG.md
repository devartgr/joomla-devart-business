# Changelog

All notable changes to this repository are documented here. Verified Joomla
runtime QA is recorded in `PROJECT_STATUS.md` after VPS confirmation.

## 1.1.9

- Businesses CSV import and export support an optional `categories` column
  (pipe-separated category id, alias, or unique title; first = primary).
- Category linking matches existing categories only; unknown or ambiguous
  tokens are skipped. Omit the column to leave links unchanged; leave it
  empty to clear them.

## 1.1.8

- Administrator forms and lists use WebAssetManager (`form.validate`, `core`,
  `multiselect`) instead of deprecated `HTMLHelper::_('behavior.*')`.
- CSV/JSON business import normalises website/social URLs via
  `ExternalUrlHelper` and filters `introtext`/`fulltext` with
  `ComponentHelper::filterText`.
- Frontend listing website links use `ExternalUrlHelper` before render.
- Listing and module primary location selection require `state = 1`, matching
  business detail.
- Module taxonomy filters use `WHERE IN` subqueries instead of `DISTINCT` for
  MySQL 8 `ONLY_FULL_GROUP_BY` safety with featured ordering.
- Categories view skips the correlated business `COUNT` when
  `show_category_business_count` is off.
- Frontend listing pagination uses a dedicated lightweight `COUNT` query
  (no display `GROUP_CONCAT` columns; location join only when filters/search
  need it).
- Category subtree expansion batches nested-set parents into one SQL query.
- `RouteHelper` memoises business/category route and path lookups per request.
- Listing filter option queries run only when the matching filter UI is enabled.
- Detail "back to results" uses a static listing URL (FPC-safe); same-origin
  `document.referrer` is applied in `site.js` when available.
- Business Settings save syncs live `ComponentHelper` params and cleans
  `com_devartbusiness`, `mod_devartbusiness`, and `_system` callback caches.
- Listing search keeps FULLTEXT boolean-mode matching in its own subquery and
  unions location prefix matches, so OR-LIKE no longer disables the FULLTEXT
  index; short terms still use title prefix + location prefix via UNION.
- Listing and module maps cap markers at 500 (`GeoHelper::MAP_MARKER_LIMIT`);
  `site.js` limits Leaflet load retries and exposes `DevartBusiness.init(root)`.
- Module uses Joomla `AbstractModuleDispatcher` + `BusinessModuleHelper` with
  `services/provider.php` instead of a procedural entry script.
- Tools diagnostics run in `ToolsDiagnosticsHelper` / Tools view (no DB queries
  in the template); failed checks log details and show a generic message.
- CSV business/category export streams in 500-row chunks; formula escaping also
  covers leading whitespace and tab/CR/LF prefixes.
- ToolsController is a thin ACL/token façade; category, import, and export logic
  live in `ToolsCategoryHelper`, `ToolsImportHelper`, and `ToolsExportHelper`.
- CSV/JSON import writes in 500-row transaction chunks; import errors log details
  and show a generic administrator message.
- Content writes clear `com_devartbusiness`, `mod_devartbusiness`, and `_system`
  callback caches via `CacheHelper` (save/delete/state/import/tools).
- Map popup links allow only http(s) URLs or same-site relative paths.
- Business detail introtext/fulltext render through `HtmlSanitizer` as
  defense-in-depth.
- Independent listing vs detail image ratios (poster/custom) in Business
  Settings Media; Image Upload Optimization fields live in Component Options.
- Overlay listing cards honour Card Background; categories view renders
  sanitized header/footer HTML from Business Settings.
- Gallery layout distinguishes grid (3 columns, 4:3) from compact (6 columns,
  1:1) via explicit CSS variables.
- Leaflet 1.9.4 is served locally from `media/com_devartbusiness/vendor/leaflet`
  (no unpkg CDN); listing/module maps initialise reliably (WAM dependency order
  plus AMD-safe dynamic load fallback).
- `DevartGalleryBridge` caches `tableExists` per request to avoid repeated
  `SHOW TABLES` probes.

## 1.1.7

- Frontend menu lookup no longer filters by `MenuItem::client_id`. Joomla
  `SiteMenu` already loads only site items and does not expose `client_id` on
  `MenuItem`, so `getItems(..., 'client_id')` triggered `Undefined property`
  warnings (same fix class as DevArt Documents / Events).

## 1.1.6

- Joomla 7 preparation: load DevArt Gallery CSS/JS and Google Maps via
  WebAssetManager instead of deprecated Document::addStyleSheet()/addScript().
- Hotfix: DevArt Gallery asset URLs use absolute Uri::root() paths so lightbox
  JS/CSS load correctly under WebAssetManager.
- Hotfix: Google Maps callback inline script uses WebAssetManager options and a
  dependency on `com_devartbusiness.google-maps` so it renders before the API.
- Joomla 8 preparation: replace Application `$app->input` magic access with
  `$app->getInput()` in frontend models, gallery bridge, and business template.

## 1.1.5

- Administrator dashboard redesigned to the DevArt hub card layout (Video/Slider
  style) with Business-specific icons and colors.
- Dashboard cards: New Business, Business list, Categories, Tags, Business
  Settings, and Options; Tools button and SEO / Structured Data block retained
  below the grid.
- Business Settings groups use bordered fieldset/legend sections matching the
  DevArt Video settings layout.
- Added frontend and administrator languages for cs-CZ, nl-NL, pl-PL, ru-RU,
  uk-UA, ja-JP, tr-TR, and zh-CN (15 locales total with existing packs).
- Language packs keep key parity with en-GB and preserve string formatting
  placeholders (`%s`, `%d`, `%1$s`, and related tokens).

## 1.1.4

- Release metadata: `creationDate` set to `2026-08-19` in package, component, and
  module manifests for GitHub release and JED submission.

## 1.1.3

- JED-FW: Removed `error_log()` fallback from tools error logging so JED Framework
  rule passes; Joomla `Log` remains the sole logging path.

## 1.1.2

- JED-LANG: Added missing `COM_DEVARTBUSINESS_IMPORT_FAILED` administrator language
  keys (7 locales).
- JED-LANG: Added base `COM_DEVARTBUSINESS_N_BUSINESSES` site language keys for
  JED `Text::plural()` scanning (7 locales).

## 1.1.1

- JED-COMP: Prefer `DatabaseInterface::class` in administrator category, settings,
  and tag controllers.
- JED-JAMSS: Render map and video embeds via JavaScript instead of literal IFRAME
  markup in PHP templates; admin map preview uses DOM APIs.

## 1.1.0

- JED-LANG: Removed duplicate `COM_DEVARTBUSINESS_MAP_PREVIEW_TITLE` keys from all
  administrator language files (7 locales).

## 1.0.37

- GAL-02: DevArt Gallery integration is consumer-only: Business delegates image
  resolution to `com_devartgallery` via `DevartGalleryBridge` instead of
  duplicating table probing or filesystem scans.
- GAL-02: Administrator gallery picker lists indexed active galleries from
  `#__devartgallery_index` (title, path, image count).

## 1.0.36

- Hotfix: Business detail hero and logo images render correctly with
  `HTMLHelper::_('image')` on root and subfolder installs.
- Hotfix: DevArt Gallery folders without `#__devartgallery_images` rows are
  scanned from disk on the business frontend (aligned with `com_devartgallery`).
- Hotfix: Gallery lightbox URLs use root-aware `devartBusinessImageUrl()`.

## 1.0.35

- Hotfix: Normalise DevArt Gallery image paths for frontend output.
- Hotfix: Preserve manual gallery media when DevArt Gallery is the active source.
- Hotfix: Respect `gallery_source` when resolving business gallery output.

## 1.0.34

- GAL-01/COMP-02: Manual gallery images from `#__devartbusiness_media` now render on
  the frontend; `gallery_source` is set to `manual` or `devart_gallery` on save.
- LANG-03: Added frontend and administrator languages for fr-FR, de-DE, es-ES,
  it-IT, and pt-PT (el-GR and en-GB unchanged).
- LANG-01: Package manifest description uses `PKG_DEVARTBUSINESS_XML_DESCRIPTION`.
- LANG-02: Removed hardcoded Greek day labels from `devartBusinessFrontendText()`.
- UX-01: Permanent delete success message counts actually deleted trashed IDs.
- COMP-01: Prefer `DatabaseInterface::class` over `DatabaseDriver` service id.
- ROUTE-01: Router logs unexpected parse errors before returning 404.

## 1.0.33

- SEC-06: Replaced regex-based settings header/footer sanitisation with shared
  `HtmlSanitizer` using Joomla `InputFilter` tag and attribute allowlists.

## 1.0.32

- DATA-07: Module random ordering and random source no longer use SQL `RAND()`.
  They shuffle a bounded recent-business pool in PHP instead.

## 1.0.31

- Hotfix: Business detail map URLs cast normalised coordinates to strings before
  `rawurlencode()`, fixing frontend HTTP 500 on business pages (L-06 regression).

## 1.0.30

- Hotfix: Restored global `translate()` scope and early Google Maps callbacks in
  administrator map preview/geocode JavaScript after 1.0.29 regression.
- ROUTE-01: Business SEF routes resolve menu-prefixed segments and return proper
  404 responses instead of silent router failures.

## 1.0.29

- LANG-01/02: Replaced hardcoded administrator dashboard, footer, module map
  loading, and geocode/map-preview JavaScript strings with language keys and
  `Joomla.Text` translations.

## 1.0.28

- L-06: Shared geo coordinate normalisation and validation in `GeoHelper` for
  administrator saves, CSV import, map rendering, and LocalBusiness JSON-LD.

## 1.0.27

- L-05: Removed the unused custom database cache table and administrator cache
  tools; frontend and module output continue to rely on Joomla-native caching.

## 1.0.26

- L-03: Added outer package `LICENSE.txt` (GPL-2.0-or-later notice) to the
  installable package root.

## 1.0.25

- DATA-02: Installer schema migrations log warnings for optional repair steps and
  fail install/update when required business/category columns cannot be added or
  inspected; duplicate-column `ADD COLUMN` attempts are treated as idempotent
  success during updates.

## 1.0.24

- M-06: Frontend listing search uses the existing business FULLTEXT index with
  boolean-mode matching; location and short-term searches use prefix matching
  instead of leading-wildcard `LIKE`.
- M-06: Category subtree expansion skips adjacency-list fallback when nested-set
  values are valid.
- M-06: Location filter options use SQL `DISTINCT` with published business
  visibility constraints.

## 1.0.23

- M-05: Component listing map uses the full filtered business dataset instead of
  the current pagination page.
- M-05: Module `source=map` loads all matching geocoded businesses without the
  list count cap.
- M-05: Shared geo coordinate validation allows equator and prime meridian values
  while rejecting invalid ranges and `(0,0)` placeholders.

## 1.0.22

- M-04: Category tree integrity via `CategoryTreeHelper` with parent validation,
  unified rebuild, Table-based duplicate, and child-safe permanent delete.

## 1.0.21

- M-03: Business image upload byte, dimension, and pixel ceilings before GD
  decode, with administrator settings and clear upload errors.

## 1.0.20

- M-02: Atomic administrator business save with transaction rollback and
  uploaded-image cleanup on failure.

## 1.0.19

- M-01: External URL and validated video embed hardening on save and render.
- M-01: JSON-LD output uses safe `json_encode` flags.

## 1.0.18

- M-08: JSON backup/restore hardening with streaming export, import limits,
  manifest version metadata, and preserved language on restore.

## 1.0.17

- M-07: CSV export spreadsheet formula injection hardening.

## 1.0.16

- M-09: Package-only Joomla update ownership; installer cleanup for stale child
  update sites.

## 1.0.15

- el-GR module administrator `sys.ini` key parity with en-GB.

## 1.0.14

- Leaflet CDN Subresource Integrity on frontend map assets.

## 1.0.12

- RB-4: Schema/update safety (`#__schemas` preservation, manifest update
  schemas, Joomla-safe update SQL).

## 1.0.10

- RB-3: Joomla 6 native APIs without Backward Compatibility plugin dependency.

## 1.0.9

- RB-2: Safe permanent delete for trashed businesses, categories, and tags.

## 1.0.8

- RB-5: Frontend listing SQL compatible with strict `ONLY_FULL_GROUP_BY`.

## 1.0.7

- Administrator featured filter and bulk feature/unfeature actions.

## 1.0.6

- SEF menu routing for business listing root URLs.

## 1.0.5

- Safer module cache context defaults.

## 1.0.3 through 1.0.4

- RB-1: Unified public visibility enforcement for access, language, and
  publication windows across component, router, and module output.

## Repository baseline

- Migrated repository development to the DevArt Business `source/` tree.
- Aligned package, component, and module metadata with Joomla 6+ and PHP 8.3+.

## Documentation alignment

- DOC-02 (`1.0.33`): `docs/current-state.md`, `README.md`, and `qa/checklist.md`
  aligned with the verified `1.0.33` audit-complete baseline.
- PHP 8.4/8.5 local Herd production certification recorded in `qa/checklist.md`
  and `PROJECT_STATUS.md` (August 2026).

## Open backlog (not yet closed)

- None. Optional production certification (PHP 8.4/8.5 matrix, large-directory
  profiling) remains advisory.
