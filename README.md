# github-workflow-as-kube

 [![Latest Release](https://img.shields.io/github/v/release/kerthcet/github-workflow-as-kube?include_prereleases)](https://github.com/kerthcet/github-workflow-as-kube/releases/latest)

## Commands

This workflow following [Kubernetes habits](https://prow.k8s.io/command-help?repo=kubernetes%2Fkubernetes), offering commands:

| Name | Add | Remove | Note |
| ---- | ----- | ----- | -----|
| Good First Issue | /good-first-issue | /remove-good-first-issue | |
| Help | /help | /remove-help | |
| LGTM | /lgtm | /lgtm cancel | |
| Approve | /approve | /approve cancel | Only approvers have the privilege |
| Hold | /hold | /hold cancel | PR will not be merged once hold |
| Category | /kind feature | /remove-kind feature | Support kinds: `feature`, `cleanup`, `bug`, `documentation` and so on... |
| Assignment | /assign @_somebody_ | /unassign @_somebody_ | When @nobody, will assign/unassign to the commenter |
| Review Request | /cc @_somebody_ | /uncc @_somebody_ | When @nobody, will cc/uncc the commenter |
| Priority | /priority backlog | /remove-priority backlog | Support priorities: `important-critical-urgent`, `important-soon`, `important-longterm`, `backlog`, `awaiting-more-evidence` |
| Title | /retitle _title_name_ | No OP | |
| Lifecycle | /reopen | /close | Authors and collaborators on the repository can trigger this command |
| Milestone | /milestone v0.0.1 | /milestone clear | Create the milestone labels manually in advance |
| Triage | /triage needs-information | /triage accepted | triage accepted will remove the `needs-triage` label |
| WIP | /wip | /wip cancel | |
| API Change | /kind api-change | /remove-kind api-change | |
| ReTest | /retest | No OP | rerun all the failed tests, use `/retest all` to rerun all tests |

**NOTE**: PR will be auto-merged once have `lgtm`, `approved` and no `do-not-merge/*` labels and all the workflow checks are passed like the ci tests.

## How To Use

To use the workflow, you have to:

- Provide a [OWNERS](./OWNERS) file, only the approvers have the privilege to tag `/approve` or `/approve cancel`
- Provide a github [secret](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions) with the name of `AGENT_TOKEN`, it should have right permissions, like owning the privilege to create labels, which is required below.
- Add the token owner to the repo's `Collaborators and teams` with written role.
- Add the [init-workflow](./examples/kube-workflow-init.yaml) to your project under the path of `.github/workflows/`, then run the workflow manually, which will help you finish the setup, like creating necessary labels.
- Add the [workflow](./examples/kube-workflow.yaml) to your project under the path of `.github/workflows/`.

Then it should work now.

## Other workflows

We support other workflows as well, you can select as your needed:

- Golang ci workflow: running golang ci, golang tests. You should provide `make test`, `make test-integration`, `make test-e2e` primitives and do not edit the workflow name.

## Roadmap

- Dispatch reviewers
- PR review by AI agent.
- PR size detecting support
