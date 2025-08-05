# Vibe Hacking

This repo contains content for performing secure code review with LLMs (/vibe coding IDEs).

Currently the contents are from [Scott Behren](https://www.linkedin.com/in/scott-behrens-6bb8611/) and [Clint Gibler](https://www.linkedin.com/in/clintgibler/)'s webinar on using [Roo Code](https://github.com/RooCodeInc/Roo-Code) for performing secure code reviews, but new content may be added in the future.

## Features

The `roomodes` file in this repo contains 5 custom roles:
1. `Security Orchestrator` - Orchestrates the overall workflow and coordinates the following agents.
1. `Threat Modeler` - Creates a threat model for a code base, documenting the project's architecture, technologies used, attack surface, trust boundaries, and more.
1. `Security Scanner` - Uses automated tools (Semgrep) and LLM-driven code review to find vulnerabilities in a code base.
1. `Security Tracer` - Given a set of findings, it uses code search to determine if the findings are likely exploitable- could an attacker provide the relevant input? Does sanization occur along the exploitation path? etc.
1. `Security Reporter` - Given a set of findings that have been traced, write a report on the security assessment, include an executive summary, the scope, and a detailed write-up for each finding.


## Getting Set Up

1. Install [VS Code](https://code.visualstudio.com/) and the [Roo Code](https://roocode.com/) extension.
1. Install dependencies.
    1. Install [Semgrep](https://github.com/semgrep/semgrep) for the code scanning part of the workflow.
        * Note: If you want inter-file analysis and 1000's of additional rules, check out Semgrep Pro. 
        * The provided `.roomodes` will work regardless though.
    1. If you want to take advantage of the `Security Tracer` Roo mode, which triages findings to determine if they are real issues ("True Positives"), set up the vector database [Qdrant](https://qdrant.tech/), which you can get a free hosted account for or run locally in Docker. 
1. Configure Roo Code.
    1. In the Roo Code extension within VS Code, choose your LLM provider of choice and provide your API keys.
        * In the webinar, we used Anthropic's Claude 3.7 Sonnet.
    1. Configure [codebase indexing](https://docs.roocode.com/features/codebase-indexing) using Qdrant.
    1. Copy the `roomodes` file in this folder into the project root of the repo you're reviewing (rename it to `.roomodes`), or globally in `~/.roo/`. See the [Roo docs](https://docs.roocode.com/features/custom-modes#importexport-modes) for more info.


## Usage

Within the Roo Code extension in VS Code, when you've cloned down a repo you want to analyze, type into Roo Code:

> Perform a security assessment of path/to/repo_target

## Notes

While this repo currently contains the security analysis prompts in a `.roomodes` file, those same prompts could likely be used almost verbatim with other coding agents, such as Claude Code's [Slash commands](https://docs.anthropic.com/en/docs/claude-code/slash-commands) or [Subagents](https://docs.anthropic.com/en/docs/claude-code/sub-agents).

See also the [Google Slides](https://docs.google.com/presentation/d/156oxmY_XpF_xO7seSYo15jSfQuP3Uv4Mtah0_9ix6j4) accompanying the webinar.

Other great resources:
* Scott Behrens' blog: [The Engineer Setlist](https://theengineersetlist.substack.com/).
* Clint's newsletter: [tl;dr sec](https://tldrsec.com/), the best way to keep up with security research.

## Contributing

If you've written additional prompts or Roo modes, or have improved on the ones in the repo, feel free to open a PR, we'd love to see what you've been cooking!