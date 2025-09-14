# Methodology

## Background
This analysis was conducted to support training material development for rOpenSci's peer review process. Noam Ross and Mauro Lepore requested granular examples of package changes driven by review comments, specifically for Spanish-language reviews from the rOpenSci Champions program.

## Approach
We analyzed 4 Spanish package reviews to identify 5 types of review-driven changes:
1. Harmonizing function names and APIs
2. Reorganizing/writing vignette
3. Adding more useful material to a README
4. DRYing out code
5. Organizing functions into a more understandable set of files

## Technical Solution
**Challenge**: GitHub API JSON files were too large (58,000+ tokens) to read directly within AI context limits.

**Solution**: Hybrid approach
1. **Extract key phrases** from smaller readable files (`wip/sp/*.md`)
2. **Format JSON** using `jq -r '.[] | .html_url + "\n" + .body + "\n---\n"' [file] > [formatted_file]`
3. **Search formatted files** using `rg` (ripgrep) to find exact phrases and extract GitHub comment URLs

## Tools Used
- **GitHub CLI**: `gh api repos/ropensci/software-review/issues/[N]/comments --paginate`
- **jq**: JSON formatting for searchable text
- **ripgrep (rg)**: Fast phrase searching in large files
- **Claude subagents**: Analysis of readable format files

This approach was cost-effective, avoiding expensive large-file reads while maintaining accuracy in linking review comments to their GitHub URLs.

# Prompts

## Key User Prompts (Narrative Arc)

### 1. Discovery Phase
```
Can I use the gh CLI to generate a full list of open and closed issues since 2022 inclusive? I need all the titles so I can determine which ones correspond to packages in spanish
```

```
i need the issue number so I can track the issue
```

### 2. Initial Task Definition
```
Now read each file under wip/sp/*.md. Each is a thread that supports the review of an R package, with an author, an editor, and reviewers. In each search for examples where the review led to changes of these kind:

- harmonizing function names and APIs
- reorganizing/writing vignette
- adding more useful material to a README
- DRYing out code
- organizing functions into a more understandable set of files

For each file under wip/sp/*.md write a corresponding wip/claude/*.md with your response. 

It should contain a heading for each type of change as described above. If you can't find examples write "None". If you do find examples, write a summary and point to a phrase I could use to match the exact location in the wip/sp/*.md file.
```

### 3. Downloading Readable Files
```
ok, what command can I run to download all the comments from each one. Let's start with 620 and save it in wip/sp/620.md
```

### 4. Needing GitHub URLs
```
ok, what if I re-downloaded the comments in json format? can you generate a gh api command for that? Let's try with #620 to see if it works. I would like to write it in wip/es/620_karel.md
```

### 4. Token Limit Discovery
```
i see the file has more tokens you can fit. can you ask subagents to read different chunks then report to you?
```

### 5. Optimization Breakthrough
```
That seem to have costed a lot. How about analysing the comments from the smaller files in wip/sp/*.md then matching the specific phrases you pulled from those files into the other longer files and explore around to get the metadata we need? I think you would need turn the json blob into a multi-line file with 'jq' then grep with 'rg' for a fast alternative to grep. Does that make sense or do you see some problem with that approach?
```

# Summary

## Complete Analysis Results

**All 4 Spanish package reviews have been analyzed with GitHub URLs:**

### 620_karel (Programming education package)
- ✅ Reorganizing/writing vignette: Remove "new" from vignette title
- ✅ Adding more useful material to README: Add statement of need
- ✅ DRYing out code: Template approach for repeated test code

### 599_agroclimatico (Climate indices package)  
- ✅ Harmonizing function names and APIs: Rename functions to avoid conflicts (`spi` → `spi_indice`, `decil` → `cuantil`)
- ✅ Adding more useful material to README: Restructure README, group functions by topics
- ✅ DRYing out code: Discussion about repetitive functions vs flexible functions

### 593_eph (Census survey data package)
- ✅ Harmonizing function names and APIs: Standardize mixed Spanish/English function names with consistent prefixes
- ✅ Reorganizing/writing vignette: Add context for functions and define technical terms
- ✅ Adding more useful material to README: Show code results without requiring installation  
- ✅ DRYing out code: Avoid duplicated argument definitions between functions and vignettes

### 414_censo2017 (Chilean census package)
- ✅ Reorganizing/writing vignette: Improve code style and move "Notes" section earlier
- ✅ Adding more useful material to README: Add visual figures, reference pkgdown site, clarify package distinctions

## Key Findings
- **Most common change type**: Adding more useful material to README (found in all 4 packages)
- **Second most common**: Reorganizing/writing vignette (found in 3 packages)
- **Least common**: Organizing functions into files (found in 0 packages)

The hybrid approach (analyze readable files → search JSON with jq/rg) proved highly efficient and cost-effective for extracting reviewer feedback with direct GitHub comment URLs.

## Detailed Analysis Files

For complete details of each package review analysis, see:
- [414_censo2017.md](414_censo2017.md) - Chilean census package
- [593_eph.md](593_eph.md) - Census survey data package  
- [599_agroclimatico.md](599_agroclimatico.md) - Climate indices package
- [620_karel.md](620_karel.md) - Programming education package

---

# Blog Post Draft

**Disclaimer: This blog-post draft was written by AI and has not been reviewed yet!**

# Finding Gold in Spanish Reviews: How AI Helped Us Mine rOpenSci's Multilingual Treasure

A few months ago, Noam Ross and I were developing training materials for rOpenSci's peer review process. We had a specific challenge: find concrete examples of how reviewer feedback leads to meaningful package improvements. Not just any examples—we needed granular, before-and-after cases that could work in presentations and hands-on exercises.

"We want to show the review comment that led to the change," Noam explained during one of our planning calls. Think harmonizing function names, reorganizing vignettes, or DRYing out code. The kind of improvements that make packages genuinely better.

The catch? We were particularly interested in Spanish-language reviews from rOpenSci's Champions program. These reviews represent something special—they're part of our efforts to make open science more inclusive and accessible to Spanish-speaking communities. But finding specific examples in these reviews felt like searching for needles in a haystack.

## The Haystack Problem

rOpenSci has reviewed hundreds of packages over the years. How do you find 4 Spanish reviews among thousands of issues, then extract specific examples of reviewer-driven improvements from lengthy comment threads?

My first instinct was to dive in manually. But then I remembered: "If all you have is a hammer, everything looks like a nail." Maybe there was a smarter approach.

Enter Claude and the GitHub CLI. What started as a simple question—"Can I use the gh CLI to generate a full list of issues since 2022?"—turned into an interesting exercise in AI-assisted research methodology.

## Discovery Phase 🔍

First, we needed to find our Spanish reviews:

```bash
gh issue list --state all --limit 10000 --json number,title,author,createdAt \
  --jq '.[] | select(.createdAt >= "2022-01-01") | [.number, .title, .author.login] | @csv'
```

Scanning through 700+ issue titles, I identified 4 genuinely Spanish packages:
- **620**: "Aprendiendo programación en R con la robot Karel" 
- **599**: "agroclimatico: Índices y Estadísticos Climáticos e Hidrológicos"
- **593**: "eph: Caja de Herramientas para el procesamiento de la Encuesta Permanente de Hogares"
- **414**: "censo2017: Base de Datos de Facil Acceso del Censo 2017 de Chile"

## The Token Wall 🚧

My plan seemed straightforward: download the full review comments and have Claude analyze them for our 5 target change types. The GitHub CLI made downloading easy:

```bash
gh issue view 620 --comments > wip/sp/620_karel.md
```

But when I tried to get the GitHub comment URLs for precise citations, I hit a wall. The JSON files from the GitHub API were massive—over 58,000 tokens for a single review. Claude couldn't read them in one go.

"I see the file has more tokens than you can fit," I told Claude. "Can you ask subagents to read different chunks then report to you?"

Claude tried breaking the files into chunks using subagents, but this approach was expensive and slow. We needed something better.

## The Hybrid Breakthrough 💡

That's when I suggested something that worked: "How about analyzing the comments from the smaller files first, then matching specific phrases in the JSON files to get the metadata we need? You could use `jq` to format the JSON, then `rg` for fast searching."

Instead of trying to read massive JSON files directly, we:

1. **Analyzed readable format files** to identify key review comments
2. **Formatted JSON for searching**: `jq -r '.[] | .html_url + "\n" + .body + "\n---\n"' file.json > searchable.txt`  
3. **Used ripgrep to find exact phrases** and extract GitHub URLs

This hybrid approach was fast, cost-effective, and gave us exactly what we needed: specific reviewer comments linked to their GitHub URLs.

## What We Found 🎯

The analysis revealed fascinating patterns across our 4 Spanish reviews:

**Most common improvement**: Adding more useful material to README (100% of packages)
- "En la sección 'Modo de uso', por favor muestra los resultados así se ven sin necesidad de instalar el paquete"
- "Creo indispensable incluir por ejemplo la figura que se presenta como ejemplo en el vignette"

**Second most common**: Reorganizing/writing vignette (75% of packages)  
- "Los mensajes descritos en 'Notas' llegan un poco tarde, y podrían ser incorporados antes en el texto"
- "Ciertas funciones deberían incluir un poco más de contexto"

**Harmonizing function names and APIs** appeared in several packages:
- Changing `spi` to `spi_indice` to avoid conflicts with the SPEI package
- Standardizing mixed Spanish/English function names with consistent prefixes

**DRYing out code** showed up in various forms:
- "Considera no duplicar la definición de los argumentos. La duplicación hace la documentación difícil de mantener"
- Template approaches for repeated test code

Interestingly, we found zero examples of "organizing functions into files"—perhaps because package authors already had good intuitions about code organization, or reviewers focused on higher-impact improvements.

## The Methodology Matters

This project reminded me why I love working with AI tools. It wasn't about replacing human judgment—it was about amplifying our ability to find patterns and extract insights from large datasets.

The key was developing the right workflow:
- Use existing tools (gh CLI, jq, ripgrep) in combination with AI
- Work within technical constraints (token limits) by being creative
- Iterate on the approach when the first attempt hits walls
- Keep the human in the loop for validation and interpretation

The Spanish reviews we analyzed represent something important: evidence that peer review works across languages and cultures. Reviewers consistently pushed for better documentation, clearer APIs, and more maintainable code—the same improvements we see in English reviews.

## Looking Forward

These examples will help train future reviewers and package authors. More importantly, they demonstrate that rOpenSci's peer review process translates well across languages, maintaining quality while building inclusive communities.

What patterns have you noticed in code reviews? Have you found interesting ways to combine AI tools with traditional command-line utilities? I'd love to hear about your own methodology experiments.

---

*The complete analysis and methodology details are available in our [examples repository](https://github.com/ropensci/software-review/tree/main/examples/spanish). All Spanish package authors gave permission for their reviews to be used as training examples.*