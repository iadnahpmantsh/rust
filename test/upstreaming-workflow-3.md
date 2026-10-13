# Upstreaming workflow test 3

Fresh test commit (new SHA) to verify the upstreaming bot's approval-preview
comment now posts correctly, after two fixes:

- Self-hosted runner is missing `gh` CLI, which `upstreaming-publish.yml`
  needs for `gh api` calls on `workflow_run`/`workflow_dispatch` events.
  Fixed by installing a portable `gh` binary and wiring it into the
  runner's `.env` PATH.
- `check_runs_and_statuses()` in `src/ci/upstreaming/lib/githubutil.py` was
  picking an arbitrary (possibly stale) check-run conclusion when a SHA had
  multiple check-runs under the same name from repeated re-runs. Fixed to
  keep only the highest-`id` (most recent) run per name.

Branched from the current tip of `dummy` (not a stale ref), so this branch
carries every upstreaming/runner/CI fix made so far.
