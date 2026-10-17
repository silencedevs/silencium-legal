# Silencium legal website

Standalone, English, buildless GitHub Pages website for the Silencium Discord bot.
Dark charcoal/crimson styling, system fonts and relative links. No scripts,
framework, backend, remote assets, package installation or custom domain.

**Technical files are ready to serve. Legal documents are drafts until every TODO
is resolved, the deployed practices match the text, and the operator approves them.**

## Publish in a separate repository

1. Create a GitHub repository named `silencium-legal` under your user/organization.
2. Copy only this directory's contents into that repository's root: `index.html`,
   `privacy.html`, `terms.html`, `style.css`, `.nojekyll` and this README. Include
   the hidden `.nojekyll` file. Do not upload the Silencium workspace, scripts,
   database, administrator interface, credentials, inputs or generated artifacts.
3. Complete the checklist below, review, commit and push to `main`.
4. Open the new repository's **Settings → Pages**. Under **Build and deployment**,
   select **Source → Deploy from a branch**, branch **main**, folder **/ (root)**,
   then **Save**. No custom build workflow or Jekyll setup is needed.
5. Wait for the Pages deployment to finish. Use the published URL shown by GitHub;
   enable **Enforce HTTPS** if the setting is offered. Open both document URLs
   directly, without signing in, and verify navigation on a phone.

GitHub's branch source supports `/` or `/docs`, not an arbitrary nested directory.
This directory is a standalone publishing payload, not an instruction to enable
Pages over the current repository's root or its existing engineering `/docs`.
See [GitHub's publishing-source instructions](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).
No GitHub deployment has been performed by creating these files.

## Discord Developer Portal

Replace `USERNAME` with the account or organization that owns the legal repository.
If you choose a different repository name, replace `silencium-legal` too.

| Field | URL |
| --- | --- |
| Terms of Service URL | `https://USERNAME.github.io/silencium-legal/terms.html` |
| Privacy Policy URL | `https://USERNAME.github.io/silencium-legal/privacy.html` |
| Website (where applicable) | `https://USERNAME.github.io/silencium-legal/` |

Open your application in the [Discord Developer Portal](https://discord.com/developers/applications),
find its General Information/legal URL fields, enter the first two URLs and save.
Portal layout can change. These are public documents, not OAuth redirect URIs,
bot API endpoints or an Interactions Endpoint URL. The gateway bot does not need
a public interactions endpoint. The URLs need no account login, form submission,
JavaScript or file upload.

## Complete before publishing

Search for `TODO[` throughout the HTML. Repeated identifiers refer to the same
operator decision and must be resolved consistently across both documents.

| Placeholder | Required action |
| --- | --- |
| `OPERATOR` | Confirm legal operator/controller, required address and Silence's role. |
| `CONTACT` | Supply a working privacy/support/legal contact and any required DPO/representative contact. |
| `DATES` | Set real approval/effective/revision dates; do not use the code creation date automatically. |
| `OPERATIONS` | Confirm deployment, support, logs/monitoring, integrations and automated decisions. |
| `BASIS` | Determine/document GDPR applicability, each purpose's legal basis and any legitimate interests. |
| `RETENTION` | Choose and actually enforce category-specific retention criteria, including backups and histories. |
| `DELETION` | Establish request/identity-verification/deletion procedures, backup handling and Discord-copy limitations. |
| `HOSTING` | Identify bot hosting, recipients/processors, access and processing locations. |
| `TRANSFERS` | Confirm international transfers, applicable safeguards and how to obtain information. |
| `CHILDREN` | Confirm audience/age rules and any required guardian process. |
| `CREDITS` | Confirm free/paid arrangements, pricing/validity and any required cancellation/refund/consumer terms. |
| `CHANGES` | Establish material-change notices and effective-date/acceptance process. |
| `LAW_REVIEW` | Review liability and any governing-law/dispute language for the actual service and users. |

Implement operational promises before replacing TODOs with assurances. Have the
operator or a qualified legal reviewer check the final text. Do not represent
this draft as proof of GDPR compliance or Discord approval. After approval,
remove each draft notice from all three pages, remove remaining placeholders,
and align the landing-page wording with the finalized status. Do not merely hide
TODOs with CSS. No contact address, hosting location or retention period is invented.

## Data-handling evidence

The draft was checked against these existing files; no live database or owner
scripts were inspected:

- `tools/discord/bot.py`: slash commands, caller ID/name, ephemeral replies,
  optional registration guild ID, settings and fixed SDK logging.
- `tools/discord/download.py`: attachment metadata, bounded Discord-CDN download.
- `tools/discord/service.py`: file processing and delivery, charge/refund flow.
- `tools/web/database.py`: SQLite account/settings/policy and credit ledger schema.
- `tools/web/jobs.py`: interaction IDs, timestamps, byte counts and reservation status.
- `tools/web/compiler.py`: temporary compiler files and normal cleanup.

Important findings: guild/channel context can be received but is not an account
schema field; source/output/attachment URLs are not stored in that database;
normal temp cleanup is not secure erasure; account/job/ledger records have no
automatic expiry or self-service deletion. `/config reset` is not account deletion.
Private replies do not establish Discord's retention or guarantee confidentiality.
A provider's data handling, host logs, backups and operational sharing cannot be
proved from the application code. The TODOs deliberately preserve those unknowns.

Reference sources for review:

- [European Commission: GDPR principles and retention](https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/principles-gdpr_en).
- [European Commission: individual rights](https://commission.europa.eu/law/law-topic/data-protection/information-individuals_en).
- [EDPB: international transfers](https://www.edpb.europa.eu/sme/be-compliant/international-data-transfers_en).
- [GDPR, especially Articles 6, 12–22 and transfer provisions](https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng/).
- [Discord Terms](https://discord.com/terms), [Privacy Policy](https://discord.com/privacy)
  and [Developer Policy](https://support-dev.discord.com/hc/en-us/articles/8563934450327-Discord-Developer-Policy).
- [GitHub Privacy Statement](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement).

## Preview and update

From the Silencium repository root:

```sh
./start/legal.sh
```

Or, from this directory, run `python3 -m http.server 8766 --bind 127.0.0.1` and
open `http://127.0.0.1:8766/`. Python is only a preview server, not a deployment
requirement. GitHub Pages serves the files directly. Stop the preview with Ctrl+C.

Edit the HTML directly; shared appearance is in `style.css`. All local links are
relative, so keep filenames stable and do not introduce `/style.css` or root-based
`/privacy.html` links. Keep dates/notices consistent and update the policy when
actual data handling changes. Push the revised files to the legal repository's
publishing branch, then verify the live pages again.


## Optional repository QA

From the Silencium checkout, the existing external Playwright setup can run:

```sh
SILENCIUM_PLAYWRIGHT=/tmp/silencium-web-browser/node_modules/playwright/index.mjs \
  node tools/legal-check.mjs
bash -n start/common.sh start/website.sh start/bot.sh start/legal.sh
```

The QA server serves a temporary copy under `/silencium-legal/`, tests direct
URLs, all relative document links/fragments,320–1440px at100/200% text, keyboard
focus, reduced motion, forced colors, contrast and print. JavaScript is disabled
in the browser; the publishing payload makes no external asset requests. QA tools
are not part of the publishing payload and are not needed by GitHub Pages.
