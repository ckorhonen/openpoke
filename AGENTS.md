# OpenPoke agent instructions

OpenPoke has a FastAPI multi-agent backend in `server/` and a Next.js UI in
`web/`. `server/agents/`, `server/routes/`, `server/services/`, and
`server/openrouter_client/` are the backend boundaries; `web/app/` and
`web/components/` own the browser surface. Runtime data under `server/data/`
is ignored.

Use Python 3.10+, Node 18+, and npm 9+. Create a local virtual environment,
install `server/requirements.txt`, and run `npm install --prefix web`; then
start the backend with `python -m server.server --reload` and the UI with
`npm run dev --prefix web`. Starting `server.server` also starts the trigger
scheduler and important-email watcher, so use an isolated runtime with no
configured external account, or rely on explicit existing authorization for
those background actions. Keep credentials in the ignored `.env` file and
never print, commit, or substitute API values in tests or docs.

Gmail/Composio actions and background email monitoring operate on external
accounts. Do not run or broaden those paths for routine validation. Keep the
interaction/execution split, tool inputs, and API responses treated as
untrusted data; use focused tests or static checks available in the affected
package, and report an absent test command rather than inventing one.

For UI changes, run `npm run lint --prefix web` and
`npm run build --prefix web`. No automated test script is configured, so
inspect the changed UI flow and review affected Python changes directly before
completion.
