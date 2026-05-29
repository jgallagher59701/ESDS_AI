# AGENTS.md

This file provides guidance to Codex when working with code in this repository.

## Interactions

- Do not make up data
- Talk to me directly
- Be concise and to the point
- Be critical of my requests and your own work
- Do not read the docs/study_phase_notes_jhrg.txt file

## Project Overview

ESDS_AI is a proposal to a NASA AI Innovations Call.

The Call text can be found in esds_ai_innovation_call.pdf

## Technical details

- The proposal is being written using LaTeX
- It is compiled and shared with two (maybe more) colleagues using Overleaf
- I build the PDF version of the prosal using Overleaf
- I do not have LaTeX on my computer
- My computer is a Mac running OSX 26.5 suing the Apple Silicon chips
- I can load new software using homebrew if you ask me
# OPeNDAP

Information about OPeNDAP servers may be found here:

https://www.earthdata.nasa.gov/engage/open-data-services-software/earthdata-developer-portal/opendap

# Code guidelines

- Reuse existing code when possible

## Python

Adhere to following:

- Generate methods when possible, not classes
- Include inline comments
- Use matplotlib for plotting

If you run Python code, use the "opendap" conda environment.

To interact with an OPeNDAP server, you may wish to use the pydap package.  Its documentation is located here https://pydap.github.io/pydap/en/intro.html

# Markdown

Place any documents in 'docs' in this repo.
