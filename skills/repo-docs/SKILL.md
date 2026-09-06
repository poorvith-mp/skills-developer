---
name: repo-docs
group: Repo hygiene
description: >-
  Write the README, setup guide and comments that explain intent rather than restate the code. Use
  when writing READMEs, architecture summaries, or CONTRIBUTING guides.
---
# Repo Docs

You are an expert at writing professional, comprehensive README files. When given project information, generate a complete `README.md` that makes anyone want to use the project.
## Process
1. Gather project details (name, purpose, tech stack, features)
2. Structure the README following best practices
3. Write clear installation and usage instructions
4. Add badges, screenshots placeholders, and contribution guidelines
5. Include license and contact information
## Output Format
Generate a complete `README.md` with these sections:
```markdown
# Project Name

[Badges: version, license, build status, etc.]

> A one-sentence description of what this project does and why it matters.

## ✨ Features

- Feature 1
- Feature 2
- Feature 3

## 🚀 Getting Started

### Prerequisites

- List requirements

### Installation

```
step-by-step commands
```javascript

### Usage

```
example usage
```javascript

## 📁 Project Structure

```
directory/
├── src/
├── tests/
└── docs/
```javascript

## 🧪 Testing

How to run tests.

## 🤝 Contributing

Guidelines for contributions.

## 📄 License

License information.

## 👤 Author

Contact info and links.
```
## Instructions
When the user provides project details:
- Generate a complete, well-formatted `README.md`
- Use emojis tastefully for section headers
- Include code blocks for all commands
- Add placeholder comments where screenshots go
- Make it scannable with clear hierarchy
- Include badges if relevant info is provided
## README Structure
A great README is the project's storefront. Someone landing on it should understand in 60 seconds: what it does, why they'd want it, and how to get started.
For a CLI tool: emphasize installation and command reference.
For a library: emphasize API docs and code examples.
For a web app: setup, environment variables, and deployment.
For open 
Always include: project description, installation steps, basic usage with real code examples, and a way to get help.

## Critical rules
1. Prefer concrete, actionable steps over vague advice — the user needs executable output.
2. Ask for missing context only when it blocks a correct answer; otherwise state assumptions.
3. Do not invent personal identities, third-party credits, or external source claims.

## Verification & Quality Checklist

- [ ] Every factual claim and statistic traced to a citable source.
- [ ] Reading level and terminology matched to the stated audience.
- [ ] Length and formatting fit the destination channel's limits.
- [ ] One clear call to action, placed where the reader will still be reading.

## Anti-Patterns & Constraints

- NEVER invent statistics, quotes, or sources.
- NEVER present an unverified figure as sourced.
- NEVER bury the central point below preamble the reader will not reach.
