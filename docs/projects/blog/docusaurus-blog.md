import GithubLinkAdmonition from '@site/src/components/GithubLinkAdmonition';

# Docusaurus Blog Portfolio

A customized Docusaurus blog portfolio set up as part of the Developer Akademie training program.

## Table of Contents

- [Overview of Changes](#overview-of-changes)
- [Quickstart](#quickstart)
- [Description](#description)
- [Further References](#further-references)

<GithubLinkAdmonition
    link="https://github.com/albert-wissigkeit/devSecOpsBlog"
    title="Github Repo"
    type="tip"
>
Checkout this repository to see the code and implementation details.
</GithubLinkAdmonition>

## Overview of Changes

1. Create a `setup-blog` feature branch with individual commits for each major step of setting up the Docusaurus blog portfolio.
2. Removed the contributing section from README.
3. Personalized site details (title, tagline, links) in `docusaurus.config.ts`.
4. Added `GIT_REPOSITORY_URL` to `example.env` and updated `docusaurus.config.ts` to use `const gitRepositoryUrl = process.env.GIT_REPOSITORY_URL` for `editUrl`.
5. Clean up footer links, add personal GitHub profile and Developer Akademie template credit and add Projects link under Docs column. Remove Community column. Also recreate copyright Infos.
6. Configured build settings to allow `core-js` and `core-js-pure` in `pnpm-lock.yaml`.
7. Authored the first Docs post featuring this Docusaurus Blog project itself and updated the `README.md`.

## Quickstart

### Prerequisites

Ensure you have the following installed:

- **Node.js** (v16 or later)
- **pnpm** (Fast, disk space-efficient package manager)

### Getting Started

1. **Clone the Repository**

```bash
git clone https://github.com/albert-wissigkeit/devSecOpsBlog .
```

2. **Install Dependencies**

```bash
pnpm install
```

3. **Start the Development Server**

```bash
pnpm start
```

> **Note:** The site opens usually automatically at `http://localhost:3000`.

## Description

This project serves as a personal developer blog and portfolio. Built with Docusaurus, it is designed to document progress, projects, and learning outcomes during the DevSecOps training at Developer Akademie.

## Further References

- [Developer Akademie](https://developerakademie.com/)
- [Docusaurus Documentation](https://docusaurus.io/docs)
- [pnpm Documentation](https://pnpm.io/motivation)
- [Node.js Documentation](https://nodejs.org/learn/getting-started/introduction-to-nodejs)
