<!-- LOVABLE:BEGIN -->
> [!IMPORTANT]
> This project is connected to [Lovable](https://lovable.dev). Avoid rewriting
> published git history — force pushing, or rebasing/amending/squashing commits
> that are already pushed — as it rewrites history on Lovable's side and the
> user will likely lose their project history.
>
> Commits you push to the connected branch sync back to Lovable and show up in
> the editor, so keep the branch in a working state.
<!-- LOVABLE:END -->

- Brand images used by the app are referenced through Lovable Assets pointers; favicon and installable-app icons live in `public/` for manifest compatibility.
- Product customization is stored per product as JSON groups and suggested product IDs, while selected options are snapshotted on order items, so historic orders remain legible after menu edits.
- The legacy stacked banner carousel is not part of the customer or admin experience; promotional products remain ordinary menu categories.
- Group orders are a single delivery order with an immutable JSON allocation/payment snapshot; use shared money allocation helpers in checkout, WhatsApp, exports and courier balances to prevent discrepancies.
- Home-screen installation is manifest-only with no app-shell service worker; this preserves preview freshness and does not imply offline support.
- Keep sector page components automatically route-split and load checkout and Excel export on demand to avoid cross-sector initial payloads.
