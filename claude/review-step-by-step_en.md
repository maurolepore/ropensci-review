# rOpenSci Software Peer Review: Step-by-Step Process

## Main Roles

1. **[Author](https://devguide.ropensci.org/softwarereview_author.html)** - Person who creates and submits the package
2. **[Editor](https://devguide.ropensci.org/softwarereview_editor.html)** - Manages the review process for a specific package
3. **Editor-in-Chief (EIC) / Lead Editor** - Assigns editors to submissions, handles scope questions
4. **[Reviewers](https://devguide.ropensci.org/softwarereview_reviewer.html)** (2 per package) - Volunteers who review the package
5. **Bot** (@ropensci-review-bot) - Automated system that runs checks and manages workflow
6. **Community Manager** - Invites participants to Slack community

## Step-by-Step Process

### Phase 1: Pre-Submission (Optional)
1. **Author** considers if their package is mature enough and [in scope](https://devguide.ropensci.org/softwarereview_policies.html#package-categories)
2. **Author** may open a [pre-submission inquiry issue](https://github.com/ropensci/software-review/issues/new/choose) to ask editors if package fits scope
3. **EIC** or **Editor** responds about scope fit

### Phase 2: Submission
1. **Author** creates a [new issue](https://github.com/ropensci/software-review/issues/new/choose) in `ropensci/software-review` repository using submission template
2. **Bot** automatically:
   - Posts welcome message with help command
   - Runs comprehensive [`pkgcheck`](https://docs.ropensci.org/pkgcheck/) analysis
   - Posts detailed report including:
     - Package dependencies analysis
     - Statistical properties and percentiles
     - Interactive network visualization of function calls
     - goodpractice results
     - R CMD check results
     - Test coverage analysis
     - Cyclocomplexity checks
     - Lintr results
     - "Editor-in-Chief Instructions" summary
3. **EIC** reviews the submission and bot report
4. **EIC** assesses if package is in scope
5. **EIC** may discuss scope with editorial board on Slack if unclear
6. If out of scope, **EIC** responds explaining why and closes issue
7. If in scope, **EIC** assigns an **Editor** with command: `@ropensci-review-bot assign @username as editor`
8. **Bot** confirms assignment and adds label `1/editor-checks`

### Phase 3: Editor Initial Check (~1-2 weeks)
1. **Editor** uses the [**editor template**](https://devguide.ropensci.org/editortemplate.html) as checklist
2. **Editor** reviews the automated pkgcheck report in detail
3. **Editor** checks if package meets minimum criteria and scope
4. **Editor** may request changes before seeking reviewers
5. If package doesn't pass checks, **Editor** asks **Author** to fix issues
6. **Author** makes fixes and **Editor** (or anyone) can re-run checks with: `@ropensci-review-bot check package`
7. **Editor** posts their editorial assessment using editor template
8. **Community Manager** invites **Editor** and **Author** to rOpenSci Slack

### Phase 4: Finding Reviewers (~2 weeks)
1. **Editor** asks **Author** to suggest 3 potential reviewers (may use 0-1 of them)
2. **Editor** searches for 2 reviewers from:
   - Reviewer volunteer database
   - Package dependencies/reverse dependencies authors
   - People active in relevant domains
   - Author suggestions (use sparingly)
3. **Editor** contacts potential reviewers (via email or GitHub)
4. **Editor** uses [review request template](https://devguide.ropensci.org/reviewrequesttemplate.html)
5. **Potential reviewers** check for [conflicts of interest](https://devguide.ropensci.org/softwarereview_policies.html#coi) using COI guide
6. **Reviewers** accept or decline within a few days
7. **Editor** assigns reviewers with: `@ropensci-review-bot assign @username as reviewer`
8. **Bot** automatically:
   - Adds reviewer to reviewers list
   - Sets due date (typically 3 weeks out)
   - Posts welcome message with link to [reviewer guide](https://devguide.ropensci.org/softwarereview_reviewer.html)
   - Asks reviewer to fill out reviewer form (Airtable)
   - Updates issue labels when 2 reviewers assigned
9. **Editor** can modify due dates with: `@ropensci-review-bot set due date for @username to YYYY-MM-DD`
10. **Community Manager** invites **Reviewers** to rOpenSci Slack

### Phase 5: Review (~2-3 weeks per reviewer)
1. **Reviewers** examine the package independently
2. **Reviewers** use the [**review template**](https://devguide.ropensci.org/reviewtemplate.html) as checklist
3. **Reviewers** check:
   - Code quality and style
   - Documentation completeness
   - Test coverage
   - Usability and API design
   - Compliance with [rOpenSci packaging standards](https://devguide.ropensci.org/pkg_building.html)
4. **Bot** sends reminder when due date approaches (e.g., "2 days left")
5. **Reviewers** post their reviews as comments on the GitHub issue
6. **Editor** logs each review with: `@ropensci-review-bot submit review <url> time <hours>`
7. **Bot** records review hours for each reviewer
8. **Reviewers** can make pull requests with fixes (optional, ~20% do this)

### Phase 6: Author Response (~2-3 weeks)
1. **Author** reads both reviews
2. **Author** responds to each point raised
3. **Author** makes changes to package
4. **Author** explains decisions if not implementing suggestions (dialogue, not commands)
5. **Author** pushes updates to GitHub
6. **Author** comments on issue when ready for re-review

### Phase 7: Iteration (Variable)
1. **Reviewers** check author's responses and updates
2. **Reviewers** may request additional changes
3. **Author** makes more updates
4. **Process repeats** until reviewers are satisfied
5. **No rejection** - process continues until package meets standards

### Phase 8: Approval
1. **Reviewers** use [approval template](https://devguide.ropensci.org/approval2template.html) to formally approve
2. **Reviewers** post approval comments
3. **Editor** confirms all issues addressed
4. **Editor** runs final approval with: `@ropensci-review-bot approve <package-name>`
5. **Bot** automatically posts comprehensive TODO list for author including:
   - Repository transfer instructions
   - Post-transfer finalization command
   - Links fixing instructions
   - Code of conduct file removal
   - pkgdown website migration options
   - Badge updates
   - Version increment instructions
   - [Codemeta](https://codemeta.github.io/) generation
   - [R-universe](https://ropensci.org/r-universe/) installation instructions
   - Reviewer acknowledgment instructions
   - Blog post invitation
   - Links to post-onboarding guides
6. **Bot** sends repository transfer invitation to author
7. **Package is accepted** into rOpenSci

### Phase 9: Post-Acceptance - Repository Transfer
1. **Author** must enable two-factor authentication (2FA) on GitHub account
2. **Bot** invitation expires after 1 week (can renew with: `@ropensci-review-bot invite me to ropensci/<package-name>`)
3. **Author** transfers repository to `ropensci` organization via GitHub Settings
4. **Author** notifies bot with: `@ropensci-review-bot finalize transfer of <package-name>`
5. **Bot** completes transfer:
   - Makes `<package-name>` team owner of repository
   - Invites author to the team
   - Restores admin access to author

### Phase 10: Post-Acceptance - Finalization
1. **Author** completes TODO checklist:
   - [x] Fix all links to point to ropensci organization
   - [x] Delete existing CODE_OF_CONDUCT file ([rOpenSci's applies](https://ropensci.org/code-of-conduct/))
   - [x] Decide on pkgdown website (keep own or migrate to docs.ropensci.org)
   - [x] Update CI/coverage badges to new URLs
   - [x] Increment package version
   - [x] Update NEWS.md with changes made during review
   - [x] Run [`codemetar::write_codemeta()`](https://docs.ropensci.org/codemetar/) to generate [codemeta.json](https://codemeta.github.io/)
   - [x] Add [R-universe](https://ropensci.org/r-universe/) installation instructions to README
   - [ ] Optionally acknowledge reviewers as "rev" in DESCRIPTION
2. **Editor** may tag blog editors suggesting a [blog post](https://blogguide.ropensci.org/)
3. **Editor** adds package to rOpenSci documentation
4. **Editor** closes the review issue
5. **Package appears** on rOpenSci website
6. **Optional**: Author may submit to [Journal of Open Source Software](https://joss.theoj.org/) (fast-tracked)
7. **Optional**: Author submits to CRAN/Bioconductor
8. **Author** reviews post-onboarding guides:
   - [Collaboration guide](https://devguide.ropensci.org/maintenance_collaboration.html)
   - [Releases guide](https://devguide.ropensci.org/maintenance_releases.html)
   - [Marketing guide](https://devguide.ropensci.org/maintenance_marketing.html)

## Key Characteristics

- **Timeline**: Typically 2-3 months total (minimum ~5-6 weeks)
- **Public & Transparent**: Everything happens in public GitHub issues
- **Iterative**: Not one-and-done like academic peer review
- **No rejection**: Process continues until package meets standards
- **Collaborative**: Authors and reviewers engage in dialogue
- **Highly Automated**: Bot handles checks, reminders, assignments, logging, and transfer
- **Volunteer-driven**: Editors and reviewers are unpaid volunteers
- **Community-focused**: Slack invitations for all participants

## Communication Happens Via:
- **GitHub issue thread** (primary communication)
- **Bot commands** (workflow automation)
- **Slack** (community connection and internal editor discussions)
- **Email** (recruiting reviewers)

## Bot Commands Reference

Full documentation: [Bot Commands Cheatsheet](https://devguide.ropensci.org/bot_cheatsheet.html)

| Command | Who Uses | Purpose |
|---------|----------|---------|
| `@ropensci-review-bot help` | Anyone | Get help with bot commands |
| `@ropensci-review-bot check package` | Anyone | Re-run automated pkgcheck |
| `@ropensci-review-bot assign @username as editor` | EIC | Assign editor to submission |
| `@ropensci-review-bot assign @username as reviewer` | Editor | Assign reviewer (auto-sets due date) |
| `@ropensci-review-bot set due date for @username to YYYY-MM-DD` | Editor | Change reviewer due date |
| `@ropensci-review-bot submit review <url> time <hours>` | Editor | Log review with hours spent |
| `@ropensci-review-bot approve <package>` | Editor | Approve package and post TODO list |
| `@ropensci-review-bot invite me to ropensci/<package>` | Author | Renew expired transfer invitation |
| `@ropensci-review-bot finalize transfer of <package>` | Author | Complete repository transfer |

## Key Templates Used:
- [**Submission template**](https://github.com/ropensci/software-review/issues/new/choose) - Used by authors when creating the issue
- [**Editor template**](https://devguide.ropensci.org/editortemplate.html) - Used by editors for initial checks
- [**Review request template**](https://devguide.ropensci.org/reviewrequesttemplate.html) - Used by editors to invite reviewers
- [**Review template**](https://devguide.ropensci.org/reviewtemplate.html) - Used by reviewers to conduct their review
- [**Approval template**](https://devguide.ropensci.org/approval2template.html) - Used by reviewers to formally approve
- **Editor approval comment** - Used by editors for final package approval

## Automated Bot Features

### On Submission:
- Welcome message
- Comprehensive pkgcheck report
- Statistical analysis and visualizations

### During Review:
- Assignment confirmations
- Due date reminders
- Reviewer form requests
- Label management

### On Approval:
- Comprehensive TODO list generation
- Repository transfer invitation
- Transfer finalization
- Admin access restoration

### Throughout Process:
- Can re-run checks on demand
- Logs review hours
- Manages workflow state
