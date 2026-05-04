# CONFIG — aeo-content-writer
# Copy this file to CONFIG.md and fill in your values. CONFIG.md is gitignored.

SITE_URL=https://your-site.com
SITE_CONTEXT=docs/site-context.md
TONE_GUIDE_PATH=docs/tone-guide.md
AGENTS_DOC=docs/AGENTS.md

# Data sources
DATA_SOURCES=BLS,ONET   # comma-separated: BLS, ONET, custom-csv
SITE_REPO=/path/to/your/site-repo
DATA_REPO=/path/to/your/data-repo

# Output paths
BLOG_COMPONENT_DIR=src/views/blog/
BLOG_ROUTE_DIR=app/blog/

# Google Docs (optional) — paste the doc ID from the URL: docs.google.com/document/d/<ID>/edit
# Add one key per content type. The skill will append new drafts to the matching doc.
# Requires Google Drive MCP authenticated via /mcp before use.
# Pattern: GOOGLE_DOCS_[USECASE] e.g. GOOGLE_DOCS_BLOG, GOOGLE_DOCS_NEWSLETTERS
GOOGLE_DOCS_[USECASE]=
